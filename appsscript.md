# Google Apps Script cheat sheet

These are some notes about using Google Apps Script to work with Google Apps. My
knowledge is only just starting, but the official docs are pretty lacking in
overview and context, so every little bit helps.

## Apps script environment

When you write a script you are essentially using Google's own implementation of
Javascript with all of the Google app libraries included by default. There is no
need to include anything.

The objects available for public use are documented in the
[Apps Script reference docs](https://developers.google.com/apps-script/reference/calendar/).
In addition to G Suite app object models, you'll find general and advanced
services.

## Service basics

All of the Google services are in the cloud, so they're always available if you
are connected to the Internet. There's no need to initialize or otherwise "spin
up" a service.

Services have top-level objects that you can use to access and create objects
deeper in the model. These are typically named `_Service_App`.
<!--
----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8
-->
