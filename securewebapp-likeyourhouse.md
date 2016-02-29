---
title: Secure Your Web Site Like Your House
author: Jake Bourne
publishDate: 2016-02-23
layout: post.jade
category: techiestuff
slug: secure-your-website-like-your-house
---
Securing a web application is like locking up your house. Would you leave your doors unlocked when you are not at home? Just as houses are located in public streets, web applications are in cyber space which can be accessed all over the world. Even houses in postcode areas with the highest crime rates will have less risk of instrusion than a web application. A web application must be built to withstand the attempts of hackers from all over the world, trying an ever-growing list of techniques to gain access to it.
<!--more-->

An easy way to view web application security is by picturing your own house. It has a front door, a back door, windows, a number of rooms, a roof, boundary fences and different access routes. Only the terminology is different.

### The Front Door.
The front door of any web application is the login page and, not surprisingly, it is the primary point of attack. A login page will consist of edit boxes to type a user name and password and a button to send these for the server to authenticate your access to the rest of the web application. Some login pages may provide a captcha to make sure you are a human being and not a mock-up of the same form on a different server. The mock-up form will cycle through variations of user names and passwords until it gains access to the application. This is known as cross-site forgery and is akin to a burglar forging the keys to your house.

Captchas are jumbled images of scrambled letters and numbers which make it impossible for an automated script to read. Unfortunately, as the scripts become cleverer at reading these images, the captcha images need to become more complex and harder for humans to read. This causes frustration for the end-user as they have repeated failed attempts at gaining access to their account because the captcha was unreadable. The solution to this has been to replace the captcha with a secure token. The secure token is generated my joining the user name, password and any other user information available with a uniquely generated key. This concatenation is then encrypted and stored as a hidden field in the form, thus making it impossible for any mock-up form to make a successful login attempt.

### The Windows and Back Door.
What are the windows of a web application? I don't mean the operating system on the server. I'm talking about potential areas of each page which could be broken to make a forced entry. These areas are edit boxes and text areas which allow a user to type information. An attacker will use edit boxes and text areas to enter commands which the database understands. If the software is not written securely then it is very easy to interrupt the database when it is saving the data, so that it will execute the commands supplied by the attacker. Typical attacks could result in the database being destroyed, data being stolen or user information being compromised. This type of attack is known as SQL injection.

### Boundary Fences.
The boundary fences of a web page are any links, editable areas and the main URL address. The URL of the page itself and links embedded in the page can be copied and modified from another site so that commands can be executed by the server. Javascript code can be inserted into editable areas to force data to be submitted to a rogue site or to gain control of the user's web browser. Database commands can also be inserted into the main URL address. These attacks are known as cross-site scripting (XSS) attacks because they are scripts which direct the user to an attacker's own web site. XSS attacks could be used to steal a user's authenticated session identifier and use it to increase the level of access of another account they have already created.

To prevent cross-site scripting, the software must scan all editable areas for code and also include a secure token in each URL and link. Just as holes and gaps in fences should be closed. All secure pages should check for the existence of an authenticated user.

### Impersonation.
We have all experienced bogus house callers who claim to be the gas man or the water company saying they need to gain access to your house to turn off your supply. Web site attackers may contact you or any other users of your site by email, social network or telephone and trick you into revealing your login details. Reasons they may give could be that your web site has already been hacked and they can fix it if you provide them with access. The only prevention is to constantly remind your users that they should not reveal their username and password to anyone and that you as the site owner will never ask them to reveal their password. You should provide links to allow your users to reset forgotten passwords by sending them an email link with an encrypted token to guarantee its source.

### Brute force entry.
The simplest and quickest method of entry for any burglar to break into a house is to use a crowbar to prise open a door, or smash a window with a brick.
The hi-tech version of this method is the Denial of Service attack (DoS). A DoS attack involves repeatedly targeting a web page until the web server runs out of memory and shuts itself down.

As the number of burglars diminish, the number of hackers is increasing. A burglar may have only been after financial gain, where as a hacker's motivation could be political, financial or just malicious damage. A house without any protection may never get burgled, but it is a certainty that an unsecure web site will eventually be attacked.
