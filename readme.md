# Spam Blocker v1.9 #

A CakePHP Behavior that moderates and validates comments to check for spam. Invalid comments will not be inserted into the database.

This version is only compatible with CakePHP 1.3.

## Compatibility ##

* v1.x - CakePHP 1.3
* v2.x - CakePHP 2.0

## Requirements ##

* PHP 5.2, 5.3
* "comments" database table

## Features ##

* Easy installation and configuration
* Just add it to your Comment models $actsAs
* Automatically runs before a comment is made
* Gives each comment a point ranking and then moderates (approves, deletes, marks as spam)
* Sends an email notification after every comment
* Always updated to ensure the best anti-spam capabilities!

## Documentation ##

Thorough documentation can be found here: http://milesj.me/code/cakephp/spam-blocker
