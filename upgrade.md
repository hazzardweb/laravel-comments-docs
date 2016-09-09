# Upgrade Guide

- [Upgrading To 1.2 From 1.1](#upgrading-to-12-from-11)
- [Upgrading To 1.1 From 1.0](#upgrading-to-11-from-10)

## Upgrading To 1.2 From 1.1

- Add `src/Jobs/SelfHandling.php`
- Replace `src/Comments/Comment.php`
- Replace `src/CommentsServiceProvider.php`
- Replace `src/Http/Controllers/AdminSettingsController.php`
- Replace `src/Http/routes.php`
- Replace `src/Jobs/FetchCommentsAdmin.php`

## Upgrading To 1.1 From 1.0

- Replace `public`, `resources`, `package.json`, `gulpfile.js` and add `elixir-uglify.js`.
- See the [usage](usage.md#include-the-javascript-files) section and include the new JavaScript files.
- If you have customized the views, you should replace with the new ones and make the required changes.
