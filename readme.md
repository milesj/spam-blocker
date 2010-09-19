# Spam Blocker v1.6 #

A CakePHP Behavior that moderates and validates comments to check for spam.

----------

Version 1.6 is not backwards compatible with previous versions.
Check the commit log for changes and please update your code accordingly!

## Requirements ##

* CakePHP 1.2.x, 1.3.x
* PHP 5.2.x, 5.3.x
* "comments" Database Table

## Features ##

* Easy installation and configuration
* Just add it to your Comment models $actsAs
* Automatically runs after a comment is made
* Gives each comment a point ranking and then moderates (approves, deletes, marks as spam)
* Sends an email notification after every comment
* Always updated to ensure the best anti-spam capabilities!

## Documentation ##

Thorough documentation can be found here: http://milesj.me/resources/script/spam-blocker-behavior
