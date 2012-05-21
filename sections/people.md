People
======

Current person
--------------

* `GET /me.xml` returns the currently logged in person (you).

**Response:**

``` xml
<person>
  <id type="integer">#{id}</id>
  <user-name>#{user_name}</user-name>
  ...
</person>
```


Get people (across projects)
----------------------------

Admins can include deleted people using the `?include_deleted=true` query parameter.

* `GET /people.xml` returns all people visible to (and including) the requesting user.
* `GET /projects/#{project_id}/people.xml` returns all people with access to the given project.
* `GET /companies/#{company_id}/people.xml` returns all people from the given company that are visible to the requesting user.

**Response:**

``` xml
<people>
  <person>
    ...
  </person>
  ...
</people>
```


Get person
----------

* `GET /people/#{person_id}.xml` returns a single person identified by their integer ID.

**Response:**

``` xml
<person>
  ...
</person>
```
