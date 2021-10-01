# Installation

- [Prerequisites](#prerequisites)
- [Install Laravel Comments](#install-laravel-comments)
- [Clone Laravel Comments Demo](#clone-laravel-comments-demo)
- [Requirements and Browser Support](#requirements-and-browser-support)

## Prerequisites

This guide assumes that you already know how to [install](https://laravel.com/docs/8.x/installation) and configure Laravel and have the latest version of [Composer](https://getcomposer.org/) installed.

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

Additionally you may want to clear the config, cache, etc:

```bash
php artisan config:clear
php artisan route:clear
php artisan cache:clear
php artisan view:clear
```

Head over to the [Usage](usage.md) section to get started.

## Clone Laravel Comments Demo

You can clone the [demo version](https://laravel-comments.demo.hazzardweb.com) from the GitHub [repository](https://github.com/hazzardweb/laravel-comments-demo):

```bash
git clone https://github.com/hazzardweb/laravel-comments-demo.git
```

Then you can continue with the [normal installation](#install-laravel-comments).

### Requirements and Browser Support

- Laravel: 6, 7, 8
- PHP: 7.2, 7.3, 7.4, 8.0
- Browsers: Chrome, Firefox, Opera, Safari, Edge

<style>.docs-content ol { padding-left: 20px; }</style>
