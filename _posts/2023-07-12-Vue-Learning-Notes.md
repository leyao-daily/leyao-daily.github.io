---
layout: post
title: Day 20 - Vue.js 3 Composition API - Computed and Watch
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 20, we'll explore computed and watch functions in the Vue.js 3 Composition API. We'll learn how to create computed properties and watchers using the Composition API to efficiently handle reactive data and perform side effects.
keywords: Vue.js, Composition API, Computed Properties, Watchers
---
# Day 20: Vue.js 3 Composition API - Computed and Watch

**Table of Contents**
- [Understanding Computed and Watch Functions in Composition API](#understanding-computed-and-watch-functions-in-composition-api)
- [Creating Computed Properties and Watchers with the Composition API](#creating-computed-properties-and-watchers-with-the-composition-api)

Welcome to Day 20 of our Vue.js journey! Today, we'll delve into the Vue.js 3 Composition API and explore the powerful concepts of computed and watch functions. We'll learn how to create computed properties and watchers using the Composition API, enabling us to efficiently handle reactive data and perform side effects when necessary.

## Understanding Computed and Watch Functions in Composition API

In the Composition API, computed functions allow us to define reactive values derived from other reactive values. Computed properties automatically update when their dependencies change, ensuring that our data remains up to date without manual intervention. Computed properties are especially useful for performing calculations or data transformations.

On the other hand, watch functions enable us to react to changes in specific reactive values and perform side effects. We can watch for changes in data and trigger custom logic such as making API calls, updating other variables, or executing specific actions. Watchers give us fine-grained control over when and how we respond to changes in our data.

## Creating Computed Properties and Watchers with the Composition API

To create computed properties and watchers using the Composition API, we can utilize the `computed` and `watch` functions.

Here's an example of creating a computed property and a watcher:

```javascript
import { computed, watch } from 'vue';

// Creating a computed property
const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`;
});

// Creating a watcher
watch(
  () => count.value,
  (newValue, oldValue) => {
    console.log(`Count changed from ${oldValue} to ${newValue}`);
  }
);
```

In this example, we create a computed property `fullName` using the `computed` function, which combines the values of `firstName` and `lastName`. Whenever `firstName` or `lastName` changes, the computed property will be automatically updated.

We also create a watcher using the `watch` function, which monitors changes in the `count` value. Whenever `count` changes, the watcher function is triggered, providing the new and old values for further processing.

Computed properties and watchers empower us to handle reactive data and perform related operations effectively within the Composition API.

That's it for today! Tomorrow, we'll continue our exploration of the Vue.js 3 Composition API and learn about using lifecycle hooks and providing reactive values with `provide` and `inject`. Stay tuned!
