# Events

<hr>

To listen for an event, first you need to [define a listener](http://laravel.com/docs/5.4/events#defining-listeners), then [register](http://laravel.com/docs/5.4/events#registering-events-and-listeners) it in `EventServiceProvider`:

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
