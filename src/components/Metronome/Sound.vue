<template>
    <mtrm-component type="lifting" :title="title" :params="serializeSounds" :val="sound"></mtrm-component>
</template>
<style scoped>
    mtrm-component {
        --display-font-size : 65px;
    }
</style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        name: 'MetronomeSound',
        data () {
            return {
                title : 'SOUND',
                sound : 1,
                sounds: [
                    {id: 1, file: '../../sound/s_01.mp3', active: false},
                    {id: 2, file: '../../sound/s_02.mp3', active: false},
                    {id: 3, file: '../../sound/s_03.mp3', active: false},
                    {id: 4, file: '../../sound/s_04.mp3', active: false},
                ]
            }
        },
        computed: {
            serializeSounds: function () {
                return JSON.stringify (this.sounds);
            }
        }
    }
</script>