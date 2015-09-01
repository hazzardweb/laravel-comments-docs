# Configuration

- [reCAPTCHA](#recaptcha)
- [Real Time](#real-time)
- [Formatting](#formatting)

All of the configuration options for the Laravel Comments are stored in `config/comments.php`.
You may also change the options from the __Settings__ page in the admin panel.

> Notice: The options from the admin panel will always have priority over the one from the file.

## reCAPTCHA

Add `"marwelln/recaptcha" : "~2.0"` to your `composer.json` file and run `composer install`.

Add `'Marwelln\Recaptcha\RecaptchaServiceProvider'` to your `providers` array in `config/app.php`.

Run `php artisan vendor:publish --provider="Marwelln\Recaptcha\RecaptchaServiceProvider"`.

Get your recaptcha keys at [google.com/recaptcha/admin](https://www.google.com/recaptcha/admin) and copy them in `config/recaptcha.php`.

Now you can enable the `captcha` option in `config/comments.php` or from the __Settings__ page under the __Protection__ tab.

## Real Time

If you wish to enable real time comments, you need to have a [broadcast](http://laravel.com/docs/5.1/events#broadcasting-events) driver configured (works with Pusher and Redis with Socket.IO).

When using the Redis driver, you must have Node server with [Socket.IO](http://socket.io) running and add it to your `redis` connection in `config/broadcasting.php`.

```php
'redis' => [
    'driver'     => 'redis',
    'connection' => 'default',
    'socket'     => 'http://localhost:3000', // <=
],
```

To run the Node socket, download the [scoket.js](https://github.com/hazzardweb/ajax-comment-system-laravel-demo/blob/master/socket.js) file and run `node socket.js`.

Learn more about [broadcasting events](https://laracasts.com/lessons/broadcasting-events-in-laravel-5-1) in Laravel.

## Formatting

The script uses the [TextFormatter](https://github.com/s9e/TextFormatter) package and allows you to highly customize the comment formatter. <br> By default you have some options to choose from, but if you want to add even more options you can configure the formatter however you want using the `Hazzard\Comments\Events\FormatterConfigurator` [event](events.md):

First [define a listener](http://laravel.com/docs/5.1/events#defining-listeners), then [register](http://laravel.com/docs/5.1/events#registering-events-and-listeners) it in the `EventServiceProvider`.

#### Example

__app/Providers/EventServiceProvider.php__

```php
protected $listen = [
    'Hazzard\Comments\Events\FormatterConfigurator' => [
        'App\Listeners\ConfigureFormatter',
    ],
];
```

__app/Listeners/ConfigureFormatter.php__

```php
<?php

namespace App\Listeners;

use s9e\TextFormatter\Configurator;
use Hazzard\Comments\Events\FormatterConfigurator;

class ConfigureFormatter
{
    /**
    * Create the event listener.
    *
    * @return void
    */
   public function __construct()
   {
       //
   }

   /**
    * Handle the event.
    *
    * @param  FormatterConfigurator $event
    * @return void
    */
   public function handle(FormatterConfigurator $event)
   {
       // Access the configurator using $event->configurator...
       
       $event->configurator->Emoticons->add(':)', '&#x1f604;');
   }
}
```

Learn more about the [TextFormatter](http://s9etextformatter.readthedocs.org/).

> Notice: Each time you change something related to the formatter, you must run `php artisan cache:clear` to clear the formatter configuration cache. 
