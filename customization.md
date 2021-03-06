# Customization

- [Assets](#assets)
- [Views](#views)
- [Translations](#translations)

## Assets

If you wish to edit something in the JavaScript/Sass files, you have to compile them with [Laravel Mix](https://laravel.com/docs/8.x/mix).

From your terminal, cd into the `laravel-comments` directory and install the npm dependencies (Node >= 8.10 required):

With npm:

```bash
npm install
```

Or with yarn:

```bash
yarn
```

After you make your changes run `npm run build` to compile the assets.

Each time the assets are compiled you have to run `php artisan vendor:publish --provider=Hazzard\Comments\CommentsServiceProvider --tag=public --force` to override them in your public directory. 

Or you edit the `webpack.mix.js` and change the `publicPath` variable:

```javascript
const publicPath = './../public/vendor/comments'
```
_Assuming that you have the `laravel-comments` folder in your project root directory._

## Views

If you wish to customize the views run:

```bash
php artisan vendor:publish --provider=Hazzard\Comments\CommentsServiceProvider --tag=views --force
```

Then edit them from `resources/views/vendor/comments`.

## Migrations

If you wish to customize the migrations publish them before migrating:

```bash
php artisan vendor:publish --provider="Hazzard\Comments\CommentsServiceProvider" --tag=migrations
```

## Translations

See [Overriding Vendor Language Files](https://laravel.com/docs/8.x/localization#overriding-package-language-files).
