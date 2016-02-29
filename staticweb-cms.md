---
title: Static Web Sites vs CMS
author: Jake Bourne
publishDate: 2016-02-01
layout: post.jade
category: techiestuff
slug: staticwebsites-cms
favimg: static-site.png
---
### History
Static web sites have been around since the start of the World Wide Web in the early 1990s. They are simply a collection of text files marked up as HTML and served by a web server when a request is received from a web browser.  All you need to edit them is the standard text editor which comes pre-installed with your operating system. Notepad on Windows, vi on Unix, TextEdit on iOS.  Javascript can also be added to the text files to add some fancy animations and dynamic styling to the web page.

### Manual HTML editing
As web sites became bigger, writing HTML became very tiresome especially for content writers with little technical expertise. To format different parts of text, opening and closing tags need to be placed around the text. When compared to highlighting the text and clicking a Bold or Italics button, it's not hard to tell which is the more user-friendly option!  When creating new content, existing web pages had to be copied to include the same banner, menus and sidebars for the sake of each new article. Add a new menu item or logo meant that every page had to be updated!

### Rise of the CMS
These issues were solved by the introduction of databases to web development. Content could be written in an HTML form, submitted to a script on the web server which would save the content to a database. Storing all the content in a database now gave web designers to re-use a single page layout to fill it with different content. Each time a new page is requested, the web server reads a layout template, then builds the content and styling before sending it back to the user. As the concept of database-backed web sites matured, mini-user interfaces were created to wrap around textareas to allow the text to be formatted as in a word processor.  Eventually, the Content Management System (CMS) was born which allowed content writers to develop their own web sites.  The technical knowledge required to publish an article online was suddenly reduced. The CMS became so advanced and transparent that it was not easy for the content writer to visualise the boundary between an article being saved locally to their hard disk and being published online.  A common call to technical support was why hadn't their article been saved after their network connection was lost.

### Disadvantages of Databases
Databases may have been the saviour for content producers and writers, but they were not designed to handle large amounts of textual data. Their main use was for accounting systems, stock control or people records. The largest data types for text data ranges between 4000 to 8000 characters. When big articles are recalled from a database, a minimum of 8Kb may need to be downloaded. A typical home page often contains the excerpts from several blog posts which caused all these records to be searched and sent back across the Internet. Think of the load on the single database when the web site attracts 100+ users!

### Do you really need a database?
Of course, solutions such as database mirroring, load balancers, CPU and memory upgrades are used to assist with high load on servers and databases, but should we really be using databases for storing large amounts of content? Databases add an extra security vulnerability which is a gold mine for hackers. A poorly developed web site can give a hacker access to your entire database. In the age of information, this is invaluable. If your information is not itself valuable, the hacker can still use your database resources for their own malicious purposes.

### How regularly does your site content get updated?
The majority of web site's do not update their *own* and *original* content more than once per day.  Only truly frequently-updated real-time content such as news, financial information, weather and forums necessitate the overhead of a database. The only dynamic portion of a basic blog is the commenting system, and this can now be provided by third party applications such as (Facebook)[www.facebook.com] or [Disqus](https://disqus.com/).

### Keeping track of updates to your content?
Although possible, it is notoriously difficult to track and control updates to a blog post when stored in a database. Each time you make a change to a blog post, it will overwrite the same database record. To implement different versions of content in a database, you need to create a new post, link it to the original post and then publish it in place of the original post. Reverting to a previous version of a blog post will involve loading all previous versions, selecting which one to re-publish in place of the latest version. Two round-trips to the database are required to achieve this!

### How can Static Web Sites be more like CMS-backed Sites?
Different web technologies have now come together to create Static Site Generators which allow content to be written easily and then merged with layout templates to generate the HTML files. The entire web site is built offline and then uploaded to a web server.  Since all pages are pre-built, the web server only needs to pass the requested page back to the web browser. Database connectivity timeouts and security holes are immediately eliminated!  Since all source files remain on your own computer, they can be copied to backup drives and stored in a version-controlled repository such as Git or SVN.  Repositories allow all changes to be recorded and tracked.  Multiple content writers can update content and their work can be merged before it is published.

### Disadvantages of Static Site Generators.
The only real sacrifice in a static web site is real-time updates, user interactivity through commenting and processing your own submitted form data. The latter two can still be provided by third party applications such as [Wufoo](http://www.wufoo.com) and [Disqus](https://www.disqus.com), although both rely on using cross-site Javascript which can affect your SEO rating.

### How many Static Site Generators are out there?
There are loads! The most popular is the Ruby-based Jekyll which gives you the framework for a responsive blog for free. Static site generators tend to make use of the modern-style of Rapid Application Development (RAD) languages such as Ruby, NodeJS and Python. They can obviously be written in any programming language.

Each site generator makes use of its own templating engine, CSS preprocessor, Coffeescript compiler and markup language. Although these can be changed to suit your own preference. Here is a list of a few of the most common site generators along with their base language and default templating engine:-

Generator | Base Language | Template Engine
--- | --- | ---
Jekyll | Ruby | Liquid
Middleman | Ruby | ERB
Octopress | Ruby  | Liquid
Metalsmith | NodeJS | Jade
Wintersmith | NodeJS | Jade
Roots | NodeJS | Jade
Hugo | Go | Go
Pelican | Python | Jinja
Cactus | Python | Django


### What are the Components of a Static Site Generator?
The template engine is essentially what gives the site generator its power. It allows content to be re-used, formatted differently, conditionally executed on pre-defined criteria and modularised to save repetition. They certainly save you the laborious task of editing HTML tags!

Markup languages make editing the actual content much less tedious. The requirement of HTML to enclose content within tags can break the flow of a writer's thoughts. Using a markup language like _*Markdown*_ or _*Textile*_ allows text to be formatted using just a few characters.

The following examples show you a brief view of how Markdown is used to format content:-

**Bold text**        ``` **Bold text** ```

*This text is in italics*   ``` *This text is in italics* ```

This is a link to [Google](http://www.google.com)    ``` [Google](http://www.google.com) ```

This will load an image     ``` ![My Logo](/images/logo.png) ```

To create an HTML page, the markup is processed to convert into HTML and then merged into a template.

An important thing to remember is that all the processing is done off-line so will have no effect on response times. The web server simply responds to user requests by sending back the pre-built page.


### Conclusion
The choice to go for a static web site or a CMS-backed web site with a database really depends on your individual needs. Consider the following:-

  - Does your web site have any content which needs to update in real-time? Note that this doesn't include content you manifest from third party sources such as weather forecast or share prices.

  - Does your content really need to be stored in a database and updated with a CMS? A CMS makes content writing relatively simple so less technical ability and knowledge is required at this level.

  - Does your web site have a login page to authenticate and store user details? There are methods to provide this for a static site, but if the application is very user-centric, then a dynamic site with a database would be necessary.

  - If the majority of your site contains static content with only a few areas which require a database, then you may still be able to opt for the best of both worlds. Have a look for third-party providers for these areas or develop them yourself. At least the hits on the database will be restricted to the areas which require it, whilst the static content can still be served fast. Restricting the security vulnerability to a much smaller area also makes it easier to control and reduce the overall risk.
