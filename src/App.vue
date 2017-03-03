<template>
  <div id="app">
  step: {{ step }}
    <home v-if="step == 0"></home>
    <step-1 v-if="step == 1"></step-1>
  </div>
</template>

<script>
import home from './home.vue';
import step1 from './step1.vue';
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      step: 0
    }
  },
  components: {home: home, step1: step1}
}
</script>

<style lang="scss">
@import url('./assets/css/style.css');
@import url('./assets/css/greater-blue.css');
</style>
