Categories
==========

The categories API is identical for both Post categories, and Attachment categories, the only difference being the "type" parameter, which can be either "post" or "attachment".

For the full XML representation of categories, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#category).

Get category
------------

* `GET /categories/#{id}.xml` returns a single category identified by its integer ID.

**Response:**

``` xml
<category>
  <name>Documents</name>
  ...
<category>
```

Get categories
--------------

* `GET /projects/#{project_id}/categories.xml(?type=[post|attachment])` returns all categories for the given project.

To filter by type, pass the `type` parameter, which can be one of `post` or `attachment`.

**Response:**

``` xml
<categories>
  <category>
    <name>Documents</name>
    ...
  </category>
  ...
</categories>
```


Create category
---------------

* `POST /projects/#{project_id}/categories.xml` creates a new category of the given type for the given project.

The `type` attribute is required and must be one of `post` or `attachment`.

**Request:**

``` xml
<category>
  <type>post</type>
  <name>Transcripts</name>
</category>
```


**Response:**

Returns HTTP status code 201 Created on success, with the Location header set to the “Get category” URL for the new category. The new category ID can be extracted from that URL. On failure, a non-200 status code will be returned, possibly with error information in XML format as the response’s content.

Update category
---------------

* `PUT /categories/#{id}.xml` updates an existing category identified by its integer ID.

**Request:**

``` xml
<category>
  <name>Transcripts</name>
</category>
```


**Response:**

Returns HTTP status code 200 on success, or any other code (and possibly error information in XML format) on error.

Destroy category
----------------

* `DELETE /categories/#{id}.xml` deletes the category identified by its integer ID.

Note: that only categories without elements can be deleted.

Returns HTTP status code 200 on success. If the category contains elements a 409 status code (conflict) will be returned.
