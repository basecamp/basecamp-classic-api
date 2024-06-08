Time tracking
=============

For the full XML representation of time entries, [check out the data reference](https://github.com/basecamp/basecamp-classic-api/blob/master/sections/data_reference.md#time_entry).

Get all entries
---------------

* `GET /todo_items/#{todo_item_id}/time_entries.xml` returns all time entries associated with the given todo item, in descending order by date.
* `GET /projects/#{project_id}/time_entries.xml` returns a page full of time entries for the given project, in descending order by date.

For the project time entries request, each page contains up to 50 time entry records. To select a specific page, set the `page` query parameter to 1 or larger. The `X-Records` HTTP header will be set to the total number of time entries in the project, `X-Pages` will be set to the total number of pages, and `X-Page` will be set to the current page.

**Response:**

``` xml
<time-entries type="array">
  <time-entry>
    ...
  </time-entry>
  ...
</time-entries>
```


Create entry
------------

* `POST /projects/#{project_id}/time_entries.xml` creates a new time entry for the given project.
* `POST /todo_items/#{todo_item_id}/time_entries.xml` creates a new time entry for the given todo item.

**Request:**

``` xml
<time-entry>
  <person-id>#{person-id}</person-id>
  <date>#{date}</date>
  <hours>#{hours}</hours>
  <description>#{description}</description>
</time-entry>
```

**Response:**

Returns HTTP status code 201 Created on success, with the Location header set to the URL of the new time entry. The integer ID of the entry may be extracted from that URL.


New entry
---------

* `GET /projects/#{project_id}/time_entries/new.xml` returns a blank “template” XML record for defining a new time entry.

Simply modify the fields accordingly, and submit as described by the `X-Create-Action` HTTP header.

**Response:**

``` xml
<time-entry>
  ...
</time-entry>
```


Get entry
---------

* `GET /time_entries/#{id}.xml` retrieves a single time-entry record, given its integer ID.

**Response:**

``` xml
<time-entry>
  ...
</time-entry>
```


Edit entry
----------

* `GET /time_entries/#{id}/edit.xml` returns the requested time-entry record, but only those fields that may be edited.

Simply modify the fields and submit as described by the `X-Update-Action` HTTP header.

**Response:**

``` xml
<time-entry>
  ...
</time-entry>
```


Update entry
------------

* `PUT /time_entries/#{id}.xml` updates the given time-entry record with the data given.

**Request:**

``` xml
<time-entry>
  <person-id>#{person-id}</person-id>
  <date>#{date}</date>
  <hours>#{hours}</hours>
  <description>#{description}</description>

  <!-- if associated with a todo-item -->
  <todo-item-id>#{todo-item-id}</todo-item-id>
</timeentry>
```

**Response:**

Returns HTTP status code 200 on success.


Destroy entry
-------------

* `DELETE /time_entries/#{id}.xml` destroys the given time entry record.

**Response:**

Returns HTTP status code 200 on success.


Get report
----------

* `GET /time_entries/report.xml` return the set of time entries that match the given criteria.

This action accepts the following query parameters: `from`, `to`, `subject_id`, `todo_item_id`, `filter_project_id`, and `filter_company_id`. Both `from` and `to` should be dates in `YYYYMMDD` format, and can be used to restrict the result to a particular date range. (No more than 6 months’ worth of entries may be returned in a single query, though). The `subject_id` parameter lets you constrain the result to a single person’s time entries. `todo_item_id` restricts the result to only those entries relating to the given todo item. `filter_project_id` restricts the entries to those for the given project, and `filter_company_id` restricts the entries to those for the given company.

**Response:**

``` xml
<time-entries type="array">
  <time-entry>
    ...
  </time-entry>
  ...
</time-entries>
```
