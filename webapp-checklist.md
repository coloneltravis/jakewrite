---
title: Checklist for Web Applications.
layout: post.jade
author: Jake Bourne
publishDate: 2016-01-28
category: techiestuff
slug: web-app-checklist
favimg: web-checklist.png
---
Web applications are complex entities which  involve many different kinds of technologies working together to deliver a good user experience. Just changing one thing can have a knock-on effect on something else which will cause the user a nasty error page which is meaningless to them.  Hopefully, in most cases,  this error page would at least be replaced by a simple message stating that “something has gone wrong”.  That is at least accurate, if not helpful!

As a developer myself, I am fully aware that it is all too easy to miss something before concluding that a bug is fixed. To help prevent, or at least reduce some regression errors from occurring, I have put together this checklist which can be used to run through as a final sanity check before releasing the change to the live environment.


### Different Web Browsers.
Today there are many different web browsers which are used to view web pages.  Each one interprets the HTML in mostly the same way, but there are subtle differences.  The HTML standard has evolved in parallel to the web browsers, making it a challenging task for the browser developer companies to keep up.  This has lead to some browsers not supporting all features.  It is important for a web developer to keep track of the most used browsers and know which versions are used by their end users.  The most common browsers today are Chrome, Internet Explorer versions 9 to 11, Firefox, Safari and Opera.  It is a safe bet to support at least the first three of these to guarantee the robustness of the web site.


### Different User Types.
A web application may be used in different ways by separate groups of people.  For example, for an eCommerce web site like Amazon, most users are visiting the site to browse for products. There are also sellers who have access to manage their own products. There will also be several groups of users within Amazon's own staff such as warehouse operatives, statistics analysts, site administrators and system administrators.  Each type of user will have access to different areas of the software so it is important to check features by logging in as each type of user.


### Form Validation.
This is the process of checking that a form has been completed with the minimum required set of fields as well as checking that all completed fields have valid data entered into them.  

Examples of invalid data include incorrectly formatted dates,  letters or symbols in number-only fields, too much text entered into a field.

Mandatory fields should be clearly marked, usually with a red asterisk.

If a field is invalid then it should be highlighted in a suitable colour so the user can easily locate it and correct it.


### Page Navigation.
Every page should have suitable links or buttons so that the user does not feel lost. They should be able to know how to get to the next page, return to the last page they viewed and go back to the main home page.
Page navigation can either be done by adding Home, Previous and Next buttons, or my implementing a breadcrumb trail.

A breadcrumb trail is a sequence of links to pages which lead from the home page to the currently viewed page.


### Database Operations.
A web application with a backend database will have different permissions to view, add, modify and delete data. This is sometimes referred to as CRUD (Create,Read,Update,Delete). These operations will be linked to specific user types.

The majority of users will have minimal access to view site content, usually the general public. The next level will be junior staff who can update some of the site content. Then more senior staff will be able to add fresh content and remove old content.

All these operations should be checked to make sure database permissions have been configured correctly. Check that data from a database is loaded without errors, make sure it can be modified and saved back to the database. Then try adding fresh content and deleting it. Different levels of access may be required to test all four operations.


### User Maintenance Features.
If a web application has the ability for users to register and login then there should be a page where user accounts can be maintained. Passwords will need to be resets, email addresses updated as well as other personal details.

Some applications may allow a user to update their own details, in which case this should be done securely since sensitive data will be updated external to the firewall.  This is less of a concern if user maintenance is done my site administrators, although it is still a good habit to implement good security in case the system is breached.


### Security Aspects.
If your web application is being deployed on the Internet then it is crucial to perform a few basic checks to make sure that hackers cannot hijack your application and exploit it for their own endeavours. Penetration testers will perform more detailed checks, but it is worth doing the following checks for your own peace of mind.

Hackers will look to exploit any point of entry in your application which include forms, text areas, URLs and any unhandled errors.


- SQL injection.

  This is the process of attempting to modify a database query by appending malicious text in text boxes or the URL address bar.  The usual technique is to add a single quote character before and SQL 'logical AND' condition which will force the database to return more data rows.

  On a login page, this technique could be used in the **username** or **password** boxes to override the login check and gain access to the application, potentially making all secure pages accessible to the hacker.

  For example, if the text *```'' OR 1=1```* is inserted into a password field, the login check query could be modified like this:-

  ```
      select username, password from tblUsers
      where username = 'user123' and password='' OR 1=1
  ```

- Cross-site scripting (XSS).

  This is the process where Javascript code can be pasted within a ```<script>``` tag into text boxes and text areas. The web browser could then be redirected to run code from another site.

  Also, if the Javascript code is saved to a database field, it could be reloaded when the field is accessed by another user. A typical security breach could involve sending a user's session data and cookies across the Internet to the hacker.

  A simple check can be made by inserting the following Javascript into all text controls that save data to the database.

  ```
    <script text="javascript">alert();</script>
  ```

  Then navigate to a page which reloads this data. If an alert box pops us, you have discovered an XSS vulnerability.

  Luckily, XSS attacks can be prevented by either removing ```<script>``` tags from and text control or, if HTML is allowed, then it could be escaped to prevent it from being executed.


