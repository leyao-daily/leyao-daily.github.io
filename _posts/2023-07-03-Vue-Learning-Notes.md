---
layout: post
title: Day 11 - Communication Between Components
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 11, we'll learn about communication between Vue.js components, focusing on parent-child component communication and the usage of props and events.
keywords: Vue.js, Components, Props, Events, Communication
---
# Day 11: Communication Between Components

**Table of Contents**
- [Understanding Parent-Child Component Communication](#understanding-parent-child-component-communication)
- [Using Props and Events for Communication](#using-props-and-events-for-communication)

On Day 11 of our Vue.js journey, we'll delve into a vital aspect of working with components: communication between components. Specifically, we'll focus on communication between parent and child components and the usage of props and events for this purpose.

## Understanding Parent-Child Component Communication

In Vue.js, components form a hierarchy similar to the Document Object Model (DOM). A component that uses another component in its template is considered the parent of the latter, which becomes the child. Communication between these parent and child components is fundamental to building complex applications.

There are two primary ways parent and child components communicate:

1. **Props Down**: The parent passes data down to the child via props.
2. **Events Up**: The child sends messages to the parent by emitting events.

## Using Props and Events for Communication

**Props** are custom attributes that you can register on a component. When a value is passed to a prop attribute, it becomes a property on that component instance. Here's an example of passing a prop from a parent to a child component:

```javascript
Vue.component('child-component', {
  props: ['message'],
  template: '<div>{{ message }}</div>'
})

new Vue({
  el: '#app',
  data: {
    parentMessage: 'Hello from parent!'
  }
})
```

In the template:

```html
<div id="app">
  <child-component :message="parentMessage"></child-component>
</div>
```

In this example, the `child-component` accepts a `message` prop, which is provided by the parent in the template.

**Events** allow child components to trigger actions in their parent components. A child component can use Vue's built-in `$emit` method to trigger an event that the parent can listen to. Here's an example:

```javascript
Vue.component('child-component', {
  methods: {
    notifyParent: function() {
      this.$emit('child-event');
    }
  }
})

new Vue({
  el: '#app',
  methods: {
    handleChildEvent: function() {
      console.log('Child event received!');
    }
  }
})
```

In the template:

```html
<div id="app">
  <child-component @child-event="handleChildEvent"></child-component>
</div>
```

In this example, when the `notifyParent` method is called in the `child-component`, it emits a 'child-event' that the parent component listens for.

That's all for today! Tomorrow, we'll continue our exploration of Vue.js components and learn about slots and dynamic components. Stay tuned!
