<template>
  <div id="app">
    <home>test</home>
    <!-- <step-1></step-1> -->
  </div>
</template>

<script>
import home from './home.vue';
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      status: null
    }
  },
  components: {home: home}
}
</script>

<style lang="scss">
@import url('./assets/css/style.css');
</style>
