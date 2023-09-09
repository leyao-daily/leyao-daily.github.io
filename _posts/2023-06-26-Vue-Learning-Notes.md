---
layout: post
title: Day 4 - Vue.js Instance and Directives - Part 1
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 4, we dive into the Vue instance and its lifecycle, properties, and methods. We also begin our exploration of Vue.js directives with v-if and v-else.
keywords: Vue.js, Vue Instance, Directives, v-if, v-else
---
# Day 4: Vue.js Instance and Directives - Part 1

**Table of Contents**
- [Understanding the Vue Instance](#understanding-the-vue-instance)
- [Introduction to Vue.js Directives: v-if, v-else](#introduction-to-vuejs-directives-v-if-v-else)

As we move into the fourth day of our Vue.js journey, we start looking at the code that powers Vue.js applications. Today, we'll dive into the Vue instance and its lifecycle, properties, and methods. We'll also introduce Vue.js directives, focusing on the v-if and v-else directives.

## Understanding the Vue Instance

The Vue instance is the heart of every Vue.js application. Each Vue instance goes through a series of initialization steps when it's created - for example, it needs to set up data observation, compile the template, mount the instance to the DOM, and update the DOM when data changes. 

A Vue instance is created by using the Vue constructor:

```javascript
let vm = new Vue({
  // options
})
```

The Vue instance has a series of properties and methods that allow you to manipulate the instance and its data:

- **Data Properties:** The data object for the Vue instance. Any properties you declare in the data object will be reactive, meaning Vue will watch for changes to these properties and update the DOM automatically when they change.
- **Computed Properties:** Computed properties are functions that are used as properties. They can be used to perform calculations or processing based on your data properties.
- **Methods:** Methods are functions that you can call from your Vue instance or from your component's template.
- **Lifecycle Hooks:** Lifecycle hooks are special methods that get called at different stages of the instance's lifecycle, such as created, mounted, updated, and destroyed. You can use these hooks to run code at specific times in your component's lifecycle.

## Introduction to Vue.js Directives: v-if, v-else

Vue.js directives are special attributes with the v- prefix that you can use in your templates. They apply special reactive behavior to the rendered DOM. Today, we'll focus on two directives: v-if and v-else.

The v-if directive is used to conditionally render a block. The block will only be rendered if the directive's expression returns a truthy value. Here's an example:

```html
<p v-if="showMessage">Hello, world!</p>
```

In this example, the paragraph will only be rendered if the showMessage property of the Vue instance is true.

The v-else directive can be used to render a block only when the preceding v-if condition is false:

```html
<p v-if="showMessage">Hello, world!</p>
<p v-else>No message to show.</p>
```

In this example, "Hello, world!" will be displayed if showMessage is true, and "No message to show." will be displayed if showMessage is false.

That's it for today! Tomorrow, we'll continue our exploration of Vue.js directives with v-for and v-on. Stay tuned!
