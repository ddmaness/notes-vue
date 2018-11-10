# [Vue Docs Essentials](https://vuejs.org/v2/guide/comparison.html)

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

Vue also allows you to build a website using small reusable components through the use of Vue's `component` method

## The Vue Instance

All Vue applications start with the a new instance of view by calling Vue's constructor

```javascript
  var vue = new Vue({
    \\ options object
  })
```

it adds all the properties found in the data object to it **reactivity system** meaning that changes in data will be reflected
in what the app displays

only data properties present during Vue's instantiation will be reactive so add them all even if they don't containd data yet

Vue instances also contain a number of methods, all of which are prefixed with `$` to prevent collision with user defined 
methods. check the [api reference](https://vuejs.org/v2/api/#Instance-Properties) for more details

Vue instances, like React instances, have several [lifecycle phases](https://vuejs.org/images/lifecycle.png) and you can add
code to any of these phases using **lifecycle hook** methods on the Vue instance.  by design `this` is bound to the Vue 
instance so arrow functions should be avoided.

## Template Syntax

text interpolation is achieved using the mustache syntax `{{ someText }}` which is responsive to changes in the interpolated
variable. if you don't want this updating behavior the `v-once` directive allows for one time interpolations on a node

The `v-html` directive allows the interpolation of html. though, this should never interpolate user provided content and
if the code needs to be reused or contain other components Vue.component may be a better option.

mustaches cannot be used inside of html attributes so use the `v-bind` directive instead.

Vue support full JS expressions in mustache and directive calls. however only single expressions are supported.

some directives take arguements or modifiers to change or dictate some part of their behaviour

Vue provides shorthands for two of the most frequently used directive `v-bind` and `v-on`

## Computed Properties and Watchers

Complex computed properties can get too verbose to be included in every interplation. for this use the `computed` property on the
Vue options object.  This can also be achieve by calling methods defined in the method property but using the computed property
is more performant as it uses caching to prevent unneccessary repeated computations. If for some reason caching needs to be
avoided use this method instead.

by default, computed properties are getters only but you can also provide a setter if needed

in most situations computed properties are more appropriate but the `watch` property is useful in cases when you want to perform
async or expensive operations when data changes

## Class and Style Bindings

To avoid the hassle of error prone string concatenation Vue provides special behavior for `class` and inline styles declared
through `v-bind`

passing an object to `v-bind:class` can allow for conditional classes declarations. these can exist alongside standard class
definitions. these objects don't have to be inline and can even be returned by a computed property that returns a class object.

Arrays can also be used. Classes can be toggled with a ternary operator element, or by simply using the object syntax as an
array element (less verbose)

any classes or class bindings added a custom component will be added to the root of the component and will not overide classes declared when that component is invoked

a similar process exists for declaring inline styles. Refer to documentation if needed.

## Conditional Rendering

the `v-if` and `v-else` directives are used to achieve conditional rendering. if a group of elements are conditional, the
directive must be attached to an invisible `<template>` wrapper that conditionally displays everything within it.  `v-else`
elements must immediately follow `v-if` or `v-else-if` statements or else they will be ignored. the `v-show` directive is 
similar to `v-if` but only toggles the elements `display` property in css. if something is going to be toggled frequently,
use `v-show` else use `v-if`

## List Rendering
