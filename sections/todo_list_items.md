Todo List Items
===============

For the full XML representation of todo items, [check out the data reference](https://github.com/basecamp/basecamp-classic-api/blob/master/sections/data_reference.md#todo_item).

Get all items (for a list)
--------------------------

* `GET /todo_lists/#{todo_list_id}/todo_items.xml` returns all todo item records for a single todo list.

This is almost the same as the “Get list” action, except it does not return any information about the list itself. The items are returned in priority order, as defined by how they were ordered either in the web UI, or via the “Reorder items” action.

**Response:**

``` xml
<todo-items type="array">
  <todo-item>
    ...
  </todo-item>
  ...
</todo-items>
```


Get item
--------

* `GET /todo_items/#{id}.xml` returns a single todo item record, given its integer ID.

**Response:**

``` xml
<todo-item>
  ...
</todo-item>
```


Complete item
-------------

* `PUT /todo_items/#{id}/complete.xml` marks the specified todo item as completed.

**Response:**

Returns HTTP status code 200 on success.


Uncomplete item
---------------

* `PUT /todo_items/#{id}/uncomplete.xml` marks the specified todo as uncompleted.

If the specified todo item was previously marked as completed, this unmarks it, restoring it to an “uncompleted” state. If it was already in the uncompleted state, this call has no effect.

**Response:**

Returns HTTP status code 200 on success.


New item
--------

* `GET /todo_lists/#{todo_list_id}/todo_items/new.xml` returns a “blank” XML record that may be used as a template for creating a new todo item. 

Just fill in the fields and submit the data as indicated by the custom X-Create-Action HTTP header.

**Response:**

``` xml
<todo-item>
  ...
</todo-item>
```


Create item
-----------

* `POST /todo_lists/#{todo_list_id}/todo_items.xml` creates a new todo item record for the given list.

The new record begins its life in the `uncompleted` state. (See the “Complete” and “Uncomplete” actions.) It is added at the bottom of the given list. If a person is responsible for the item, give their id as the party_id value. If a company is responsible, prefix their company id with a ‘c’ and use that as the party_id value. If the item has a person as the responsible party, you can also use the `notify` key to indicate whether an email should be sent to that person to tell them about the assignment.

**Request:**

``` xml
<todo-item>
  <content>#{content}</content>

  <!-- if the item has a due date (in the company time zone) -->
  <due-at>#{due_at}</due-at>

  <!-- if the item has a responsible party -->
  <responsible-party>#{party_id}</responsible-party>
  <notify type="boolean">#{true|false}</notify>
</todo-item>
```

**Response:**

Returns HTTP status code 201 Created on success, with the Location header being set to the URL for the new item. (The new item’s integer ID may be extractd from that URL.)


Update item
-----------

* `PUT /todo_items/#{id}.xml` updates an existing todo item record with the given data.

See the “Create item” action for a full discussion of the meaning of the data fields.

**Request:**

``` xml
<todo-item>
  <content>#{content}</content>

  <!-- if the item has a responsible party -->
  <responsible-party>#{party_id}</responsible-party>
  <notify type="boolean">#{true|false}</notify>
</todo-item>
```

**Response:**

Returns HTTP status code 200 on success.


Edit item
---------

* `GET /todo_items/#{id}/edit.xml` returns an XML record for the requested todo item, ready to be modified and submitted via the “Update item” action.

A custom HTTP header, `X-Update-Action`, is also given, indicating where and how the data may be submitted.

**Response:**

``` xml
<todo-item>
  ...
</todo-item>
```


Destroy item
------------

* `DELETE /todo_items/#{id}.xml` destroys the given todo item record.

**Response:**

Returns HTTP status code 200 on success.


Reorder items
-------------

* `POST /todo_lists/#{todo_list_id}/todo_items/reorder.xml` changes the ordering of the items for the given list.

Completed items cannot be reordered, and any items not specified will be sorted after the items explicitly given (allowing you to easily move a single item to the head of the list without having to specify the positions of all the other items). You may reparent items by putting items from one list into the ordering of items for a different list (though items cannot be reparented across project boundaries).

**Request:**

``` xml
<todo-items type="array">
  <todo-item><id>#{id}</id></todo-item>
  ...
</todo-items>
```

**Response:**

Returns HTTP status code 200 on success.
