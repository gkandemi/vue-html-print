# vue-html-to-paper
Vue mixin for paper printing html elements.

### Demo

https://mycurelabs.github.io/vue-html-to-paper/

### Install

**NPM**
```
npm install vue-html-to-paper
```
**Yarn**
```
yarn add vue-html-to-paper
```
**CDN**
```
https://unpkg.com/vue-html-to-paper/build/vue-html-to-paper.js
```

### Usage

**main.js**

```javascript
import Vue from 'vue';
import VueHtmlToPaper from 'vue-html-to-paper';

const options = {
  name: '_blank',
  specs: [
    'fullscreen=yes',
    'titlebar=yes',
    'scrollbars=yes'
  ],
  styles: [
    'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css',
    'https://unpkg.com/kidlat-css/css/kidlat.css'
  ]
}

Vue.use(VueHtmlToPaper, options);

// or, using the defaults with no stylesheet
Vue.use(VueHtmlToPaper);
```

See `window.open` API [here](https://www.w3schools.com/Jsref/met_win_open.asp).

**component**

```html
<template>
  <div>
    <!-- SOURCE -->
    <div id="printMe">
      <h1>Print me!</h1>
    </div>
    <!-- OUTPUT -->
    <button @click="print"></button>
  </div>
<template>

<script>
export default {
  data () {
    return {
      output: null
    }
  },
  methods: {
    print () {
      // Pass the element id here
      this.$htmlToPaper('printMe');
    }
  }
}
</script>
```

### With local options

You can also 

### Callback

Use the callback function to be notified when printing has been completed (whether or not it was successful). The callback method is not required.

**Notes**

> When using callback, be aware that there's now a 2nd argument for local options. So the callback will be the 3rd arg. Pass `null` as 2nd arg if you don't want to override the global options.

```js
this.$htmlToPaper('printMe', null, () => {
  console.log('Printing completed or was cancelled!');
});
```

### FAQ

**How to print in landscape**

In the global option, you can pass a css with the following: 

```css
@media print {
  @page {
    size: landscape
  }
}
```

Then, inject the custom css in the styles option like so:

```js
const options = {
  styles: [
    'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css',
    './path/to/custom.css' // <- inject here
  ]
}
```

This can also be done by using the local option.

Made with ❤️ by Jofferson Ramirez Tiquez