- Cross-site forgery.

  Login forms are naturally built to be extremely secure since they are the front door to an entire web site. However, this does not necessarily stop hackers from mimicking the login request sent to the server.

  How does the server recognise that a request has come from the correct web application? Anyone can view the HTML source to determine the form fields sent to the server. A hacker could therefore generate login requests to attempt access using sequentially-generated login credentials.

  The solution to cross-site forgery is to include a token as a form field which is encrypted using a secret key on the server. When the form is submitted, the token will be checked to guarantee that the request is genuine and authentic.


### Overall Performance.
As you use the web application, do you notice that some actions appear to be taking too long to complete?

Are there lots of timeout errors being produced by the server?

There may be a database query which is returning too much or unnecessary data. Some code could be included in a loop where it should only be executed once.  Perhaps there is a problem with the server configuration?

Of course, the development environment may need a memory or processor upgrade to reduce sluggishness, but it is always good to eliminate the software first. If the environment is naturally sluggish for other applications, use this as the benchmark to assess whether the source code can be improved.


### No Javascript Functionality.
These days Javascript is switched on for the majority of users. Some web applications may even disable the
login screen if Javascript is not enabled.  However, if a web site needs to be accessible to people with visual impairments then it will need to provide some kind of Functionality without Javascript.

Screen readers parse a web page to read out the text to the user. Links and buttons will need to be activated via the 'tab' key or invoked by a 'hot key' sequence.  Any Javascript in the page will be ignored and could hinder or confuse the user's understanding of the page.

Turn off Javascript in your web browser and see how each page is displayed. Are all controls accessible without using the mouse?


### User Accessibility.
Any web application should be accessible to as many people as possible. Some may only be targeted at technical users who don't require much guidance or instruction, whereas others will need to be designed to be used by less computer-literate or people with learning disabilities.

It is best to design an application to be accessible to the least computer-literate, or at least allow features to be customised by the user.


Here are some guidelines to make sure your application is accessible:-

  - Be able to control overall text size.
  - Clear contrast between background/foreground colours. Black on white or vice versa is the ideal.
  - Links and buttons should have keyboard shortcuts.
  - Clear images with alternate text specified for screen readers.
  - Suitable line spacing to match font size and avoid cluttered paragraphs.
  - Form labels matching with fields.
  - Clear navigation links - Home and Back buttons, pagination, breadcrumb trails.
  - A good consistent heading structure.
  - Avoid sole use of colours to highlight information. Colour-blindness is very common.


### Different Devices or Screen Sizes.
Nowadays, people don't just use a computer to view web pages. Your web site could be viewed on phones, tablets, large TV screens or even watches.

Some web sites may be designed for mobile-first, others may be designed for the most common 800x600 or 1024x768 resolutions. Web browsers on smaller devices will often zoom out to show all content on a page so it is up to the user to pinch/zoom to the content they desire.

A truly responsive application should collapse large areas to display vertically, resize fonts or images appropriately, increase size of buttons for fat fingers or omit areas to reduce clutter on a smaller screen.

Some pages may provide the option to print on a printer or download as a PDF. Menus, navigation links and banners are redundant for printers so these areas should be excluded. Image and font size may need to be adjusted to show clearly on an A4 page as opposed to the screen.


### Different Languages.
If the language of the application can be changed to suit users from different countries, then it is a good idea to scan through the content in each language. Non-English languages use character sets which may contain accented characters.

The web page will need to recognise the character set to avoid garbage characters being displayed. If the content is returned from a database, then the database column will also need to be configured to recognise the character set.


### Does it work from fresh?
Remove all data and users and start using the application from fresh.

As an application is developed, configuration data can be pre-populated manually so it is assumed that it is always available. Then the software is installed in the production environment and it fails because the data cannot be found.


### Site-wide Error Handlers.
It is impossible to locate all bugs in any software application, but when a bug is found by a user, you do not want the server to show them an error dump which may reveal source code or clues to the server infrastructure. This information would be invaluable to a hacker intent on devising a method to break your server.

The protection for this is to create a page to be invoked whenever an error is encountered. A general server error in an existing page is assigned a status code of 500.  If a page cannot be located on the server, a status code of 404 is assigned.

A page to handle each status code should be created so that the user will see an informative screen saying that "something has gone wrong" or "the page could not be found". The page will then email the error diagnostics to the system administrators or developers so that the bug can be logged and resolved.


### Consistent Look and Feel?
Navigate through the pages of your web application and look for any irregularities in how each page is display.

Content text should be in the same font and alignment throughout the site. Likewise, all buttons and links should be styled in the same way, unless there is an obvious reason to deviate. Each page should have the correct navigation links and appropriate breadcrumb trail. Make sure that the banner, sidebars and footer are included on each applicable page.

If a single page is different from the rest, then it will look odd and stand out to the end user. They may also become stuck a page if there are no links to 'break' out of the loop.



If you run through these checks before you deploy your application, the extra time spent will reduce the number of bugs coming your way to resolve and gain you huge respect  in the testing team!
