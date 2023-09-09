---
layout: post
title: Day 7 - Vue.js Methods and Computed Properties
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 7, we'll explore how to define and use methods in Vue.js and understand the power of computed properties.
keywords: Vue.js, Methods, Computed Properties
---
# Day 7: Vue.js Methods and Computed Properties

**Table of Contents**
- [Defining and Using Methods](#defining-and-using-methods)
- [Working with Computed Properties](#working-with-computed-properties)

On Day 7 of our Vue.js journey, we'll delve into two core aspects of Vue.js: methods and computed properties. Understanding these will allow us to create more dynamic and interactive web applications.

## Defining and Using Methods

In Vue.js, methods are functions we define in our Vue instance or components. We can use these methods to handle events, compute values, and more.

Defining a method in Vue.js is as simple as adding a methods property to our Vue instance:

```javascript
new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue!'
  },
  methods: {
    reverseMessage: function() {
      this.message = this.message.split('').reverse().join('');
    }
  }
})
```

In this example, we define a method called `reverseMessage` that reverses the characters of the `message` data property. To use this method, we can bind it to a button click event using the `v-on` directive:

```
htmlCopy code<div id="app">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

## Working with Computed Properties

Computed properties are like methods but with some key differences. Computed properties are cached based on their dependencies, and only re-evaluate when some of its dependencies have changed.

Here's an example of a computed property:

```javascript
new Vue({
  el: '#app',
  data: {
    firstName: 'John',
    lastName: 'Doe'
  },
  computed: {
    fullName: function() {
      return this.firstName + ' ' + this.lastName;
    }
  }
})
```

In this example, we define a computed property called `fullName` that returns the concatenation of `firstName` and `lastName`. We can use this computed property in our template like this:

```html
<div id="app">
  <p>{{ fullName }}</p>
</div>
```

That's it for today! Tomorrow, we'll continue our exploration of Vue.js with an understanding of watchers and their usage. Stay tuned!
