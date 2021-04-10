# Configuration

- [reCAPTCHA](#recaptcha)
- [Real Time](#real-time)
- [Formatting](#formatting)

All of the configuration options can be changed from `config/comments.php` or from the __Settings__ page in the admin panel.

The options from the admin panel will always have priority over the ones from the file.

## reCAPTCHA

Get your recaptcha keys at [google.com/recaptcha/admin](https://www.google.com/recaptcha/admin) and copy them in `config/services.php`:

```php
'recaptcha' => [
    'key' => 'your-key',
    'secret' => 'your-secret',
],
```

Now you can enable captcha from `config/comments.php` or from the __Settings > Protection__ page.

## Real Time

Real Time only works with Laravel 5.3+.

Before enabling this option you need to have a [broadcast](https://laravel.com/docs/8.x/broadcasting) driver configured. you can either use [Pusher](https://pusher.com) or [Redis+Socket.IO](https://socket.io).

## Formatting

The script uses the [TextFormatter](https://github.com/s9e/TextFormatter) package and allows you to highly customize the comment formatter.

By default you have some options to choose from, but if you want to add even more options you can configure the formatter however you want using the `Hazzard\Comments\Events\FormatterConfigurator` [event](events.md):

First [define a listener](https://laravel.com/docs/8.x/events#defining-listeners), then [register](https://laravel.com/docs/8.x/events#registering-events-and-listeners) it in `EventServiceProvider`:

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

Learn more about the [TextFormatter](https://s9etextformatter.readthedocs.io).

> Notice: Each time you change something related to the formatter via the config file, you must run `php artisan cache:clear` to clear the formatter configuration cache. 
