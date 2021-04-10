# Events

<hr>

To listen for an event, first you need to [define a listener](https://laravel.com/docs/8.x/events#defining-listeners), then [register](https://laravel.com/docs/8.x/events#registering-events-and-listeners) it in `EventServiceProvider`:

__app/Providers/EventServiceProvider.php__

```php
protected $listen = [
    'Hazzard\Comments\Events\CommentWasPosted' => [
        'App\Listeners\HandleCommentWasNotification',
    ],
];
```

__app/Listeners/HandleCommentWasNotification.php__

```php
<?php

namespace App\Listeners;

use Hazzard\Comments\Comments\Comment;
use Hazzard\Comments\Events\CommentWasPosted;

class HandleCommentWasNotification
{
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

You can find all of events in the `src/Events` folder.
