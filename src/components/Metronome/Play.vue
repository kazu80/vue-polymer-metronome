<template>
    <mtrm-component id="play" type="play" :params="params" :param="beatCount"></mtrm-component>
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
        name   : 'MetronomePlay',
        data () {
            return {
                params   : '',
                beatCount: 0
            }
        },
        mounted: function () {
            this.$el.addEventListener ('play', (e) => {
                // this.play ();
                console.log ('play');
            });
        }
    }
</script>