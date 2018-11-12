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

`v-for` can be used to render a list of items based on the elements in an array. For loops also have access to parent scope and
can take the index of an item as it's second arguement, either `in` or `of` can be used as the delimiter, they are equvalent

`v-for` can also be used to iterate through the values of properties in an object. an optional second arguement will provide
the key of the property, and an optional third for the index (do not trust if order is important).

Like in react, elements generated by the for directive should be given a unique key.

Vue cannot detect if an array item is modified directly using its index. Use an array method `splice` or Vue method `set` 
instead for array modification

it is possible to make new properties reactive only be adding them to a nested object using Vue's `set` method

If youd like to display a filtered or sorted array without changing the original, a computed property should be used. methods
can be used if using computed properties are not possible.

`v-for` optionally can take an interger to repeat a template x number of times

a invisible `<template>` can also be used with `v-for` to repeat blocks of elements

`v-for` always takes priority over `v-if` so the for loop will always run with only some elements be rendered. in instead of
this behavior you want execution of the for loop to be conditional, the if directive needs to be placed on the parent element
or an `<template>` wrapper.

you can use `v-for` on components as well, if doing this, data needs to be passed as props to the component

## Event Handling

The `v-on` directive is used for event handling whichcan take js directly or (more appropriately) a method. if invoking the 
event handler function using an inline statement, to pass the event if needed, use the special `$event` 

several event modifiers exist on the `on` directive to hand dom event behavior.  the directive also has various key modifiers
available if needed and custom ones can be declared, including adding key modifiers or requiring exact key presses

## Form Input Bindings

`v-model` is used to establish links for form input, textarea, and select elements. The default behavior of checkbox, radio,
and select can be modified with the `v-bind` directive. several modifiers on `v-model` exist to change the way it handles
the dataon a form field.  `v-model` works with custom form compoenents as well.

## Components

accept all the same options as `new Vue` (since they are just Vue instances) with the exception of a few root specific options

A component's data option must be a function. To ensure that each maintains its own state.

Components can be registered either locally or globally (available for use in all other components)

data can be passed down to components as props. once a prop is registered it can be passed data through a custom attribute

`v-bind` can be used to dynamically pass props in a `v-for` loop from the data property.

like in React every component may only have a single root element.  Use wrappers as needed.

The `$emit` method is used to pass the name of an event up to the parent component. `v-on` can then be used in the parent
component to listen for the emitted event. This works kind of like message passing. `$emit`'s second parameter is optionally
used to pass along a value, which will be accessable as either `$event` or as the first parameter on a method

`<slot>` elements are used to pass content into a component

dynamically switching components is made possible with the `is` special attribute



