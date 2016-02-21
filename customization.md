# Customization

- [Assets](#assets)
- [Views](#views)
- [Translations](#translations)
- [Not Found Exceptions](#not-found-exceptions)

## Assets

If you wish to edit something in the JavaScript/Sass files, you have to compile them with [Laravel Elixir](http://laravel.com/docs/5.2/elixir).

From your terminal, cd into the `comments` directory, then [install](http://laravel.com/docs/5.2/elixir#installation) Laravel Elixir (`npm install`).

Now you can edit the JavaScript/Sass files and [run Elixir](http://laravel.com/docs/5.2/elixir#running-elixir) with `gulp` or `gulp watch`.

Each time the assets are compiled you have to run `php artisan vendor:publish --tag="public" --force` to override them in your public directory. 

Or you edit the `gulpfile.js` file and change the `jsDest` and `cssDest` variables:

```javascript
var jsDest  = '../../public/vendor/comments/js/';
var cssDest = '../../public/vendor/comments/css/';
```
_Assuming that you have the `comments` folder in your `app` directory._

## Views

If you wish to customize the views copy the view files from `comments/resources/views` to `resources/vendor/comments` and edit there.

## Translations

See [Overriding Vendor Language Files](http://laravel.com/docs/5.2/localization#overriding-vendor-language-files).

## Not Found Exceptions

To catch `ModelNotFoundException` exceptions edit `app/Exceptions/Handler.php` and add in the `render` method:

```php
public function render($request, Exception $e)
{
    if ($e instanceof \Illuminate\Database\Eloquent\ModelNotFoundException && $request->ajax()) {
        return response()->json('Not found.', 404);
    }

    return parent::render($request, $e);
}
```
