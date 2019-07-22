<template>
  <div id="app">
      <arm-bandit></arm-bandit>
  </div>
</template>

<script>
import ArmBandit from './view/ArmBandit.vue'
export default {
  name: 'App',
  components: {
    ArmBandit
  }
}
</script>

<style lang="scss">
    @import './assets/scss/common.scss';
</style>

