<template>
    <mtrm-component type="lifting" :title="title" :params="serializeBeats" :val="beat"></mtrm-component>
</template>
<style></style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        name: 'MetronomeBeat',
        data () {
            return {
                title: 'BEAT',
                beat : 1,
                beats: [
                    {id: 1, active: false},
                    {id: 2, active: false},
                    {id: 3, active: false},
                    {id: 4, active: false},
                    {id: 5, active: false},
                    {id: 6, active: false},
                    {id: 7, active: false},
                    {id: 8, active: false},
                ]
            }
        },
        computed: {
            serializeBeats: function () {
                return JSON.stringify (this.beats);
            }
        }
    }
</script>