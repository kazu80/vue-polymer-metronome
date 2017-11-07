<template>
    <mtrm-component id="play" type="play" :params="params" :param="beatCount" v-on:play="play"></mtrm-component>
</template>
<style scoped>
    mtrm-component {
        --wrapper-height    : auto;
        --wrapper-height-sp : auto;
        text-align          : left;
    }
</style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing,no-unused-vars */
    export default {
        props  : ['sound'],
        name   : 'MetronomePlay',
        data () {
            return {
                params          : '',
                isPlay          : false,
                interval        : 0,
                beat            : 4,
                beatCount       : 0,
                tempo           : 100,
                volume          : 5,
                context         : {},
                soundSourceTempo: {},
                soundSourceBeat : {},
                soundGainTempo  : {},
                soundGainBeat   : {},
            }
        },
        mounted: function () {
            this.context = new AudioContext ();

            // Tempo
            this._loadBufferFromURL ('/static/sound/s_01.mp3', (buffer) => {
                this.initialTempo (buffer, this.$data.volume * 0.1);
            });

            // Beat
            this._loadBufferFromURL ('/static/sound/s_02.mp3', (buffer) => {
                this.initialBeat (buffer, this.$data.volume * 0.1);
            });
        },
        methods: {
            play () {
                this.isPlay = !this.isPlay;
            },

            _loadBufferFromURL (url, callback) {
                const request = new XMLHttpRequest ();
                request.open ('GET', url, true);
                request.responseType = 'arraybuffer';

                request.onload = () => {
                    this.context.decodeAudioData (request.response,
                                                  function (buffer) {
                                                      if (!buffer) {
                                                          alert ('error decoding file data: ' + url);
                                                          return;
                                                      }

                                                      callback (buffer);
                                                  },
                                                  function (error) {
                                                      console.error ('decodeAudioData error', error);
                                                  }
                    );
                };

                request.onerror = function () {
                    alert ('BufferLoader: XHR error');
                };

                request.send ();
            },

            _playBeat () {
                this.$data.soundSourceBeat.start (0);
            },

            _playTempo () {
                this.$data.soundSourceTempo.start (0);
            },

            initialTempo (buffer, gain) {
                this.$data.soundSourceTempo = this.$data.context.createBufferSource ();
                this.$data.soundGainTempo = this.$data.context.createGain ();

                this.$data.soundSourceTempo.buffer = buffer;
                this.$data.soundGainTempo.gain.value = gain;

                this.$data.soundGainTempo.connect (this.$data.context.destination);
                this.$data.soundSourceTempo.connect (this.$data.soundGainTempo);

                this.$data.soundSourceTempo.onended = () => {
                    this.initialTempo (buffer, this.volume * 0.1);
                };
            },

            initialBeat (buffer, gain) {
                this.$data.soundSourceBeat = this.$data.context.createBufferSource ();
                this.$data.soundGainBeat = this.$data.context.createGain ();

                this.$data.soundSourceBeat.buffer = buffer;
                this.$data.soundGainBeat.gain.value = gain;

                this.$data.soundGainBeat.connect (this.$data.context.destination);
                this.$data.soundSourceBeat.connect (this.$data.soundGainBeat);

                this.$data.soundSourceBeat.onended = () => {
                    this.initialBeat (buffer, this.$data.volume * 0.1);
                };
            }
        },
        watch  : {
            sound : function (val) {
                this._loadBufferFromURL (val, (buffer) => {
                    this.initialTempo (buffer, this.$data.volume * 0.1);
                });
            },
            beat  : function (val) {
                this._loadBufferFromURL (val, (buffer) => {
                    this.initialBeat (buffer, this.$data.volume * 0.1);
                });
            },
            isPlay: function (val) {
                if (val) {
                    let count = 0;

                    this.$data.interval = setInterval (() => {
                        //
                        count % this.$data.beat === 0 ? this._playBeat () : this._playTempo ();

                        //
                        this.$data.beatCount = count;

                        count++;
                    }, 60 * 1000 / this.$data.tempo);
                } else {
                    if (this.$data.interval) {
                        //
                        clearInterval (this.$data.interval);

                        //
                        this.$data.interval = 0;

                        //
                        this.$data.beatCount = 0;
                    }
                }
            }
        }
    }
</script>