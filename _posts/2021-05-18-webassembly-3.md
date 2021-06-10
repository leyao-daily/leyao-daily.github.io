---
layout: post
title: Dive into WebAssembly - Toolchain
categories: Webassembly
description: TBD
keywords: WebAssembly, WASM, Web, JavaScript, Emscripten, Rust, AssemblyScript, Blazor
---
WebAssembly - Toolchain

* [Overview](#overview)
* [Language Specific Toolchains](#language-specific-toolchains)

## Overview

In this article, we will have a journey about how WebAssembly interoperates with its host environment and its current toolchain. 

## Language Specific Toolchains

### C/C++ with Emscripten

Emscripten was the very first toolchain for creating WebAssembly applications - in fact, it predates WebAssembly itself, being created in 2013 as part of the asm.js project.

Emscripten is based on the widely-used LLVM compiler toolchain. The process of compilation, stated in its most simplest form, takes a high-level language and compiles it to a number of architecture-specific binaries. The LLVM architecture simplifies that task by introducing an intermediate language (IR), allowing for a more pluggable architecture with multiple language front-ends, and architecture-specific back-ends.

![LLVM](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/llvm.jpg)

The Emscripten project uses the LLVM toolchain, and adds a WebAssembly back-end, allowing you to compile C and C++ applications to WebAssembly. WebAssembly modules have no built in I/O capabilities, in order to plug this gap, it also has comprehensive support for a wide range of existing APIs, including OpenGL (for 3D graphics), and SDL (which provides access to audio, keyboard, and other I/O capabilities). We can also make use of HTML APIs through the toolchain generated `glue code`.

For C/C++ developers, Emscripten is a comprehensive tool for WebAssembly development.

There are a number of notable applications which use Emscripten. Here are a few selected highlights:

- *AutoCAD* - a very popular desktop-based Computer Aided Design (CAD) package that supports engineers, architects, and designers across a wide range of industries. 
- *PSPDFKit* - provides a suite of tools for working with Portable Document Format (PDF) documents on a wide range of platforms. 
- *Google Earth* - was launched as a desktop application in 2001, giving users the opportunity to explore the globe via an immersive 3D experience.
- *Tensorflow* - a widely-used open source library for machine learning, allowing you to train and run complex neural networks within the browser. 



### Rust

Rust is a relatively new programming language, designed by the team at Mozilla and initially released in 2010. The language was designed to make it easy to create high performance multi-threaded applications, while avoiding many of the classic C++ security and memory safety pitfalls. With Mozilla’s active involvement in developing WebAssembly, it is only natural that Rust provides very good support.

Similar to Emscripten, Rust also uses the LLVM toolchain for the core task of compiling to WebAssembly. There is also a vibrant and active community of Rust developers creating associated tooling that helps bundle, distribute and optimize WebAssembly code. Probably the most notable is wasm-bindgen, a tool that generates the ‘glue code’ that is required in order to allow access to Web APIs and transfer complex types across the JavaScript/WebAssembly boundary.

Whereas Emscripten is most often used for compiling large-scale C++ codebases to WebAssembly, Rust tends to be the language of choice for green-field development. Here are a few examples:

- *Ditto* - a cross-platform database that allows you to synchronize data between devices without an internet connection. Their database is written in Rust, and runs on desktop, IoT, web and mobile devices. 
- *Makepad* - an online collaborative shader programming environment, where you can develop shaders using Rust. The output targets a wide range of platforms, including WebAssembly/WebGL, OSX/Metal, Windows DX11 and Linux/OpenGL.



### AssemblyScript

AssemblyScript is a subset of TypeScript (a popular superset of JavaScript that adds optional static typing), which has been carefully designed to allow compilation to WebAssembly. The advantages of WebAssembly (predictable performance, small payload, etc.) are equally desirable to JavaScript/TypeScript developers.

In common with Rust and C++, AssemblyScript is built on the LLVM toolchain, using the Binaryen tooling that was developed alongside Emscripten. The AssemblyScript runtime performs garbage collection through reference counting. It also provides a JavaScript-like standard library, which includes strings, arrays, and a (limited) date API.

AssemblyScript is a nascent language, with current users considered early adopters. Here are some related projects:

- *Micrio* - a story-telling platform that allows users to create 'deep zoom' experiences with narrative. Performance, and a wide-ranging browser support are very important for this commercial tool. 
- *Wasabi Chess Engine* - a fully featured chess engine that was written from scratch in AssemblyScript. It has been coupled with a React front-end to allow you to play against the engine directly in the browser.



### C# with Blazor

Blazor is a web application development framework that is part of Microsoft’s .NET framework. It started life in 2017.

Blazor is designed to be more than just a C#-to-WebAssembly compiler, it is intended to be a complete framework for building web-based applications, furthermore. The framework has a component-based UI framework, makes use of Razor (HTML templating), includes a router and many of the core .NET framework services.

A novel feature of Blazor is its runtime execution model. Your C# code (including razor templates) is not compiled directly into WebAssembly, it is instead compiled into a .NET assembly (or DLL), a ‘bytecode’ file that can be executed by the .NET runtime. These DLLs are loaded directly into the browser and executed by a .NET runtime that has been compiled to WebAssembly.

![Blazor](https://raw.githubusercontent.com/leyao-daily/leyao-daily.github.io/master/images/posts/webassembly/blazor.jpg)

In other words, Blazor applications ship a .NET runtime, which executes your application which is distributed as a number of assemblies.

This interpreted execution model does have some performance implications, and the need to ship a runtime also means that Blazor applications can be quite large. The team is working on Ahead-Of-Time (AOT) compilation that will compile applications directly to WebAssembly, removing the need for much of the runtime.