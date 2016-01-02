---
layout:     post
title:      "Dojo 1.7 DataGrid Paging With Java Servlet "
subtitle:   "Grids are familiar in the client/server development world"
date:       2015-10-29 17:01:00
author:     prateep_gedupudi
header-img: "img/post-bg-dojo-datagrid.jpg"
---

<p>One of the more powerful features of the Dojo DataGrid is on-demand paging in response to scrolling. This provides a seamless, intuitive experience for the user viewing large data sets—as they simply scroll to see more data, rather than having to futz with paging controls. This on-demand paging is achieved by sending count limited queries to the store; the grid will call the query() method with a second parameter that is an object, with start and count properties. The JsonRest store communicates this count limit with the HTTP Range header. This is an important feature for scalability since it allows us to defer loading of out-of-view rows rather than loading an entire table or query result of data. The first request to our server should look like (it can be helpful to look at the requests in your debugger).</p>

<p> It's a given that you can use the grid to display relatively small data sets effectively in the browser and get the niceties of sorting, column resizing, etc. that come along with it. That's cool and all, but there's a practical limit to the number of records you can deal with at any given time, which eventually leads to the concept of paginating results.
Well, go ahead and forget about pagination; those days are finally over. Dojo's grid works by lazy loading data as the grid scrolls. For a relatively small data set consisting of hundreds of records, lazy loading amounts to building out the DOM for a pre-loaded data set when you scroll. For example, if you had 100 records but could only view 20 of them at a time, you wouldn't want to build the nodes for any of the records in 21 through 100 until you scrolled to that particular section. Sorting by a column and related tasks work in memory as expected for small data sets since you can effectively get things done in JavaScript.</p>

<p>For very large data sets, however, it quickly becomes impractical or even impossible to use JavaScript for tasks such as sorting by a column; if the data set is gargantuan, it's not even practical to try and maintain it in the browser through something like an ItemFileReadStore. Dojo's approach to the problem of dealing with large data sets is simple, elegant and boils down to two things: a dojo.data implementation (we'll use QueryReadStore) that can request data from the server in arbitrary page sizes, and a grid that is capable of scrolling such that it requests and loads a particular page on demand. Now, let's see it in action.</p>
Links for Test and Code: 
<a href="http://dojo-prateepgedupudi.rhcloud.com/prateepdatagrid/">http://dojo-prateepgedupudi.rhcloud.com/prateepdatagrid/</a>
<a href="https://github.com/prateepgedupudi/prateepdatagrid">https://github.com/prateepgedupudi/prateepdatagrid</a>  

<div class="embed-responsive embed-responsive-16by9">
	<iframe width="1280" height="720" src="https://www.youtube.com/embed/ULxHEedvmZ0" frameborder="0" allowfullscreen></iframe>
</div>
