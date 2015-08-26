# Customization

- [Assets](#assets)
- [Views](#views)
- [Translations](#translations)

## Assets

If you wish to edit something in the JavaScript (or less) files, you have to compile them with [Laravel Elixir](http://laravel.com/docs/5.1/elixir).

From your terminal/console cd into the `comments` directory and [install](http://laravel.com/docs/5.1/elixir#installation) Laravel Elixir there.  

Now you can edit the JavaScript files and [run Elixir](http://laravel.com/docs/5.1/elixir#running-elixir) with `gulp` or `gulp watch`.

Each time you compile the assets you have to run `php artisan vendor:publish --tag="public" --force` to override the compiled assets (or change the `jsDest` and `cssDest` variables in the `gulpfile.js` file).

## Views

If you wish to customize the views copy the view files from `comments/resources/views` to `resources/vendor/comments` and edit there.

## Translations

See [Overriding Vendor Language Files](http://laravel.com/docs/5.1/localization#overriding-vendor-language-files).
