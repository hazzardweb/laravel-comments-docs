# Events

<hr>

To listen for an event, first you need to [define a listener](http://laravel.com/docs/5.1/events#defining-listeners), then [register](http://laravel.com/docs/5.1/events#registering-events-and-listeners) it in the `EventServiceProvider`.

#### Example

__app/Providers/EventServiceProvider.php__

```php
protected $listen = [
    'Hazzard\Comments\Events\CommentWasPosted' => [
        'App\Listeners\SendEmailNotification',
    ],
];
```

__app/Listeners/SendEmailNotification.php__

```php
<?php

namespace App\Listeners;

use Hazzard\Comments\Comments\Comment;
use Hazzard\Comments\Events\CommentWasPosted;

class SendEmailNotification
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
    * @param  CommentWasPosted $event
    * @return void
    */
   public function handle(CommentWasPosted $event)
   {
       // Access the comment using $event->comment...
   }
}
```

You can find all of Ajax Comment System events in the `src/Events` folder.
