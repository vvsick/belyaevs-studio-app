<template>
  <div id="app">
    <Stopwatch />
  </div>
</template>

<script>
import Stopwatch from './components/StopwatchComponent.vue'

export default {
  name: 'App',
  components: {
    Stopwatch
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  background-color: #353638;
}

#app {
  font-family: GothamPro;
  font-size: 22px;
  font-weight: 400;
  line-height: 21px;
  text-align: center;
  color: #9E9E9E;
  width: 100%;
  height: 100%;
}
</style>

