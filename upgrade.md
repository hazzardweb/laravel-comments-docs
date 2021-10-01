# Upgrade Guide

- [Git](#git)
- [Upgrading To 4.0 From 3.x](#upgrading-to-40-from-3x)

## Git

You can view the all the changes on [git.hazzardweb.com](https://git.hazzardweb.com) by logging in with your Envato account.

## Upgrading To 4.0 From 3.x

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
