# Upgrade Guide

- [Git](#git)
- [Upgrading To 3.0 From 2.x](#upgrading-to-30-from-2x)

## Git

You can view the all the changes on [git.hazzardweb.com](https://git.hazzardweb.com) by logging in with your Envato account.

## Upgrading To 3.0 From 2.x

Replace `laravel-comments` and run: 

```bash
composer update hazzard/laravel-comments

php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider" --tag=public --force
```

Additionally you may want to clear the config, cache, etc:

```bash
php artisan config:clear
php artisan route:clear
php artisan cache:clear
php artisan view:clear
```
