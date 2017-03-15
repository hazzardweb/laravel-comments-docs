# Upgrade Guide

- [Upgrading To 2.0 From 1.2](#upgrading-to-20-from-12)

## Upgrading To 2.0 From 1.2

Since this is a major update only the database tables can be upgraded.
This means you can keep your comments but you'll have to reinstall and update the usage of the comments.

Run:

```bash
php artisan config:clear
php artisan route:clear
php artisan cache:clear
```

Delete `app/comments`, `public/vendor/comments` and `config/comments.php`.

Edit `composer.json` and remove `"Hazzard\\Comments\\": "app/comments/src/"` and`"s9e/text-formatter": "^0.4"`.

Edit `config/app.php` and remove `Hazzard\Comments\CommentsServiceProvider::class` from your `providers` array.

Run `composer dumpautoload`

Now follow the [Installation](installation.md) guide but remember: __DO NOT RUN__ `php artisan migrate` yet.

Once you've re-installed the comments you can continue.

Run `composer require doctrine/dbal`. This package is required by Laravel in order to [modify columns](https://laravel.com/docs/5.4/migrations#modifying-columns).

Cd into `laravel-comments/migrations` and delete:
- `2017_02_03_00001_create_comments_table.php`
- `2017_02_03_00002_create_comment_votes_table.php`

Then create a new migration `2017_02_13_00005_update_comments_table.php`:

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class UpdateCommentsTable extends Migration
{
    public function up()
    {
        Schema::getConnection()
                ->getDoctrineSchemaManager()
                ->getDatabasePlatform()
                ->registerDoctrineTypeMapping('enum', 'string');

        Schema::table('comments', function (Blueprint $table) {
            $table->nullableMorphs('commentable');
            $table->string('page_id')->nullable()->change();
            $table->string('author_ip')->nullable()->change();
            $table->string('user_agent')->nullable()->change();
            $table->string('permalink')->nullable()->change();
        });
    }

    public function down()
    {
        Schema::table('comments', function (Blueprint $table) {
            $table->dropColumn('commentable_id');
            $table->dropColumn('commentable_type');
        });
    }
}
```

This migration will add 2 new columns and update some old ones.

Finally, run `php artisan migrate` to update the comments table.

Head over to the [Usage](usage.md) section to get started.
