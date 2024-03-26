<template>
  <div id="app">
    <div class="code-input-container">
      <sms-code-input />
    </div>
  </div>
</template>

<script>
import SmsCodeInput from './sms-code-input/index.vue'
export default {
  name: 'App',
  components: {
    SmsCodeInput
  }
}
</script>

<style lang="scss">
.code-input-container {
  width: 300px;
}
</style>
