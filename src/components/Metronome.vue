<template>
    <main class="main-wrapper">
        <ul class="grid">
            <li>
                <metronome-tempo :tempo="tempo" @change="changeTempo"></metronome-tempo>
            </li>
            <li>
                <metronome-beat :beat="beat" @change="changeBeat"></metronome-beat>
            </li>
            <li>
                <metronome-sound :sound="sound" @change="changeSound"></metronome-sound>
            </li>
            <li>
                <metronome-volume :volume="volume" @change="changeVolume"></metronome-volume>
            </li>
            <li class="width-full-mobile">
                <metronome-play :tempo="tempo" :beat="beat" :sound="soundFile" :volume="volume"></metronome-play>
            </li>
        </ul>
    </main>
</template>

<style>
    :host {
        --margin-side            : 20px;
        --margin-side-mb         : 3vw;
        --margin-wrapper-main    : 0 var(--margin-side);
        --margin-wrapper-main-mb : 0 var(--margin-side-mb);
    }

    .main-wrapper {
        margin : 0 20px;
    }

    @media (max-width : 767px) {
        .main-wrapper {
            margin : 0 3vw;
        }
    }

    .grid {
        display         : var(--layout-horizontal_-_display);
        flex-direction  : var(--layout-horizontal_-_flex-direction);
        flex-wrap       : var(--layout-wrap_-_flex-wrap);
        justify-content : var(--layout-justified_-_justify-content);
        /* @apply(--layout-horizontal);
        @apply(--layout-wrap);
        @apply(--layout-justified); */
        margin          : 0 10px 32px 10px;
        padding         : 0;
        list-style      : none;
    }

    .grid li {
        -webkit-flex       : 1 1;
        flex               : 1 1;
        -webkit-flex-basis : 33%;
        flex-basis         : 33%;
        max-width          : 33%;
    }

    @media (max-width : 767px) {
        .grid {
            margin  : 0;
            padding : 0;
        }

        .grid li {
            -webkit-flex-basis : 48%;
            flex-basis         : 48%;
            max-width          : 48%;
        }
    }

    .width-full-mobile {

    }

    @media (max-width : 767px) {
        .width-full-mobile {
            max-width : 100% !important;
        }
    }
</style>

<script>
    /* eslint-disable indent,key-spacing,comma-dangle,semi,spaced-comment,padded-blocks,func-call-spacing */
    export default {
        name      : 'Metronome',
        data () {
            return {
                tempo    : 120,
                sound    : 1,
                beat     : 4,
                volume   : 5,
                soundFile: '',
            }
        },
        methods   : {
            changeTempo : function (val) {
                this.$data.tempo = val;
            },
            changeSound : function (val) {
                this.$data.soundFile = val;
            },
            changeBeat  : function (val) {
                this.$data.beat = val;
            },
            changeVolume: function (val) {
                this.$data.volume = val;
            }
        },
        components: {
            'metronome-tempo' : () => import('./Metronome/Tempo.vue'),
            'metronome-beat'  : () => import('./Metronome/Beat.vue'),
            'metronome-sound' : () => import('./Metronome/Sound.vue'),
            'metronome-volume': () => import('./Metronome/Volume.vue'),
            'metronome-play'  : () => import('./Metronome/Play.vue')
        }
    }
</script>