<template>
    <mtrm-component :title="title" :params="serializeTempos" :val="tempo" type="slider" @change="change"></mtrm-component>
</template>
<style>

</style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        props   : {
            tempo: {
                type: Number,
            },
        },
        name    : 'MetronomeTempo',
        data () {
            return {
                title : 'TEMPO',
                tempos: {
                    min : 1,
                    max : 255,
                    step: 1
                }
            }
        },
        computed: {
            serializeTempos: function () {
                return JSON.stringify (this.tempos);
            }
        },
        methods : {
            change: function (val) {
                const value = val.detail.value;

                // 何故か値が変化した時に、正常にemitした後に、undefindでもう一度送られるので、if文を置く
                if (value) {
                    this.$emit ('change', value);
                }
            }
        },
    }
</script>