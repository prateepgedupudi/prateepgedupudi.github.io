---
layout:     post
title:      "Asynchronous Module Definition (AMD)"
subtitle:   "Load all JS files separately, even when they are dependent on each other"
date:       2015-05-03 11:400:00
author:     "Prateep Gedupudi"
header-img: "img/post-bg-amd.jpg"
---

<p>The Asynchronous Module Definition API specifies a mechanism for defining modules such that the module and its dependencies can be asynchronously loaded. This is particularly well suited for the browser environment where synchronous loading of modules incurs performance, usability, debugging, and cross-domain access problems. This specification used to be called Modules Transport/C, but this is specification is not primarily geared for transported existing CommonJS modules, but for defining modules.</p>
