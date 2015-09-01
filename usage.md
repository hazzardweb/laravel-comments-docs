# Usage

<hr>

### The Get Author Method

In your `User` class/model you must add the `getAuthor` method that has to return some user attributes: 

```php
class User extends Model implements ...
{
    /**
     * Return the user attributes.

     * @return array
     */
    public function getAuthor()
    {
        return [
            'id'     => $this->id,
            'name'   => $this->name,
            'email'  => $this->email,
            'url'    => $this->url,  // Optional
            'avatar' => 'gravatar',
            'admin'  => $this->role === 'admin', // bool
        ];
    }
}
```

By default the avatar is set to Gravatar, but you can return an image.

The `admin` attribute makes use of the `role` field, added to the users table in the [installation](#installation.md) part. <br> If you have another way of detecting if the user is admin, then the `admin` attribute must a boolean value.

### Include The CSS Files

```markup
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
<link rel="stylesheet" href="/vendor/comments/css/prism-okaidia.css"> <!-- Optional -->
<link rel="stylesheet" href="/vendor/comments/css/comments.css">
```

> Note: 
> #### No Bootstrap!
> If you don't use Bootstrap, include `/vendor/comments/css/bootstrapless.css` instead of `bootstrap.min.css`.<br>
> By doing so, the Bootstrap CSS will be isolated to the comments and won't conflict with your CSS.

<style>.callout-info p:first-child { display: none; }</style>

### Include The JavaScript Files

```markup
<script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
<script src="/vendor/comments/js/prism.js"></script> <!-- Optional -->
<!-- This must be included before the closing </body> tag! -->
<script src="/vendor/comments/js/comments.js"></script> 
```

If you have already included jQuery or Bootstrap JS you don't have to include them again. <br>
Even if your app doesn't use Bootstrap, the `bootstrap.min.js` file is still required.

> Notice: 
> Make sure you you have the [Laravel Authentication](http://laravel.com/docs/5.1/authentication) driver configured.

### Display The Comments

```php
@include('comments::display', ['pageId' => 'page1'])
```

The `pageId` parameter should be set to an unique identifier (int/string) for each page. 

### Access The Admin Panel

You can access the Admin Panel at `/comments/admin`, but make sure the user that you're logged in with has the `role` field set to `admin` in the database.

If you have something like `phpMyAdmin` just edit the role field or you can write a simple query to edit a user:

```php
$user = \App\User::find(1);
$user->role = 'admin';
$user->save();
```
