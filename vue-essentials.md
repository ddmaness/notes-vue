# [Vue Docs Essentials](https://vuejs.org/v2/guide/comparison.html)

## Declarative Rendering

Vue allows what user's see in the app reflect changes the apps data

```html
<div id ="app">
  {{ message }}
</div>
```
```javascript
var app = new Vue({
  el: '#app'
  data: {
    message: 'Hello World'
  }
})
```

Vue can also be used to bind element attributes

conditional **directives** like `v-if` can control what info gets rendered to the dom as well as the dom structure --
even applying transition effects!

Vue can also loop through an array of data with its `v-for` directive

`v-on` allows you to attach event listeners to elements on the page

`v-model` allows the app state to reflect user input a task that can be a bit of a choir in React
