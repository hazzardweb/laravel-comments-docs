# Changelog

### Git

To get the latest updates go to [git.hazzardweb.com](https://git.hazzardweb.com), log in with your Envato account and then browse repository.

## 4.0.0 (2021-10-10)

- Upgraded to Bootstrap 5.1.
- Update npm dependencies.
- Dropped IE support.

## 3.0.0 (2021-04-10)

- Added support for Laravel 8
- Added support for PHP 8
- Dropped support for Laravel 5.*

## 2.0.7 (2020-03-29)

- Update npm packages to support Node 12+

## 2.0.6 (2020-03-28)

- Added support for Laravel 7

## 2.0.5 (2019-09-26)

- Added support for Laravel 6

## 2.0.4 (2018-06-28)

- Hide reply button for guests (when `allow_guests` is disabled).

## 2.0.3 (2018-01-16)

- Fixed config key for model
- Fixed scroll to comment and pagination
- Only override config if not cached

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
