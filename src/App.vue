<template>
  <FirstCanvas />
  <!-- <SecondCanvas id="second"/> -->
</template>

<script>
import FirstCanvas from './components/FirstCanvas.vue';
// import SecondCanvas from './components/SecondCanvas.vue';

export default {
  name: 'App',
  components: {
    FirstCanvas,
    // SecondCanvas
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
/* #first {
    width: calc(50% - 2px);
    border-right: 2px dashed darkgray;
    float:left;
}

#second {
    width: calc(50% - 2px);
    float: right
} */

</style>
