# Installation

- [Prerequisites](#prerequisites)
- [Install Laravel Comments](#install-laravel-comments)
- [Clone Laravel Comments Demo](#clone-laravel-comments-demo)
- [Requirements and Browser Support](#requirements-and-browser-support)

## Prerequisites

This guide assumes that you already know how to [install](http://laravel.com/docs/5.4/installation) and configure Laravel and have the latest version of [Composer](https://getcomposer.org/) installed.

## Install Laravel Comments

Extract the files from the archive you have downloaded from CodeCanyon into a `laravel-comments` folder in your project root.

Edit your `composer.json` file and add a [local path](https://getcomposer.org/doc/05-repositories.md#path) repository:

```json
"repositories": [
    {
        "type": "path",
        "url": "./laravel-comments"
    }
]
```

In your terminal run:

```bash
composer require hazzard/laravel-comments *@dev
```

For 5.4 and bellow, add the service provider:

```php
// config/app.php
'providers' => [
    ...
    Hazzard\Comments\CommentsServiceProvider::class,
];
```

For 5.2 and bellow, you have to publish the migrations with:

```bash
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider" --tag=migrations
```

Run the migrate command to create the necessary tables:

```bash
php artisan migrate
```

Publish the assets files with:

```bash
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider" --tag=public
```

You can publish the config-file with:

```bash
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider" --tag=config
```

If you use Laravel 5.2 or bellow and want to enable mail notifications you must install the [Laravel Notification Channels Backport](http://laravel-notification-channels.com/backport) package.

Head over to the [Usage](usage.md) section to get started.

## Clone Laravel Comments Demo

You can clone the [demo version](https://laravel-comments.demo.hazzardweb.com) from the GitHub [repository](https://github.com/hazzardweb/laravel-comments-demo):

```bash
git clone https://github.com/hazzardweb/laravel-comments-demo.git
```

Then you can continue with the [normal installation](#install-laravel-comments).

### Requirements and Browser Support

Laravel Comments requires Laravel >= 5.1.9 and supports the following browsers (desktop and mobile): Chrome, Firefox, Opera, Safari, MS Edge and IE10+.

<style>.docs-content ol { padding-left: 20px; }</style>
