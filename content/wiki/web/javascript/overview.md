---
title: Overview
description: An overview of JavaScript and related technologies
---

Overview
==========

ECMAScript, JavaScript, Java, asm.js
------------------------------------

ECMAScript is the standardized, versioned spec of JavaScript.


ECMAScript Support
------------------

The ES6 spec is expected to be finalized and implemented by the various browser vendors sometime mid / late 2015.

================= === ====================================
Browser           ES5 ECMAScript 2015  (ES6) (in progress)
================= === ====================================
Chrome            23+ Evergreen
Internet Explorer 9+  12+
Firefox           21+ Evergreen
================= === ====================================

Evergreen browsers automatically update to the latest version.

Transpiling ES6
------------------

Google Traceur is an ES6 to ES5 transpiler that can be used to develop in ES6 but target ES5 browsers.

TypeScript
------------------

TypeScript is a superset of ES6, driven by Microsoft.

It has 1st-class support in VS2013 Update 2 and onwards.

It also transcompiles, and allows targetting ES3, ES5 and later ES6.

Google were developing their own superset called AtScript, which was going to be used by Angular 2. However, Google are now using TypeScript instead.

Notable JavaScript luminaries
------------------

- Brendan Eich
- John Resig
- Douglas Crockford

JavaScript on the Desktop
------------------

You can script in Windows using JScript (instead of VBScript)

JavaScript as intermediate language
------------------

Google Web Toolkit (GWT) was perhaps the most notable early language to compile to JavaScript, in this case compiling a subset of Java to JavaScript.

Emscripten is an LLVM linker for compiling native code to JavaScript

Other notables are CoffeeScript, Dart.
