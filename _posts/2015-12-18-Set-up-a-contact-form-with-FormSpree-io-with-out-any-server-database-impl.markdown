---
layout:     post
title:      "How to set up a contact form with FormSpree.io with out any server/database impl"
subtitle:   "Functional HTML forms with no server/database"
date:       2015-12-18 15:27:00
author:     prateep_gedupudi
header-img: "img/JekyllContactSubmittion.png"
---
<p>
	I recently moved my blog from WordPress to Jekyll after experimenting with Jekyll as a documentation platform for the past several months. Jekyll also loads more quickly.
</p>
<p>
	Erlier I was using php for form submission. But now in jekyll we do not have support for php in github. We need to handle any thing with only java script. When I was searching for a contact form submission to a mail, I found some interesting service website to do the same from java script. 
	It is nothing but <a href="http://formspree.io/">formspree io</a>. 
</p>
<p>
	While coming to the details of formspree io, it sends the submitted form as a text to your mensioned email.You don't even have to register. Just send your form to the URL and it will forward it to your email. No PHP, Javascript or sign up required — perfect for static sites!
</p>
<h2 class="section-heading">Setting it up is easy and free</h2>
<p>
	Lets take below example of code.
</p>
<p>
	<pre>
		<code class="language-html" data-lang="html"><span class="nt">&lt;form</span> <span class="na">action=</span><span class="s">&quot;//formspree.io/your@email.com&quot;</span><span class="nt">&gt;</span>
		  Email: <span class="nt">&lt;input</span> <span class="na">type=</span><span class="s">&quot;text&quot;</span> <span class="na">name=</span><span class="s">&quot;name&quot;</span><span class="nt">&gt;&lt;br&gt;</span>
		  Name: <span class="nt">&lt;input</span> <span class="na">type=</span><span class="s">&quot;text&quot;</span> <span class="na">name=</span><span class="s">&quot;email&quot;</span><span class="nt">&gt;&lt;br&gt;</span>
		  Subject: <span class="nt">&lt;input</span> <span class="na">type=</span><span class="s">&quot;text&quot;</span> <span class="na">name=</span><span class="s">&quot;subject&quot;</span><span class="nt">&gt;&lt;br&gt;</span>
		  Message: <span class="nt">&lt;textarea</span> <span class="na">name=</span><span class="s">&quot;message&quot;</span> <span class="na">cols=</span><span class="s">&quot;40&quot;</span> <span class="na">rows=</span><span class="s">&quot;5&quot;</span><span class="nt">&gt;&lt;/textarea&gt;</span>
		  <span class="nt">&lt;input</span> <span class="na">type=</span><span class="s">&quot;submit&quot;</span> <span class="na">value=</span><span class="s">&quot;Send Message&quot;</span><span class="nt">&gt;</span>
		<span class="nt">&lt;/form&gt;</span></code>
	</pre>
</p>

<h3>1.Setup the HTML form</h3>
<p>
	Change your form's <code>action</code>-attribute to this and replace your@email.com with your own email.
</p>
<pre><code>
http://formspree.io/myusername@gmail.com
</code></pre>

<h3>2. Submit the form and confirm your email address</h3>
<p>
	Go to your website and submit the form once. This will send you an email asking to confirm your email address, so that no one can start sending you spam from random websites.
</p>
<h3>3. All set, receive emails</h3>
<p>
	From now on, when someone submits that form, formspree will forward you the data as email.
</p>
<h3>We can even use AJAX</h3>
<p>
	You can use Formspree via AJAX. This even works cross-origin. The trick is to set the <code>Accept</code> header to <code>application/json</code>. If you're using jQuery this can be done like so:
</p>
<pre><code>
$.ajax({
    url: "//formspree.io/username@gmail.com", 
    method: "POST",
    data: {message: "hello!"},
    dataType: "json"
});
</code></pre>
<div class="embed-responsive embed-responsive-16by9">
	<iframe width="1280" height="720" src="https://www.youtube.com/embed/ykeZisJ64WI" frameborder="0" allowfullscreen></iframe>
</div>
