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

### Service top-level objects

-   Initialized automatically.
-   Use to access and create objects deeper in the model.
-   Typically named <code><i>Service</i>App</code>. For example, the spreadsheet
    top-level object is `SpreadsheetApp`.
    
### Primary container objects

-   Most services have an object for their fundamental data container (document,
    spreadsheet, calendar, contact, etc.).
-   Generally (but not always) shares a name root with the thop-level object.
    For example, `SpreadsheetApp` uses primary container called `Spreadsheet`.

### Active objects
One of the ways you can use Apps Script is attached to a container. For example,
you can create a script that applies to a single spreadsheet.

-   Access the instance of an app that the script is attached to by getting
    _active_ objects. For example:
    
    ```javascript
    var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
    ```
-   In some cases, you can access other objects deeper in the model in the same
    way:
    
    ```javascript
    var sheet = SpreadsheetApp.getActiveSheet();
    var range = SpreadsheetApp.getActiveRange();
    ```
    
## Spreadsheets

This is the model for the Spreadsheets application (called Sheets in the UI).

### Model hierarchy



<!--
----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8
-->
