---
title: Build a Cookie Scanning Extension
slug: CookieScanning
tags: Extend Fiddler, .NET, Extension, Cookies, IAutoTamper2, Privacy, P3P
publish: true
ordinal: 10
---

Build a Cookie Scanning Extension
=================================

1. Install the [Privacy Scanner Fiddler add-on][1].

 Fiddler will gain a new top-level menu named **Privacy**.

 ![Privacy menu][2]

2. Ensure **Privacy > Enabled** is checked.

 The add-on will add a **Privacy Info** column to the session list and will flag HTTP/HTTPS responses which set cookies. Evaluation of any P3P statements that come along with those cookies will change the session's background color.

 ![Privacy Info Column][3]

 

[1]: http://fiddler2.com/add-ons
[2]: ../../images/CookieScanning/PrivacyMenu.png
[3]: ../../images/CookieScanning/PrivacyInfo.png