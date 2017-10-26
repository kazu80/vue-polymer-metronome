<template>
    <main class="main-wrapper">
        <ul class="grid">
            <li>
                <metronome-tempo></metronome-tempo>
            </li>
            <li>
                <metronome-beat></metronome-beat>
            </li>
            <li>
                <metronome-sound></metronome-sound>
            </li>
            <li>
                <metronome-volume></metronome-volume>
            </li>
            <li class="width-full-mobile">
                <metronome-play></metronome-play>
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
        margin : var(--margin-wrapper-main);
    }

    @media (max-width : 767px) {
        .main-wrapper {
            margin : var(--margin-wrapper-main-mb);
        }
    }

    .grid {
        @apply(--layout-horizontal);
        @apply(--layout-wrap);
        @apply(--layout-justified);
        margin     : 0 10px 32px 10px;
        padding    : 0;
        list-style : none;
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
    /* eslint-disable indent */
    export default {
        name      : 'Metronome',
        data () {
            return {
                msg: 'This is Metronome'
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