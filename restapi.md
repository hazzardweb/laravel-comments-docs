# REST API

- [Comments Endpoints](#comments-endpoints)
- [Admin Dashboard Endpoints](#admin-dashboard-endpoints)
- [Admin Settings Endpoints](#admin-settings-endpoints)
 
## Comments Endpoints

### Retreive Comments

To retrieve the comments, send a __GET__ request to `/comments` with the following parameters:

Name | Type | Description
-----|------|------------
page_id | string | The page unique identifier.
target | int | A linked comment id. (Optional)
page | int | The page number. (Optional)
sort | int | The sorting option (newest, oldest, best). <br> Supported: `1`, `2`, `3`. (Optional)

The response will be a JSON object with two keys called `comments` and `pagination`. 

The value of the `comments` key will be an array of comment objects, each of which contain the following attributes:

Name          | Type             | Description
--------------|------------------|-------------------------------------------
id            | int              | The comment unique id. 
user_id       | int&#124;null    | The comment user id, if exists.
author        | object           | The comment author object.
author.avatar | string           | The author avatar image url.
author.name   | string           | The author name. 
author.url    | string           | The author url.
canEdit       | bool             | Whether the current user can edit the comment.
content       | string           | The comment content.
contentHTML   | string           | The comment content rendered as HTML.
edit_link     | string           | The link to the admin edit page.
page_id       | string           | The comment unique identifier.
permalink     | string           | The comment permalink.
parent_id     | int&#124;null    | The parent comment id. 
root_id       | int&#124;null    | The root comment id.
status        | string           | The comment status. Values: `pending`, `approved`, `spam`, `trash`.
replies       | array            | An array of comment replies.
downvotes     | int              | The number of downvotes.
upvotes       | int              | The number of upvotes.
voted         | string&#124;null | Whether the current user has voted the comment. Values: `up` / `down`, `null` otherwise. 
created_at    | string           | The comment creation timestamp in ISO 8601 format.
updated_at    | string           | The comment update timestamp in ISO 8601 format.

The value of the `pagination` key will be an object of comment objects, containing the following attributes:

Name         | Type          | Description
-------------|---------------|---------------------------------
current_page | int           | The number of the current page.
last_page    | int           | The number of the last page.
next_page    | int&#124;null | The next page number.
prev_page    | int&#124;null | The previous page number.
per_page     | int           | The number of comments per page.
total        | int           | The total number of comments.

### Post a new Comment

To post a new comment, send a __POST__ request to `/comments`. Set the attributes for the comment you are creating:

Name                 | Type   | Description                  | Required 
---------------------|--------|------------------------------|----------
content              | string | The comment content.         | yes 
author_name          | string | The author name.             | Only if guest. 
author_email         | string | The author email address.    | Only if guest. 
author_url           | string | The author url.              | Only if guest. 
page_id              | string | The page unique identifier.* | yes 
parent_id            | int    | The parent comment id.*      | no 
root_id              | int    | The root comment id.*        | no 
permalink            | string | The current page permalink.  | no 
g-recaptcha-response | string | The recaptcha response.      | Only if captcha is enabled.

&#42; If the posted comment is a reply, the `parent_id` must be the id of the parent comment (the comment you're replying) and the `root_id` must be the id of the root comment.

On success the response status will be `201`, containing a JSON object containing the comment attributes (see [Retreive Comments](#retreive-comments)).

If the validation fails, the response status will be `422`, containing an array of error messages.

Example:
```json
[
    "The author name field is required.",
    "The author email field is required.",
    "The content field is required."
]
```

### Update an existing Comment

To update an existing comment, send a __PUT__ request to `/comments/:id`. Any attribute for the comment can be set to a new value:

Name    | Type   | Description          | Required
--------|--------|----------------------|---------
content | string | The comment content. | yes

On success the response will have a `200` status code and will be a JSON object containing the comment attributes (see [Retreive Comments](#retreive-comments)).

If the comment you're trying to update doesn't exists the response status will be `404`.
If you don't have the permission to edit the comment the response status will be `403`.
If the validation fails, the response status will be `422`, containing an array of error messages.

### Vote a Comment

To vote an existing comment, send a __POST__ request to `/comments/:id/vote` with the `type` attribute having one of the following values: 
- `up` - upvote the comment 
- `down` - downvote the comment 
- `remove` - remove the upvote or downvote

On success the response status will be `200` with no content.

If the comment doesn't exists the response status will be `404`.

## Admin Dashboard Endpoints

### Retreive all Comments

To retrieve the comments, send a __GET__ request to `/comments/admin` with the header `X-Requested-With` set to `XMLHttpRequest` (must be an AJAX request, see `AdminDashboardController@index`) and the following parameters:

Name   | Type   | Description                          | Default
-------|--------|--------------------------------------|-----------------------------
pageId | string | A page unique identifier. (Optional) | n\a
page   | int    | The page number. (Optional)          | `1`
status | int    | Values: `all`, `pending`, `approved`, `spam`, `trash`. (Optional) | `all`

### Retreive an existing Comment

To retrieve a comment, send a __GET__ request to `/comments/admin/:id`.

The response will be a JSON object containing the comment attributes (see [Retreive Comments](#retreive-comments)).

If the comment doesn't exists the response status will be `404`.

### Update an existing Comment

To update an existing comment, send a __PUT__ request to `/comments/admin/:id`. Any attribute for the comment can be set to a new value:

Name         | Type   | Description         
-------------|--------|---------------------
content      | string | The comment content.
status       | string | The comment status. Values: `pending`, `approved`, `spam`, `trash`.
author_name  | string | The author name.
author_email | string | The author email
author_url   | string | The author url.

On success the response will have a `200` status code and will be a JSON object containing the comment attributes (see [Retreive Comments](#retreive-comments)).

If the comment you're trying to update doesn't exists the response status will be `404`.
If the validation fails, the response status will be `422`, containing an array of error messages.

### Bulk Update/Delete

To perform a bulk update/delete, send a __PUT__ request to `/comments/admin` with the following attributes:

Name   | Type   | Description         
-------|--------|---------------------
ids    | array  | An array of comment ids you want to update or delete.
status | string | The new comment status: `pending`, `approved`, `spam`, `trash`. <br> Or `delete`, if you want to permanently delete the comments.

On success the response will have a `200` status code containing the number of affected comments.

### Delete a Comment 

To delete a comment, send a __DELETE__ request to `/comments/admin/:id`.

The comment will be deleted and the response status will be a `204`.

### Admin Settings Endpoints

To update the settings, send a __PUT__ request to `comments/admin/settings` and you must specify two attributes:

A key called `group`, that can have one of the values `general`, `formatting`, `moderation`, `protection`, `notifications`.

A key called `settings`, that is an array of objects with the `name` and `value` keys. The `name` keys can be found in `AdminSettingsController` under the `update{group}Settings` methods and the `value` is the new value you want to set.
