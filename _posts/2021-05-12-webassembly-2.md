---
layout: post
title: Dive into WebAssembly - A Simple WASM Module
categories: Webassembly
description: TBD
keywords: WebAssembly, WASM, Web, JavaScript
---
WebAssembly - A Simple WASM Module

* [Overview](#overview)
* [A Simple WASM Module](#a-simple-wasm-module)
* [Design Goals](#design-goals)

## Overview

*WebAssembly or wasm is a new portable, size- and load-time-efficient format suitable for compilation to the web.”*

It was designed for performance; designed to be compact; designed as a compilation target (C++, C, Rust, C#, Go and many more), and designed for the web. It can be considered as a compilation target for a wide range of languages.

## A Simple WASM Module

[WebAssembly Studio](https://webassembly.studio/) is an online WebAssembly `playground` with support for various languages, created by Mozilla.

Open up WebAssembly Studio and you will be initially prompted to select a project type. Select `Empty C Project`.

![Create a new project](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/Create_a_New_Project.png)

Ignore the files within the root folder of the project, these are part of the build process. Take a look at the `src` folder:

```markdown
- src/main.c, the C file that is compiled to wasm
- src/main.js, a simple JavaScript file that loads and executes the WebAssembly module
- src/main.html, a simple HTML file that loads the main.js script.
```

*Note: the **WASM_EXPORT** in `src/main.c` directive indicates that the compiled module should export this function so that it can be invoked by the host.*

Before we can run this example, the C file needs to be compiled to WebAssembly. Simply click the ‘Build’ option in the toolbar to kick off the compilation process. The output window should display the following:

***\*[info]: Task build is running...\****
***\*[info]: Task build is completed\****

You’ll notice that a new file, ***\*out/main.wasm\**** has appeared in the project folder structure.

Finally click the ‘Run’ option in the toolbar, and you should see a small window appear proudly displaying the number ‘42’.

We can simply change the `main.c` to create something a bit more realistic.

```c
#define WASM_EXPORT __attribute__((visibility("default")))

WASM_EXPORT
float power(float number, int pow) {
 float res = number;
   for (int i = 0;i < pow - 1; i++) {
     res = res * number;
   }
 return res;
}
```

Save and build, we can get the modified `wasm` file. To dive into it, right-click the generated wasm file and select `View as Binary`.  WebAssembly code is distributed as binary modules, making them both compact and efficient (fast to download, and fast to parse).

![view as binary](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/binary_format.png)

To make it readable, click the file to open it. And you will see its `Text Format`. This is exactly the same module  which is typically saved with the **wat** file extension, and is much more readable. There is a pretty simple mapping between the instructions you see in this file and the underlying binary representation.

![view as text format](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/Review_the_wasm_File_in_Text_Format.png)

WebAssembly feels quite assembly language-like in nature, having a low-level instruction set (of 67 instructions in its initial release); however, it does also have some more high-level concepts such as functions and loops. WebAssembly has a very simple type system, with only 4 types, all of which are numeric - two integers (32 and 64 bit) and two floating points (again 32 and 64 bit).

To clearly know how a WebAssembly module is executed, we take a close look at `main.js`:

```js
WebAssembly.instantiateStreaming(fetch("../out/main.wasm"))
 .then(({ instance }) => {
   // invoke the exported function
   const result = instance.exports.power(2, 5);
   document.getElementById("container").textContent = result;
});
```

Before a WebAssembly module is executed it needs to be downloaded. In the above code you can see that the fetch API is being used to load the wasm module, this function asynchronously returns a response object.

The WebAssembly namespace provides a number of functions for managing WebAssembly modules. In the example above, the `instantiateStreaming` function is used to read the response, compile and create an instance of the module. Finally, the exported function is located and invoked. 

WebAssembly modules cannot be loaded and executed by the browser directly, they must be downloaded, compiled and instantiated via JavaScript. The WebAssembly specification defines the concept of a ‘host’, which in this case is the browser’s JavaScript engine.  Also, WebAssembly functions are invoked synchronously, the JavaScript host `yields` to the module function, waiting until it returns before resuming.

---

## Design Goals

Early on in the process, a team with engineers from Mozilla, Google, Apple, Microsoft and various other organizations settled on a small collection of design goals that shaped the technology we use today. The most significant of these goals include:

- Minimum Viable Product (MVP) - designed to meet the needs of image processing, audio processing, computer aided design, games and various other applications that are computationally intensive. Focus on migration of existing applications and will be added incrementally over time.
- Security - WebAssembly modules run within a sandbox, which is isolated from the host environment. 
- Portability -  WebAssembly modules must be loaded by a host, and interoperate with the host in order to do anything meaningful. (rather than the `browser`, host can be a wide range of other environments, for example cloud, IoT or blockchain.)
- Performance
  - JavaScript is distributed in text format, WebAssembly is a binary.
  - JavaScript is not strongly typed, so optimization requires complex runtime monitoring. WebAssembly is strongly typed and can be compiled very quickly to the native machine code.
  - The WebAssembly binary format is designed to support parallel decoding across multiple threads and streamed instantiation.

