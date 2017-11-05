<template>
    <mtrm-component type="lifting" :title="title" :params="serializeSounds" :val="sound" @change="change"></mtrm-component>
</template>
<style scoped>
    mtrm-component {
        --display-font-size : 65px;
    }
</style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        name    : 'MetronomeSound',
        data () {
            return {
                title : 'SOUND',
                sound : 1,
                sounds: [
                    {id: 1, file: '/static/sound/s_01.mp3', active: false},
                    {id: 2, file: '/static/sound/s_02.mp3', active: false},
                    {id: 3, file: '/static/sound/s_03.mp3', active: false},
                    {id: 4, file: '/static/sound/s_04.mp3', active: false},
                ]
            }
        },
        computed: {
            serializeSounds: function () {
                return JSON.stringify (this.sounds);
            }
        },
        methods : {
            change: function (val) {
                const selected = val.detail.selected;
                const file = this.sounds[selected - 1].file;
                this.$emit ('change', file);
            }
        },
    }
</script>