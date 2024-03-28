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

```html
<div style="width: 300px">
  <sms-code-input></sms-code-input>
</div>
```

## Example
```
npm run serve
```

### Options
|    Property    |    Description   |   type   |	default	|
| -----------------  | ---------------- | :--------: | :----------: |
| digits         | the code numbers for the SMS  |Number| 6 |
| styles         | the custom styles you want to set |Object / Function | {} |