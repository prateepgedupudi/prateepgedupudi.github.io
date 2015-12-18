---
layout:     post
title:      "How to dynamically change log level in SLF4j Log4J with Standalone Java Class"
subtitle:   "LogLevel change based on the log level choosen"
date:       2015-12-12 15:59:00
author:     "Prateep Gedupudi"
header-img: "img/Slflog4jinstandard.png"
---
<p>
	Many of us already know this, but logging is just a way of monitoring our application, and when used right this can provide you with information of what is happening during application’s runtime process.
</p>
<p>
	We can log errors and actions applications encounter, which is pretty critical. Logging other things can be very informative e.g. the start and end of a batch process, amount of processed files, duration within a certain method call and so on.
</p>
<p>
	We want the right kinds of information available to us, but don’t want to store tons of old logs that don’t mean anything to us a year later. We want to try to write concise informative messages that are self-explanatory and able to be dumped soon after, as needed.
</p>
<h3 class="section-heading">Here are some of logging levels</h3>
<ul class="list-group">
  <li class="list-group-item">ERROR label for actual errors</li>
  <li class="list-group-item">WARN for potential issues that can interfere with correct workings of the application but will not crash it.</li>
  <li class="list-group-item">INFO for messages announcing the start of your batch process</li>
  <li class="list-group-item">DEBUG and TRACE for all other things we don’t want to read in the future or only when really needed, like the type of implementations of certain interfaces loaded on startup. I believe if we are using the DEBUG or TRACE level to actually debug our application, we probably should have written a unit test that verifies that part of code we wrote full with debug statements</li>
</ul>

<h2 class="section-heading">Facade vs. Implementation</h2>
<p>
	JUL, Log4j 1.2, Log4j 2 and Logback are full-blown logging implementations. We can just use these directly.
	Apache Commons Logging and SLF4J are facades over actual logging implementations. Each of them does include an internal, simplistic logging implementation (“SimpleLog” for Commons Logging, “Simple” for SLF4J) but we are meant to use a real implementation in production
</p>
<img class="img-responsive center-block" src="/img/slf4jlog4jbinding.png" alt="">
<span class="caption text-muted">Slf4j and Log4j Binding</span>
<blockquote><a href="https://github.com/prateepgedupudi/Slf4jLog4jDemoApp.git">Code Download</a> </blockquote>

<div class="embed-responsive embed-responsive-16by9">
	<iframe width="1280" height="720" src="https://www.youtube.com/embed/9KJDWEyuhgE" frameborder="0" allowfullscreen></iframe>
</div>
