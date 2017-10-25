<template>
    <div id="app">

        <mtrm-header rootPath="/"></mtrm-header>

        <router-view/>
    </div>
</template>

<script>
    /* eslint-disable indent */

    export default {
        name: 'app'
    }
</script>

<style>
    #app {
        font-family             : 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing  : antialiased;
        -moz-osx-font-smoothing : grayscale;
        text-align              : center;
        color                   : #2c3e50;
    }

    mtrm-header {
        --background-color : #00aa88;
        --text-color: #fff;
        --font-weight: bold;
        text-align: left;
    }

</style>
