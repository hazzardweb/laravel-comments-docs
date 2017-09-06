# Changelog

### Git

To get the latest updates go to [git.hazzardweb.com](https://git.hazzardweb.com), log in with your Envato account and then browse repository.

## 2.0.2 (2017-09-06)

- Fixed bug in `CommentsServiceProvider.php` introduced in the previous release.

## 2.0.1 (2017-09-01)

- Fixed `api.js` filename for Unix systems.
- Removed check for settings table.
- Added support for Laravel 5.5 package discovery.
- Update internal tooling.

## 2.0.0 (2017-04-19)

- Added IE10 compatibility.
- Fixed Pusher empty options.
- Fixed `StoreComment` request.
- Replace [Zenscroll](https://github.com/zengabor/zenscroll) with [MoveTo](https://github.com/hsnaydd/moveTo).

## 2.0.0-beta.2 (2017-03-23)

- Added compatibility with Laravel 5.1 and 5.2.

## 2.0.0-beta.1 (2017-03-13)

The script has been rewritten from scratch. It now uses a iframe to embed the comments so it doesn't interfere anymore with the app you're using the comments in.

New Features:

- Bootstrap 4
- Embed via iframe
- Comment reports
- Comment preview
- Support for commentable models
