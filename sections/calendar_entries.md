Calendar Entries
================

Please refer to the data reference for a full XML representation of [calendar entries](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#calendar_entry) or [milestones](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#milestone).

Get all calendar entries
------------------------

* `GET /projects/#{project_id}/calendar_entries.xml` returns a page of calendar entries for the given project, ordered by due date.

Each page contains up to 50 time entry records. To select a different page of data, set the “page” query parameter to a value greater than zero.

**Response:**

``` xml
<calendar-entries>
  <calendar-entry>
    ...
  </calendar-entry>
  <calendar-entry>
    ...
  </calendar-entry>
  ...
</calendar-entries>
```


Get all milestones
------------------

* `GET /projects/#{project_id}/calendar_entries/milestones.xml` returns a list of milestones for the given project.

This endpoint can return all milestones, or only those that are late, completed, or upcoming.

**Request:**

``` xml
<request>
  <!-- optional, defaults to all -->
  <find>#{all|late|completed|upcoming}</find>
</request>
```

**Response:**

``` xml
<calendar-entries>
  <calendar-entry>
    ...
  </calendar-entry>
  <calendar-entry>
    ...
  </calendar-entry>
  ...
</calendar-entries>
```


Get all calendar events
-----------------------

* `GET /projects/#{project_id}/calendar_entries/calendar_events.xml` returns a page of calendar events for the given project, ordered by due date.

Each page contains up to 50 time entry records. To select a different page of data, set the `page` query parameter to a value greater than zero.

**Response:**

``` xml
<calendar-entries>
  <calendar-entry>
    ...
  </calendar-entry>
  <calendar-entry>
    ...
  </calendar-entry>
  ...
</calendar-entries>
```


Create calendar entry
---------------------

* `POST /projects/#{project_id}/calendar_entries.xml` creates a new calendar entry.

To make the entry a milestone, set `type` to `Milestone`. To make a company responsible for the milestone, prefix the company id with a `c`.

**Request:**

``` xml
<request>
  <calendar-entry>
    <title>#{title}</title>
    <start-at type="date">#{start_at}</start-at>
    <deadline type="{date|datetime}">#{deadline}</deadline>
    <type>#{Milestone|CalendarEvent}</type>
    <!-- Only applicable to milestones -->
    <responsible-party>#{id}</responsible-party>
  </calendar-entry>
</request>
```

**Response:**

``` xml
<calendar-entry>
  ...
</calendar-entry>
```


Update calendar entry
---------------------

* `PUT /projects/#{project_id}/calendar_entries/#{id}.xml` modifies a calendar entry.

Supplying a different value for `type` can convert a calendar event to a milestone and vice versa. You can use this to shift the deadline of a single milestone, and optionally shift the deadlines of subsequent milestones as well.

**Request:**

``` xml
<request>
  <calendar-entry>
    <title>#{title}</title>
    <deadline>#{deadline}</deadline>
    ....
  </calendar-entry>
  <!-- Only applicable to milestones -->
  <move-upcoming-milestones>#{true|false}</move-upcoming-milestones>
  <move-upcoming-milestones-off-weekends>#{true|false}</move-upcoming-milestones-off-weekends>
</request>
```

**Response:**

``` xml
<calendar-entry>
  ...
</calendar-entry>
```

Get calendar entry
------------------

* `GET /projects/#{project_id}/calendar_entries/#{id}.xml` returns a calendar entry identified by the given ID.

**Response:**

``` xml
<calendar-entry>
  ...
</calendar-entry>
```


Destroy calendar entry
----------------------

* `DELETE /projects/#{project_id}/calendar_entries/#{id}.xml` deletes a calendar entry from the project.

**Response:**

Returns HTTP status code 200 on success.


Complete calendar entry
-----------------------

* `PUT /projects/#{project_id}/calendar_entries/#{id}/complete.xml` marks the specified milestone as complete.

**Response:**

``` xml
<calendar-entry>
  ...
</calendar-entry>
```


Uncomplete calendar entry
-------------------------

* `PUT /projects/#{project_id}/calendar_entries/#{id}/uncomplete.xml` marks the specified milestone as uncomplete.

**Response:**

``` xml
<calendar-entry>
  ...
</calendar-entry>
``` xml
