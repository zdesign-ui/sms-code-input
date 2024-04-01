<template>
  <div id="app">
    <div class="title">{{ title }}</div>
    <div class="code-input-container">
      <sms-code-input
        :digits="counts"
        :color="color"
        :styles="styles"
        @change="onInputChange"
        @complete="onInputComplete"
      />
    </div>
  </div>
</template>

<script>
import SmsCodeInput from './sms-code-input/index.vue'
export default {
  name: 'App',
  components: {
    SmsCodeInput
  },
  data () {
    return {
      title: 'Examples',
      counts: 4,
      color: '#409eff',
      styles: {
        height: '50px',
        width: '30px',
        fontSize: '20px',
        color: '#275edb'
      }
    }
  },
  methods: {
    onInputChange (val) {
      console.log(val)
    },
    onInputComplete (val) {
      console.log(val)
    }
  }
}
</script>

<style lang="scss">
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  .title {
    font-size: 24px;
    font-weight: bold;
    color: #333;
    padding: 20px 0;
  }
  .code-input-container {
    width: 200px;
  }
}
</style>
