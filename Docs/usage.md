# SpamBlocker #

*Documentation may be outdated or incomplete as some URLs may no longer exist.*

*Warning! This codebase is deprecated and will no longer receive support; excluding critical issues.*

Spam Blocker is a CakePHP Behavior that automatically before after a comment is made. Each comment is tested upon a point system to determine and classify it. If a comment has more then 1 point it is automatically approved, if it has 0 points it continues pending, and if it is in the negative point range, it is either marked as spam or deleted entirely. The Behavior is extremely easy to install and requires no moderation from you (maybe a little!).

The point system is based on an idea by Jonathon Snook and his article "[How I built an effective blog comment spam blocker](http://snook.ca/archives/other/effective_blog_comment_spam_blocker/)". I merely took his points and outlines and built the behavior from the ground up.

* Easy installation and configuration
* Just add it to your Comment models $actsAs
* Automatically runs after a comment is made
* Gives each comment a point ranking and then moderates
* Sends an email notification after every comment
* Always updated to ensure the best anti-spam capabilities!

## Installation ##

First off, you need to download the script and place the behavior in your `app/Model/Behavior` folder of your installation. To enable the behavior, add it to your `$actsAs` variable on the `Comment` Model.

```php
class Comment extends AppModel {
    public $actsAs = array('SpamBlocker');
}
```

Below is the comments table structure that the behavior is based around. Again, if your table does not look like this, there is some configuration you can do to get it working (which you can check in the next step). The points column isn't necessary, it is only there for reference and fun. If you do not want the points column, you can disable it from updating in the database.

```sql
CREATE TABLE `comments` (
    `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `entry_id` INT NOT NULL,
    `status` SMALLINT NOT NULL DEFAULT 0,
    `points` INT NOT NULL,
    `name` VARCHAR(50) NOT NULL,
    `email` VARCHAR(50) NOT NULL,
    `website` VARCHAR(50) NOT NULL,
    `content` TEXT NOT NULL,
    `created` DATETIME NULL DEFAULT NULL,
    `modified` DATETIME NULL DEFAULT NULL,
    INDEX (`entry_id`)
) ENGINE = InnoDB CHARACTER SET utf8 COLLATE utf8_general_ci;
```

## Configuration ##

When you install the behavior by attaching it to `$actsAs`, you can supply an array of settings. These settings will be loaded automatically when the behavior is called, so no need for manually editing the core file. The following variables are use able in the settings array:

* `parent_model` - The name of the model that comments belong to. By default its Entry, but yours might be Article, News, Blog, etc.
* `article_link` - The full url address for the article the comments belong to. For example, my url would be `milesj.me/blog/read/:id`. The string :id in your url will be replaced with the dynamic id for the corresponding article. You can also use :slug for slug based URLs.
* `notify_email` - The destination email, for the notification email when a comment is made.
* `save_points` - Saves points score for each comment to the database.
* `send_email` - Toggles on/off the notification email.
* `deletion` - The points number in which to delete a comment at (deletion number should be negative). So if you want your spam to be deleted when its points reach -5, just set deletion to -5.

If you are getting a lot of spam and the default blacklisted words aren't working, you can add your own to the `blacklist_keys` and `blacklist_chars` settings. These must be an array of words to work correctly.

```php
public $actsAs = array(
    'SpamBlocker' => array(
        'settings' => array(
            'parent_model'    => 'Article',
            'article_link'    => 'http://milesj.me/blog/read/:id',
            'notify_email'    => 'testemail@milesj.me',
            'deletion'    => -5
        )
    )
);
```

## Custom Column Names ##

If you already have an existing comments table with different column names, you have the option of defining column name overrides. To do this, pass an array of column names to overwrite the defaults, using `columns`. The following overrides are supported:

For comments:

* `author` - The authors name
* `email` - The authors email
* `website` - The authors website
* `content` - The comment body
* `status` - The comments status (approved, denied)
* `points` - The points scored

For articles:

* `foreign_id` - The foreign key ID that comments relate to
* `slug` - The URL slug
* `title` - The title

```php
public $actsAs = array(
    'SpamBlocker' => array(
        'columns' => array(
            'author' => 'username',
            'content' => 'comment',
            'foreign_key' => 'article_id'
        )
    )
);
```

## Custom Status Codes ##

Just like columns, you can override all the possible comment statuses. By default, the following statuses are supported and their respective level: pending (0), approved (1), delete (2), spam (3). If you want to change this, say to strings, you can do so by passing an array to `statusCodes`. Just make sure your comments table supports it.

```php
public $actsAs = array(
    'SpamBlocker' => array(
        'statusCodes' => array(
            'pending' => 'pending',
            'approved' => 'approved',
            'delete' => 'denied',
            'spam' => 'garbage'
        )
    )
);
```
