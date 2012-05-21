Files
=====

For the full XML representation of files, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#attachment).

Get files
---------

* `GET /projects/#{project_id}/attachments.xml(?n=...)` returns a list of files (attachments) in the given project that are visible to the authenticated user.

The list is paginated using offsets. If 100 attachments are returned (the page limit), use `?n=100` to check for the next 100 and so on.

**Response:**

``` xml
<attachments>
  <attachment>
    ...
  </attachment>
  <attachment>
    ...
  </attachment>
  ...
</attachments>
```
