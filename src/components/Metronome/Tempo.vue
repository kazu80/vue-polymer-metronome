<template>
    <mtrm-component :title="title" :params="serializeTempos" :val="tempo" type="slider"></mtrm-component>
</template>
<style>

</style>
<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks */
    export default {
        name    : 'MetronomeTempo',
        data () {
            return {
                title : 'TEMPO',
                tempo : 120,
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
        }
    }
</script>