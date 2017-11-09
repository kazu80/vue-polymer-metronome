<template>
    <mtrm-component type="lifting" :title="title" :params="serializeBeats" :val="beat" @change="change"></mtrm-component>
</template>
<style></style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        props   : {
            beat: {
                type: Number,
            },
        },
        name    : 'MetronomeBeat',
        data () {
            return {
                title: 'BEAT',
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
        },
        methods : {
            change: function (val) {
                this.$emit ('change', val.detail.selected);
            }
        }
    }
</script>