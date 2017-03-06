<template>
  <div id="app">
    <home v-if="step == 0"></home>
    <step-1 v-if="step == 1"></step-1>
    <step-2 v-if="step == 2"></step-2>
    <step-3 v-if="step == 3"></step-3>
    <step-4 v-if="step == 4"></step-4>
  </div>
</template>

<script>
import home from './home.vue';
import step1 from './step1.vue';
import step2 from './step2.vue';
import step3 from './step3.vue';
import step4 from './step4.vue';
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      step: 0,
      result: {
        oblation: "",
        familyName: ""
      }
    }
  },
  components: {home: home, step1: step1, step2: step2, step3: step3, step4: step4}
}
</script>

<style lang="scss">
@import url('./assets/css/style.css');
@import url('./assets/css/greater-blue.css');
</style>
