Todo lists
==========

Get all lists (across projects)
-------------------------------

* `GET /todo_lists.xml` returns a list of todo-list records for the current user, with todo-item records assigned to the current user
* `GET /todo_lists.xml?responsible_party=#{id}` returns a list of todo-list records, with todo-item records that are assigned to the given `responsible party`.

The responsible party may be changed by setting the `responsible_party` query parameter to a blank string (for unassigned items), a person-id, or a company-id prefixed by a `c` (e.g., `c1234`).

**Response:**

``` xml
<todo-lists array="true">
  <todo-list>
    ...
    <todo-items array="true">
      <todo-item>
        ...
      </todo-item>
    </todo-items>
  </todo-list>
  ...
</todo-lists>

```


Get all lists (within project)
------------------------------

* `GET /projects/#{project_id}/todo_lists.xml?filter=#{filter}` returns a list of todo-list records that are in the given project.

By default, all lists are returned, but you can filter the result by giving the `filter` query parameter, set to `all` (the default), `pending` (for lists with uncompleted items), and `finished` (for lists that have no uncompleted items). The lists will be returned in priority order, as determined by their ordering.

**Response:**

``` xml
<todo-lists array="true">
  <todo-list>
    ...
  </todo-list>
  ...
</todo-lists>
```


Get list
--------

* `GET /todo_lists/#{id}.xml` returns a single todo-list record identified by its integer ID.

**Response:**

``` xml
<todo-list>
  ...
</todo-list>

```


Edit list
---------

* `GET /todo_lists/#{id}/edit.xml` returns an XML “template” for a single todo-list record, prefilled with the existing values for that record, and ready to be resubmitted via the “update list” action.

This endpoint will also return a custom HTTP header, `X-Update-Action`, indicating where and how the data may be submitted.

**Response:**

``` xml
<todo-list>
  ...
</todo-list>

```


Update list
-----------

* `PUT /todo_lists/#{id}.xml` updates the specified todo-list record with the changes indicated by the submitted XML data.

**Request:**

``` xml
<todo-list>
  <name>#{name}</name>
  <description>#{description}</description>
  <milestone-id>#{milestone_id}</milestone-id>
  <private type="boolean">#{true|false}</private>
  <tracked type="boolean">#{true|false}</tracked> <!-- enable/disable time tracking -->
</todo-list>
```

**Response:**

Returns HTTP status code 200 on success, or any other code (and possibly error information in XML format) on error.


New list
--------

* `GET /projects/#{project_id}/todo_lists/new.xml` returns a blank XML “template” for a single todo-list record, indicating which fields may be submitted to create a new list.

This endpoint will also return a custom HTTP header, `X-Create-Action`, indicating where and how the data may be submitted.

**Response:**

``` xml
<todo-list>
  ...
</todo-list>
```


Create list
-----------

* `POST /projects/#{project_id}/todo_lists.xml` creates a new todo-list based on the submitted XML data.

If you wish to base the new list on a todo-list template that you’ve created previously, you can specify the `todo-list-template-id` field in the data, and the new list will default to the name, description, and todo-items indicated by that template.

**Request:**

``` xml
<todo-list>
  <name>#{name}</name>
  <description>#{description}</description>
  <milestone-id>#{milestone_id}</milestone-id> <!-- optional -->
  <private type="boolean">#{true|false}</private> <!-- optional -->
  <tracked type="boolean">#{true|false}</tracked> <!-- enable/disable time tracking -->

  <!-- if based on an existing todo-list template -->
  <todo-list-template-id>#{template_id}</todo-list-template-id>
</todo-list>
```

**Response:**

Returns HTTP status code 201 Created on success, with the Location header set to the “Get list” URL for the new list. The new list’s ID can be extracted from that URL. On failure, a non-200 status code will be returned, possibly with error information in XML format as the response’s content.


Destroy list
------------

* `DELETE /todo_lists/#{id}.xml` destroys the given todo-list and all of its associated todo items.

**Response:**

Returns HTTP status code 200 on success.


Reorder lists
-------------

* `POST /projects/#{project_id}/todo_lists/reorder.xml` reorders the lists in the project according to the ordering given.

Any lists that are not explicitly specified will be positioned after the lists that are specified.

**Request:**

``` xml
<todo-lists type="array">
  <todo-list><id>...</id></todo-list>
  <todo-list><id>...</id></todo-list>
  ...
</todo-lists>
```

**Response:**

Returns HTTP status code 200 on success.
