<template>
  <div class="code-container">
    <input
      v-for="(code, index) in codes"
      type="number"
      pattern="[0 - 9]"
      :ref="iRefs[index]"
      :key="`input-key-${index}`"
      :data-id="index"
      :value="code"
      class="code"
      :style="getCustomStyles(index)"
      autofocus="true"
      v-on:input="onValueChange"
      v-on:focus="onFocus(index)"
      v-on:blur="onBlur"
      v-on:keydown="onKeyDown"
      oninput="if (value.length > 1) { value = value.slice(0, 1) }"
    />
  </div>
</template>
<script>
const KEYBOARD_CODE = {
  backspace: 8,
  left: 37,
  up: 38,
  right: 39,
  down: 40
}

export default {
  name: 'SMSCodeInput',
  props: {
    // 验证码位数
    digits: {
      type: Number,
      default: 6
    },
    // input color
    color: {
      type: String,
      default: '#af3737'
    },
    // 用户自定义样式
    styles: {
      type: Object,
      default: () => {}
    }
  },
  data () {
    const { digits } = this
    this.iRefs = []
    for (let i = 0; i < digits; i++) {
      this.iRefs.push(`code_input_${i}`)
    }
    // 根据传入的digits设置code input数量
    const codes = Array(digits).fill('')

    return {
      customStyles: '',
      focusedIndex: null, // 跟踪当前获得焦点的输入框的索引
      isFocus: false,
      codes: codes
    }
  },
  methods: {
    getCustomStyles (index) {
      if (this.focusedIndex === index) {
        return {
          border: `1px solid ${this.color}`,
          caretColor: `${this.color}`,
          ...this.styles
        }
      } else {
        return {
          ...this.styles
        }
      }
    },
    onKeyDown (e) {
      // 禁止输入 +,-,e等字符
      if (e.code === 'KeyE' || e.code === 'Minus' || e.code === 'Equal') {
        e.preventDefault()
      }
      const index = parseInt(e.target.dataset.id)
      const prev = this.iRefs[index - 1] // 如果index=0时，数组下标为-1, prev为 undefined
      const next = this.iRefs[index + 1]

      switch (e.keyCode) {
        // 键盘按下向左键
        case KEYBOARD_CODE.left: {
          if (prev) {
            // 不要移除，否则光标会出现在数字左侧
            e.preventDefault()
            this.$refs[prev][0].focus()
          }
          break
        }
        // 键盘按下向右键
        case KEYBOARD_CODE.right: {
          if (next) {
            // 不要移除，否则光标会出现在数字左侧
            e.preventDefault()
            this.$refs[next][0].focus()
          }
          break
        }
        // 键盘按下回退键
        case KEYBOARD_CODE.backspace: {
          e.preventDefault()
          const vals = [...this.codes]
          if (this.codes[index]) {
            vals[index] = ''
            this.codes = vals
            if (prev) {
              const element = this.$refs[prev][0]
              element.focus()
              element.select()
            }
            this._triggerChanged(vals)
          }
          break
        }
        // 键盘按下上、下键
        case KEYBOARD_CODE.up:
        case KEYBOARD_CODE.down: {
          e.preventDefault()
          break
        }
        default:
          break
      }
    },
    onValueChange (e) {
      const index = parseInt(e.target.dataset.id)
      const value = e.target.value.replace(/[^\d]/gi, '') // e.target.value
      this.codes[index] = value

      const next = this.iRefs[index + 1]
      if (next) {
        const element = this.$refs[next][0]
        element.focus()
        element.select()
      }
      this._triggerChanged(this.codes)
    },
    onFocus (idx) {
      this.focusedIndex = idx
      this.isFocus = true
    },
    onBlur () {
      // 处理失去焦点事件
      this.focusedIndex = null
      this.isFocus = false
    },
    _triggerChanged (values = this.codes) {
      const flag = values.every(val => val !== '')
      if (flag) {
        this.$emit('complete', values)
      } else {
        this.$emit('change', values)
      }
    }
  }
}
</script>
<style>
.code-container {
  display: flex;
  justify-content: space-between;
  .code {
    caret-color: transparent;
    height: 36px;
    width: 25px;
    border: 1px solid #dcdfe6;
  }
  input {
    text-align: center;
    border-radius: 4px;
  }
  input:focus {
    outline: none;
    border: 1px solid #af3737;
    caret-color: #af3737;
  }
  input[type=number] {
    appearance: textfield;
  }
  input[type=number]::-webkit-inner-spin-button,
  input[type=number]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
}
</style>
