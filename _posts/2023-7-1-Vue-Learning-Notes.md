---
layout: post
title: Day 9 - Review and Practice - Methods, Computed Properties, Watchers
categories: ['Vue.js', 'JavaScript', 'Web Development']
description: On Day 9, we'll review methods, computed properties, and watchers in Vue.js, then put our knowledge into practice with hands-on exercises and mini-projects.
keywords: Vue.js, Review, Practice, Methods, Computed Properties, Watchers, Exercises, Projects
---
# Day 9: Review and Practice: Methods, Computed Properties, Watchers

**Table of Contents**
- [Reviewing Methods, Computed Properties, and Watchers](#reviewing-methods-computed-properties-and-watchers)
- [Hands-on Exercises and Mini-Projects](#hands-on-exercises-and-mini-projects)

Welcome back to our Vue.js learning journey! Today is Day 9, and we'll take the opportunity to review the important concepts we've covered so far: methods, computed properties, and watchers. After the review, we'll put our knowledge to the test with some hands-on exercises and mini-projects.

## Reviewing Methods, Computed Properties, and Watchers

Let's briefly recap the main points about methods, computed properties, and watchers:

- **Methods:** Functions defined inside the Vue instance or components. They can handle events, compute values, and more.
- **Computed Properties:** Like methods, but with a cache mechanism. They only re-evaluate when their dependencies change, making them efficient for expensive operations.
- **Watchers:** They monitor changes on data properties and run a function when a change is detected. Useful for performing side effects in response to data changes.

## Hands-on Exercises and Mini-Projects

Now, let's dive into some exercises and mini-projects:

**Exercise 1: Using Methods**

Create a Vue instance with a `count` data property and a `incrementCount` method. Use the `incrementCount` method to increase the `count` whenever a button is clicked.

**Exercise 2: Using Computed Properties**

Extend the above Vue instance by adding a `doubleCount` computed property. This computed property should return the double of the `count` data property.

**Exercise 3: Using Watchers**

Add a watcher to the above Vue instance to watch the `count` data property. Whenever the `count` changes, log a message to the console.

**Mini-Project: Interactive Quiz**

Combine what you've learned to create an interactive quiz. The quiz should have multiple questions, and each question should have multiple choice answers. The user should be able to select an answer for each question, and at the end of the quiz, the total score should be displayed.

That's all for today! Keep practicing and applying what you've learned. Tomorrow, we'll move into a new and exciting area of Vue.js: components. See you then!
