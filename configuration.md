# Configuration

- [reCAPTCHA](#recaptcha)
- [BBCode](#bbcode)

All of the configuration options for the Laravel Comments are stored in `config/comments.php`.
You may also change the options from the __Settings__ page in the admin panel.

> Notice: The options from the admin panel will always have priority over the one from the file.

## reCAPTCHA

Add `"marwelln/recaptcha" : "~2.0"` to your `composer.json` file and run `composer update`.

Add `'Marwelln\Recaptcha\RecaptchaServiceProvider'` to your `providers` array in `config/app.php`.

Run `php artisan vendor:publish --provider="Marwelln\Recaptcha\RecaptchaServiceProvider"`.

Get your recaptcha keys at [google.com/recaptcha/admin](https://www.google.com/recaptcha/admin) and copy them in `config/recaptcha.php`.

Now you can enable the `captcha` option in `config/comments.php` or from the __Settings__ page under the __Protection__ tab.

## BBCode

Laravel Comments includes the default bbcode tags like `[b][/b]`, `[i][/i]`, `[u][/u]`, `[url][/url]`, `[img][/img]`, `[color][/color]` and a few custom `[code=language][/code]` (see [language](http://prismjs.com/#languages-list)) , `[quote][/quote]` and `[youtube]video-id[/youtube]`.

Because it uses the [jBBCode](http://jbbcode.com) package you can add any other tags you want. <br>
You can add the tags in `comments/src/Formatting/BBCodeDefinitionSet.php`, or/and if you need the parser instance (`JBBCode\Parser`) you can access like this:

```php
$parser = app('comments.formatter')->getBBCode();
```

Please refer to the [JBBCode documentation](http://jbbcode.com) for more.
