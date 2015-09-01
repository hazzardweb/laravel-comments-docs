# Installation

- [Prerequisites](#prerequisites)
- [Install Ajax Comment System](#install-ajax-comment-system)
- [Clone Ajax Comment System Demo](#clone-ajax-comment-system-demo)
- [Requirements and Browser Support](#requirements-and-browser-support)

## Prerequisites

This guide assumes that you already know how to [install](http://laravel.com/docs/5.1/installation) and configure Laravel.

## Install Ajax Comment System

1. In your `app` directory, create a `comments` folder and extract all the files from the archive you have downloaded from CodeCanyon.
2. Edit your `composer.json` file and add the following line to the `psr-4` autoload:
```php
"Hazzard\\Comments\\": "app/comments/src/"
```
And this one to your dependencies (`require`): 
```php
"s9e/text-formatter": "^0.2.1"
```
In your terminal/console run `composer install`.
3. Add `'Hazzard\Comments\CommentsServiceProvider'` to your `providers` array in `config/app.php` and run:
```php
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider"
```
This command will publish the configuration file (config/comments.php), the assets folder (public/vendor/comments) and the database migrations __*__.<br>
> Notice: The script assumes that you have already have the users table installed.
5. Finally, run: 
```php
php artisan migrate
```
6. Head over to the [Usage](usage.md) section to get started. 

<br> 
__*__ The migrations will add 3 tables `comments`, `comment_votes`, `comment_options` and a `role` field to your users table. This field will be used to determine if the the authenticated user is an admin or a regular user. <br>

> Notice: If your app already has another method to determine that, then delete the `..._add_users_role_column.php` migration from the database/migrations directory.

## Clone Ajax Comment System Demo

You can clone the [demo version](http://acs-laravel.demo.hazzardweb.com) from the GitHub [repository](https://github.com/hazzardweb/ajax-comment-system-laravel-demo). Run:

```bash
git clone https://github.com/hazzardweb/ajax-comment-system-laravel-demo.git
```

Now you can continue with the [normal installation](#install-ajax-comment-system). This demo requires you to have reCAPTCHA [configured](configuration.md#recaptcha).

### Requirements and Browser Support

Laravel Comments requires Laravel 5.1.9 and supports the following browsers (desktop and mobile): Chrome, Firefox, Opera, Safari MS Edge and IE9+.

<style>.docs-content ol { padding-left: 20px; }</style>
