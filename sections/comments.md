Comments
========

The comments API is identical for Messages, Milestones, Todo Items, and Calendar Events, the only difference being the resource named in URL prefix. This can be one of `posts`, `milestones`, `todo_items`, or `calendar_events`, respectively. In the documentation that follows, the generic `#{resource}` should be replaced with the resource you are acting on.

For the full XML representation of comments, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#comment).

Get recent comments (for a commentable resource)
------------------------------------------------

* `GET /#{resource}/#{resource_id}/comments.xml` return a list of the 50 most recent comments associated with the specified resource.

The resource named in the URL can be one of `posts`, `milestones`, or `todo_items`. For example, to fetch the most recent comments for the todo item with an id of 1, you would use the path: `/todo_items/1/comments.xml`.

The root `<comments>` element has a `count` attribute specifying the total number of comments for the resource. If there are older comments not included in the response, the `<comments>` element will also have a `continued-at` attribute specifying the path where the next oldest 50 comments can be retrieved.

**Response:**

``` xml
<comments count="50" continued-at="...">
  <comment>
    ...
  </comment>
  <comment>
    ...
  </comment>
  ...
</comments>
```


Get comment
-----------

* `GET /comments/#{comment_id}.xml` retrieve a specific comment by its id.

**Response:**

``` xml
<comment>
  ...
</comment>

```


New comment
-----------

* `GET /#{resource}/#{resource_id}/comments/new.xml` returns a blank XML “template” for a single comment record, indicating which fields may be submitted to create a new comment.

This endpoint will also return a custom HTTP header, `X-Create-Action` indicating where and how the data may be submitted.

**Response:**

``` xml
<comment>
  ...
</comment>

```


Create comment (for a commentable resource)
-------------------------------------------

* `POST /#{resource}/#{resource_id}/comments.xml` create a new comment, associating it with a specific resource.

The resource named in the URL can be one of `posts`, `milestones`, or `todo_items`. For example, to create a comment for the milestone with an ID of 1, you would use the path: `/milestones/1/comments.xml`.

**Request:**

``` xml
<comment>
  <body>#{body}</body>
</comment>
```


**Response:**

Returns HTTP status code 201 Created on success, with the Location header set to the URL for the new comment. The new comment’s ID can be extracted from that URL. On failure, a non-200 status code will be returned, possibly with error information in XML format as the response’s content.


Edit comment
------------

* `GET /comments/#{id}/edit.xml` returns an XML “template” for a single comment record, prefilled with the existing values for that record, and ready to be resubmitted via the “update comment” action. 

This endpoint will also return a custom HTTP header, `X-Update-Action`, indicating where and how the data may be submitted.

**Response:**

``` xml
<comment>
  ...
</comment>

```


Update comment
--------------

* `PUT /comments/#{id}.xml` update a specific comment. This can be used to edit the content of an existing comment.

**Request:**

``` xml
<request>
  <comment>
    <body>#{body}</body>
  </comment>
</request>
```

**Response:**

Returns HTTP status code 200 on success, or any other code (and possibly error information in XML format) on error.


Destroy comment
---------------

* `DELETE /comments/#{id}.xml` delete the comment with the given ID.

**Response:**

Returns HTTP status code 200 on success.
