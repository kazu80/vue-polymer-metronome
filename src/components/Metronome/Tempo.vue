<template>
    <div>
        <mtrm-component :title="title" :min="tempos.min" :max="tempos.max" :step="tempos.step" :val="tempo" type="slider"></mtrm-component>
    </div>
</template>
<style>

</style>
<script>
    /* eslint-disable indent,key-spacing */
    export default {
        name: 'MetronomeTempo',
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
        }
    }
</script>