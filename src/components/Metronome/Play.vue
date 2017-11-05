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
                params   : '',
                isPlay   : false,
                interval : 0,
                beat     : 0,
                beatCount: 0,
                tempo    : 100,
                context  : {}
            }
        },
        mounted: function () {
            this.context = new AudioContext ();
        },
        methods: {
            _observerSoundFileTempo: function () {

            },
            _observerSoundFileBeat : function () {

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
            }
        },
        watch  : {
            sound : function (val) {
                this._loadBufferFromURL (val, (buffer) => {
                    this.initialTempo (buffer, this.volume * 0.1);
                });
            },
            isPlay: function (val) {
                if (val) {
                    let count = 0;

                    this.interval = setInterval (() => {
                        //
                        count % this.beat === 0 ? this._playBeat () : this._playTempo ();

                        //
                        this.beatCount = count;

                        count++;
                    }, 60 * 1000 / this.tempo);
                } else {
                    if (this.interval) {
                        //
                        clearInterval (this.interval);

                        //
                        this.interval = 0;

                        //
                        this.beatCount = 0;
                    }
                }
            }
        }
    }
</script>