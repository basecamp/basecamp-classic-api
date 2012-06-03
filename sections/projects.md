Projects
========

For the full XML representation of projects, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#project).

Get projects
------------

* `GET /projects.xml` returns all accessible projects. This includes active, inactive, and archived projects.

**Response:**

``` xml
<projects>
  <project>
    ...
  </project>
  <project>
    ...
  </project>
  ...
</projects>

```


Get project
-----------

* `GET /projects/#{project_id}.xml` returns a single project identified by its integer ID

**Response:**

``` xml
<project>
  <name>Design Review</name>
  ...
  <company>
    <name>Globex Corporation</name>
    ...
  </company>
</project>

```


Create project
--------------

* `POST /projects.xml` creates a new project with the given name.

**Request:**

``` xml
<request>
  <project>
    <name>Shopping Cart Redesign</name>
  </project>
</request>
```


**Response:**

Returns status code 201 (Created) on success with the Location header set to the URL for the new project. You can extract the ID of the project from the URL. Failed requests will receive a 422 (Unprocessable Entity) or 500 (Server Error) status code in the response.


Update project
--------------

* `PUT /projects/#{project_id}.xml` updates attributes of the given project. 

Only administrative users may update project records. You only need to provide the attributes you wish to update; others ought to be omitted from the request.

**Request:**

``` xml
<project>
  <name type="string">Shopping Cart Redesign</name>
  <start-page type="string">log|all|todos|milestones|files</start-page>
  <status>active|on_hold|archived</status>
  <company-id>#{client-id}</company-id>
  <show-writeboards>true|false</show-writeboards>
  <announcement>...</announcement>
  <show-announcement>true|false</show-announcement>
</project>
```


**Response:**

Returns 200 OK on success. Otherwise, returns an error code (e.g. 422 or 403), possibly including a payload describing the error.


Project counts
--------------

* `GET /projects/count.xml` returns a count of all projects, by project status.

If there are no projects with a particular status, that status entry will be omitted from the report.

**Response:**

``` xml
<count>
  <active type="integer">5</active>
  <on-hold type="integer">2</active>
  <archived type="integer">11</active>
</count>
```
