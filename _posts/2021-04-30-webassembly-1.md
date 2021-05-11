---
layout: post
title: Dive into WebAssembly - Overview and History
categories: Webassembly
description: TBD
keywords: WebAssembly, WASM, Web, JavaScript
---
WebAssembly - Overview and History

* [Overview](#overview)
* [World Wide Web](#word-wide-web)
  * [History](#history)
  * [Why WebAssembly](why-webassembly)
* [Before Webassembly](before-webassmebly)

## Overview

WebAssembly is a language as the fourth official language of the web and the latest technology to be added to the web toolkit (alongside HTML, JavaScript and CSS).

The web has become the most ubiquitous platform for content and application distribution, however, the only programming language that this platform supports is JavaScript over the past few decades. To bring languages such as Java and C# to the browser via the plugin model, WebAssembly is created as a new runtime that lives alongside the JavaScript virtual machine. 

It provides a secure, fast and efficient compilation target for a wide range of modern programming languages, allowing them to target the browser. 

WebAssembly is also gaining traction beyond the web, the simplicity of the runtime and the lightweight sandbox it provides for execution of potentially untrusted code makes it a good candidate for many different use cases, such as potential applications in blockchain, Serverless, edge-computing and IoT.

---

## World Wide Web

The World Wide Web (or web) is ubiquitous, running on practically every internet-connected device we own, and indeed running much of our daily lives. The web gives us rapid access to content from ~2 billion websites, but more than that, it is a platform for business tools ranging from simple todo lists, right up to fully-featured spreadsheets.

### History

1980s - 1990s Web was invented in the 1980s, which connected a number of pre-existing computer networks for rapid information and content sharing. `HTTP` - Hypertext Transfer Protocol and `HTML` Hypertext Markup Language are the cornerstones of the internet. The most significant invention was the lowly hyperlink, which allows authors to reference documents from other pages and websites (seamless navigability). As the web grew, the `book like` web experience became dynamic. In 1996, Macromedia Flash (later acquired by Adobe) and Java Applets were introduced as `plugins`. Flash were ideal for web comics and games where it found great success. In contrast, Java Applets was limited.

2000s Flex in 2004 and Silverlight in 2007 prove the plugin model was very much in its heyday. The `native` web technologies of `JS`, `CSS`, `HTML` were still very much used for rendering static contents. While Rich Internet Application were booming, the web was changing. The web can be accessible on more devices, instead of desktop computers as the portal onto the web. In these cases, Flash and Silverlight can not work well because its resource hungry, so they died out after Steve Jobs `Thoughts of Flash`.  The capabilities of browser were evolving as new API were added, JavaScript was maturing as a a language, together with AJAX, it create interactive app-like experience.

2010s - Present Forward to 2014, `HTML5` was firmly targeted at adding the capabilities required to support app-like experiences within the browser without the need for plugins, it is now synonymous with `HTML`. The JavaScript execution engines sit within browser are now really quite fast.

### Why WebAssembly

- JavaScript applications are rich and interactive, however, the way in which they are sent and executed by the client is highly inefficient. e.g. video editing, computer aided design, streaming and AI

  ![Convoluted Path](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/js.jpg)

- There are many different languages that have been numerous attempted to be brought onto the Web. And the only way to bring a new language to the Web is for it to compile to JavaScript (never be designed to be a compilation target)

- JavaScript performance is generally quite good, but unpredictable, and not suitable for various applications

- JavaScript is not a good compilation target, which makes it difficult to bring other languages to the web

In conclusion, JavaScript is not a perfect solution, especially for applications that require consistent performance, furthermore it is not an ideal compilation target, making it hard to migrate legacy codebases to run within the browser.

---

## Before WebAssembly

To skip as many of the time-consuming steps involved in JavaScript execution, in order to reach peak  performance,`asm.js` a Mozilla project that first emerged in 2013, which create a C++ compiler that generated a struct subset of JavaScript (remove garbage collection, various runtime optimizations). 

​	![Convoluted Path](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/asm.jpg)

However, `asm.js` worked within the constraints of JavaScript itself. (delivered as plain text, parser into AST). But its fantastic success is basically a proof of concept for WebAssembly and many design decisions are adopted by WebAssembly.
