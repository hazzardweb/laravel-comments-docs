# Installation

<hr>

1. In your `app` directory, create a `comments` folder and extract all the files from the archive you have downloaded from CodeCanyon.
2. Edit your `composer.json` file and add the following line to the `psr-4` autoload:
```php
"Hazzard\\Comments\\": "app/comments/src/"
```
If you plan using the BBCode or Markdown parsers then add these packages (in the `require` section): 
```php
"jbbcode/jbbcode": "^1.3",
"erusev/parsedown": "^1.5"
```
and run `composer update`.
3. Add `'Hazzard\Comments\CommentsServiceProvider'` to your `providers` array in `config/app.php`.
4. In your terminal/console run: 
```php
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider"
```
This command will publish the configuration files (`config/comments.php` and `config/smilies.php`), the assets folder (`public/vendor/comments`) and the database migrations __*__.<br><br>
5. Finally, run: 
```php
php artisan migrate
```
6. Head over to the [Usage](usage.md) section to get started. 

<br> 
__*__ The migrations will add 3 tables `comments`, `comment_votes`, `comment_options` and a `role` field to your users table. This field will be used to determine if the the authenticated user is an admin or a regular user. <br>
If your app already has another method to determine that, then delete the `..._add_users_role_column.php` migration.

### Requirements & Browser Support

Laravel Comments requires Laravel 5.1 and supports the following browsers (desktop and mobile): Chrome, Firefox, Opera, Safari MS Edge and IE9+.

<style>.docs-content ol { padding-left: 20px; }</style>
