#Know to Do - Jekyll Version

###[View Live Demo &rarr;](https://prateepgedupudi.github.io)

## Before You Begin

In the _config.yml file, the base URL is set to /prateep.info which is this themes gh-pages preview. It's recommended that you remove the base URL before working with this theme locally!

It should look like this:
`baseurl: ""`

## What's Included

A full Jekyll environment is included with this theme. If you have Jekyll installed, simply run `jekyll serve` in your command line and preview the build in your browser. You can use `jekyll serve --watch` to watch for changes in the source files as well.

A Grunt environment is also included. There are a number of tasks it performs like minification of the JavaScript, compiling of the LESS files, adding banners to keep the Apache 2.0 license intact, and watching for changes. Run the grunt default task by entering `grunt` into your command line which will build the files. You can use `grunt watch` if you are working on the JavaScript or the LESS.

You can run `jekyll serve --watch` and `grunt watch` at the same time to watch for changes and then build them all at once.

## Adding FormSpree.io to Contact form
Change the `email` under `js/prateep-blog.js` while submiting post data with 
`ajax` 
> url: "//formspree.io/prateep.gedupudi@gmail.com"

More on FormSpree.io can be found on link
[https://prateepgedupudi.github.io/2015/12/18/Set-up-a-contact-form-with-FormSpree-io-with-out-any-server-database-impl/](https://prateepgedupudi.github.io/2015/12/18/Set-up-a-contact-form-with-FormSpree-io-with-out-any-server-database-impl/)