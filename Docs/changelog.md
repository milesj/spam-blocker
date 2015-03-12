# Changelog #

*These logs may be outdated or incomplete.*

## 2.1.0 ##

* Updated beforeSave() to check blacklisted words within the author, website and content

## 1.9 ##

* Updated beforeSave() to check blacklisted words within the author, website and content

## 2.0 ##

* Updated to CakePHP 2.0 (not backwards compatible with 1.3)

## 1.8 ##

* Changed from afterSave() to beforeSave() to trigger before the database is hit
* Improved documentation

## 1.7 ##

* Updated the $statusCodes to use an enum
* Added a referrer check to comment scoring
* Refactored notify() to be public

## 1.6 ##

* Renamed the class to SpamBlocker
* Improved the support for custom column names
* Refactored the notify() method
* Will now work within plugins

## 1.5 ##

* Upgraded to PHP 5 only

## 1.4 ##

* Added support for multi-byte and UTF-8 characters

## 1.3 ##

* Adding a setting for the number in which to delete a comment at (negative)
* Modified afterSave() so that the first word may not start with the blacklisted words
* Fixed a problem with the :id in article_link not working

## 1.2 ##

* Added a setup() method that loads settings automatically, settings are defined in the model
* Added a settings property that contains all variables, in turn removed all other properties
* Rebuilt the notify() method so that you don't have to edit it manually, instead you define the vars in the settings array
* Added more blacklisted keywords

## 1.0 ##

* First initial release of Commentia
