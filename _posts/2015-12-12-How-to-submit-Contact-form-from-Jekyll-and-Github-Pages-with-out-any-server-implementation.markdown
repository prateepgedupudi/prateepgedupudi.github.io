---
layout:     post
title:      "How to submit Contact form from Jekyll and Github Pages with out any server implementation"
subtitle:   "Functional HTML forms with no database"
date:       2015-12-18 15:27:00
author:     "Prateep Gedupudi"
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

<pre><code>
<form action="//formspree.io/your@email.com"
      method="POST">
    <input type="text" name="name">
    <input type="email" name="_replyto">
    <input type="submit" value="Send">
</form>
</code></pre>

<h3>1.Setup the HTML form</h3>
<p>
	Change your form's <blockquote>action</blockquote>-attribute to this and replace your@email.com with your own email.
</p>
<blockquote>http://formspree.io/myusername@gmail.com</blockquote>
<h3>2. Submit the form and confirm your email addres</h3>
<p>
	Go to your website and submit the form once. This will send you an email asking to confirm your email address, so that no one can start sending you spam from random websites.
</p>
<h3>3. All set, receive emails</h3>
<p>
	From now on, when someone submits that form, we'll forward you the data as email.
</p>
<h3>We can even use AJAX</h3>
<p>
	You can use Formspree via AJAX. This even works cross-origin. The trick is to set the <blockquote>Accept</blockquote> header to <blockquote>application/json</blockquote>. If you're using jQuery this can be done like so:
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
	
</div>
