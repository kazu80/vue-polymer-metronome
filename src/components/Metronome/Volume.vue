<template>
    <mtrm-component type="lifting" :title="title" :params="serializeVolume" :val="volume" @change="change"></mtrm-component>
</template>
<style></style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        props   : {
            volume: {
                type: Number,
            },
        },
        name    : 'MetronomeVolume',
        data () {
            return {
                title  : 'VOLUME',
                volumes: [
                    {id: 1, active: false},
                    {id: 2, active: false},
                    {id: 3, active: false},
                    {id: 4, active: false},
                    {id: 5, active: false},
                    {id: 6, active: false},
                    {id: 7, active: false},
                    {id: 8, active: false},
                    {id: 9, active: false},
                ],
            }
        },
        computed: {
            serializeVolume: function () {
                return JSON.stringify (this.volumes);
            }
        },
        methods : {
            change: function (val) {
                this.$emit ('change', val.detail.selected);
            }
        }
    }
</script>