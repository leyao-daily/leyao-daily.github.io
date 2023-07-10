---
layout: post
title: Day 19 - Introduction to Vue.js 3 Composition API
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 19, we'll introduce the Composition API in Vue.js 3. We'll explore the advantages of using the Composition API and learn about reactive variables using ref and reactive.
keywords: Vue.js, Composition API, Reactive Variables, ref, reactive
---
# Day 19: Introduction to Vue.js 3 Composition API

**Table of Contents**
- [Understanding the Composition API and Its Advantages](#understanding-the-composition-api-and-its-advantages)
- [Introduction to Reactive Variables with ref and reactive](#introduction-to-reactive-variables-with-ref-and-reactive)

Welcome to Day 19 of our Vue.js journey! Today, we'll dive into the Composition API, a powerful addition to Vue.js 3 that provides a more flexible and modular approach to organizing our code. We'll explore the advantages of using the Composition API and learn about reactive variables using `ref` and `reactive`.

## Understanding the Composition API and Its Advantages

The Composition API is a new way of organizing and reusing logic in Vue.js components. It allows us to define component logic in a more granular and composable manner, making it easier to understand, test, and maintain our codebase. The Composition API promotes better separation of concerns and enables code reuse across different components.

Some advantages of using the Composition API include:

- **Modularity**: With the Composition API, we can encapsulate related logic into reusable functions, making our code more modular and easier to reason about.
- **Improved Organization**: The Composition API encourages organizing code based on functionality, leading to a more logical and structured codebase.
- **Better Code Reusability**: With the Composition API, we can easily extract and reuse logic across different components, reducing duplication and improving overall code reusability.
- **Type Safety**: The Composition API plays well with TypeScript, enabling enhanced type checking and providing better development experience for statically typed languages.

## Introduction to Reactive Variables with ref and reactive

Reactive variables are at the core of the Vue.js reactivity system, allowing us to create data that automatically updates when its dependencies change. In the Composition API, we have two main functions to create reactive variables: `ref` and `reactive`.

- **`ref`**: The `ref` function is used to create a reactive variable that holds a single value. It returns a **ref object**, and we can access the value using the `.value` property. When the value changes, the associated component will be updated.

- **`reactive`**: The `reactive` function is used to create a reactive object that can hold multiple values as properties. It returns a **reactive object**, and any changes to its properties will trigger updates in the associated component.

Here's an example of using `ref` and `reactive`:

   ```javascript
   import { ref, reactive } from 'vue';

   // Creating a reactive variable with ref
   const count = ref(0);
   console.log(count.value); // Output: 0

   // Creating a reactive object with reactive
   const state = reactive({
   name: 'John',
   age: 25,
   });
   console.log(state.name); // Output: John
   console.log(state.age); // Output: 25
   ```

In this example, we create a reactive variable `count` using `ref` and a reactive object `state` using `reactive`.

That's it for today! Tomorrow, we'll continue our exploration of the Vue.js 3 Composition API and learn about using computed properties and hooks. Stay tuned!
