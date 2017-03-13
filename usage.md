# Usage

### The Author Attributes Method

In your `User` model add a `authorAttributes` method that return some user attributes: 

```php
...

class User extends Authenticatable
{
    /**
     * @return array
     */
    public function authorAttributes()
    {
        return [
            'name' => $this->name,
            'email' => $this->email,
            'url' => $this->url,    // optional
            'avatar' => 'gravatar', // optional
        ];
    }
}
```

By default the avatar is set to Gravatar, but you can return an image url.

### Include the CSS 

```markup
<link href="/vendor/comments/comments.css" rel="stylesheet">
```

Or if you use Laravel 5.4+ you can make use of the `mix` helper:

```markup
<link href="{{ mix('comments.css', 'vendor/comments') }}" rel="stylesheet">
```

### Include the JavaScript 

```markup
<script src="/vendor/comments/comments.js"></script>
```

Again, if you use Laravel 5.4+ you can make use of the `mix` helper:

```markup
<script src="{{ mix('comments.js', 'vendor/comments') }}"></script>
```

### Display the Comments

Add a `div` element with an id:

```markup
<div id="my-comments"></div>
```

Then add the JavaScript that loads the comments:

```markup
<script>
    new Comments.default({
        el: '#my-comments',
        pageId: 'my-page-id'
    })
</script>
```

The `pageId` should be set to an unique identifier (integer or string) for each page. 

If you have a ["commentable model"](https://laravel.com/docs/5.4/eloquent-relationships#polymorphic-relations), like a page or post you can use:

```markup
<script>
    new Comments.default({
        el: '#my-comments',
        commentableId: {{ Page::first()->id }},
        commentableType: 'App.Page'
    })
</script>
```

Where `commentableId` is your model id and the `commentableType` is your model class name.

### Access The Admin Panel

Make sure you you have the [Authentication](http://laravel.com/docs/5.4/authentication) configured so you can log in.

You need to define a [gate](https://laravel.com/docs/5.4/authorization#gates) to determine what users have access to the admin panel:

```php
// app/providers/AuthServiceProvider.php

...

class AuthServiceProvider extends ServiceProvider
{
    ...

    public function boot()
    {
        $this->registerPolicies();
    
        /**
         * Determine if the current user can access the admin panel.
         *
         * @param  User $user                        
         * @return bool
         */
        \Gate::define('moderate-comments', function ($user) {
            // Add your own logic here...
            return (bool) $user->is_admin === true;
        });
    }
}
```

Now you can access the Admin Panel at `/comments/admin`.
