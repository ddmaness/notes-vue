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

