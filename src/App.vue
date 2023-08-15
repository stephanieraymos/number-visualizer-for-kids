<template>
    <number-visualizer />
</template>

<script>
import NumberVisualizer from './components/NumberVisualizer.vue';

export default {
    name: 'App',
    components: {
        NumberVisualizer,
    },
};
</script>

<style>
#app {
    margin: 0;
    padding: 0;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    min-height: 100vh; /* Ensure the app takes at least the full viewport height */
    display: flex; /* Use flexbox to align the content vertically */
    flex-direction: column; /* Align the content vertically */
    --dark-color-1: #333333;
    --dark-color-2: #414141;
    --dark-color-3: #454242;
    --light-color-1: #f2f2f2;
    --light-color-2: #e6e6e6;
    --light-color-3: #d9d9d9;

    --color-red: #770202;
    --color-green: #0b7702;
    --color-blue: #020277;

    background-color: var(--dark-color-1);
}
body {
    margin: 0;
    padding: 0;
}
</style>
