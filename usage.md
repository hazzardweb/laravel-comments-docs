# Usage

<hr>

### The Author Interface

Your `User` class/model must implement the `Hazzard\Comments\Author\AuthorContract` interface. This interface imposes these methods: `getAuthorName`, `getAuthorEmail`, `getAuthorAvatar`, `getAuthorUrl` and `userIsAdmin`. <br>

If you have a standard `User` model just import the `Hazzard\Comments\Author\Author` trait and you should be good to go. This trait will use the `name` or `username` fields for the `getAuthorName` method, the `email` field for the `getAuthorEmail` and `getAuthorAvatar` methods and the `role` field for the `userIsAdmin` method.

__Example:__
```php
...
use Hazzard\Comments\Author\Author;
use Hazzard\Comments\Author\AuthorContract;

use Illuminate\Database\Eloquent\Model;
...

class User extends Model implements ..., AuthorContract // <= Implement interface
{
    use ..., Author; // <= Import trait
    ...
}
```

Of course you can implement the methods by yourself.

### Include the CSS files

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

### Include the JavaScript files

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
> Make sure you you have the [Authentication](authentication.md) configured.

### Display the Comments

```php
@include('comments::display', ['pageId' => 'page1'])
```

The `pageId` parameter should be set to an unique identifier (int/string) for each page. 

### Admin Panel

To access the Admin Panel make sure the user that you're logged in with has the `role` field set to `admin` in the database.
