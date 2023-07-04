---
layout: post
title: Day 13 - Introduction to Vue Router
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 12, we'll review everything we've learned about Vue.js components so far and put our knowledge into practice with hands-on exercises and mini-projects.
keywords: Vue.js, Components, Review, Practice, Exercises
---
# Day 13: Introduction to Vue Router

**Table of Contents**
- [Setting up Vue Router](#setting-up-vue-router)
- [Creating Routes and Linking Views](#creating-routes-and-linking-views)

Welcome to Day 13 of our Vue.js journey! Today, we'll dive into Vue Router, a powerful routing library that allows us to build single-page applications with ease. We'll learn how to set up Vue Router, create routes, and link views together to provide a seamless navigation experience.

## Setting up Vue Router

To get started with Vue Router, we need to install it and set it up in our Vue.js project. Here are the steps:

1. Install Vue Router via npm or yarn:

   ```bash
   npm install vue-router
   ```

2. Import Vue Router in your main.js file:

   ​```javascript
   import VueRouter from 'vue-router';
   ```

1. Use Vue Router as a Vue plugin:

   ```javascript
   Vue.use(VueRouter);
   ```

2. Create a new instance of VueRouter and pass in your routes configuration:

   ```javascript
   const router = new VueRouter({
     routes: [
       // Your routes configuration goes here
     ]
   });
   ```

3. Mount the router instance to your Vue instance:

   ```javascript
   new Vue({
     router,
     // Your other Vue options go here
   }).$mount('#app');
   ```

With these steps, you have successfully set up Vue Router in your Vue.js project.

## Creating Routes and Linking Views

Now that we have Vue Router set up, we can define our routes and link them to our views. Each route corresponds to a specific URL and maps to a component that will be rendered when that URL is accessed.

Here's an example of how to define routes and link them to views:

```javascript
const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/about', component: About },
    { path: '/contact', component: Contact }
  ]
});
```

In this example, we define three routes: one for the home page, one for the about page, and one for the contact page. Each route specifies a path and the component to be rendered when that path is accessed.

To render the views associated with the routes, we need to add a `<router-view>` component in our main template:

```html
<template>
  <div>
    <router-view></router-view>
  </div>
</template>
```

With the `<router-view>` component in place, Vue Router will dynamically render the appropriate component based on the current URL.

That's it for today! Tomorrow, we'll continue our exploration of Vue Router and learn about route parameters and navigation guards. Stay tuned!