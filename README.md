# SMS-CODE-INPUT
> SMS code input component for Vue2 

 [![vue2](https://img.shields.io/badge/vue-2.x-brightgreen.svg)](https://vuejs.org/)
 [![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/zdesign-ui/sms-code-input.git)
 [![npm](https://img.shields.io/npm/v/sms-code-input.svg)](https://www.npmjs.com/package/sms-code-input)

 sms-code-input is a dependency-free, lightweight vue component that can be overwrited by yourself.

## Usage

When you use it, you need to wrapper this component by an exact size container or element. (e.g: use <code>div</code> with definitely width)

### step-1
```
vue create demo
```
### step-2
```
cd demo
npm install sms-code-input
```

## Example
```
npm run serve
```
```vue
<template>
  <div style="width: 300px">
    <sms-code-input 
      :digits="counts"
      :color="color"
      :styles="styles"
      @change="onInputChange" 
      @complete="onInputComplete"
    >
    </sms-code-input>
  </div>
</template>
<script>
export default {
  data() {
    return {
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
    onInputChange(val) {
      console.log('input change: --->', val)
    },
    onInputComplete(val) {
      console.log('input complete: --->', val)
    }
  }
}
</script>
```

### Options
|    Property    |    Description   |   type   |	default	|
| -----------------  | ---------------- | :--------: | :----------: |
| digits         | the code numbers for the SMS  |Number| 6 |
| color          | the input border color  |String| '#af3737' |
| styles         | the custom styles for the input |Object | {} |

### Functions
|    Function Name   |    Description   |
| -----------------  | ---------------- |
| change             | trigger when input code changed   |
| complete           | tirgger when input code completed |