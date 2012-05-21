Messages
========

Note: that the Messages API names its resource "posts" (not "messages").

Get messages
------------

* `GET /projects/#{project_id}/posts.xml` returns the 25 most recent messages in the given project.
* `GET /projects/#{project_id}/cat/#{category_id}/posts.xml` returns the most 25 most recent messages in the given project for the given category.

**Response:**

    <posts>
      <post>
        ...
      </post>
      ...
    </posts>


Get message
-----------

* `GET /posts/#{id}.xml` returns a single message record identified by its integer ID.

**Response:**

    <post>
      ...
    </post>


Get archived messages
---------------------

* `GET /projects/#{project_id}/posts/archive.xml` returns a summary record for each message in the given project.
* `GET /projects/#{project_id}/cat/#{category_id}/posts/archive.xml` returns a summary record for each message in the given project for the given category.

Note: that a summary record includes only a few bits of information about a message, not the complete record.

**Response:**

    <posts>
      <post>
        ... <!-- abbreviated post -->
      </post>
      <post>
        ... <!-- abbreviated post -->
      </post>
      ...
    </posts>


New message
-----------

* `GET /projects/#{project_id}/posts/new.xml` returns a blank XML “template” for a single message record, indicating which fields may be submitted to create a new message. 

This endpoint will also return a custom HTTP header, `X-Create-Action` indicating where and how the data may be submitted.

**Response:**

    <post>
      ...
    </post>


Create message
--------------

* `POST /projects/#{project_id}/posts.xml` creates a new message, optionally sending notifications to a selected list of people.

Note: you can also upload files using this function, but you need to upload the files first and then attach them.

**Request:**

    <request>
      <post>
        <category-id>#{category_id}</category-id>
        <title>#{title}</title>
        <body>#{body}</body>
        <private>1</private> <!-- only for firm employees -->
      </post>
      <notify>#{person_id}</notify>
      <notify>#{person_id}</notify>
      ...
      <attachments>
        <name>#{name}</name> <!-- optional -->
        <file>
          <file>#{temp_id}</file> <!-- the id of the previously uploaded file -->
          <content-type>#{content_type}</content-type>
          <original-filename>#{original_filename}</original-filename>
        </file>
      </attachments>
      <attachments>...</attachments>
      ...
    </request>

**Response:**

Returns HTTP status code 201 Created on success, with the Location header set to the “Get message” URL for the new message. The new message ID can be extracted from that URL. On failure, a non-200 status code will be returned, possibly with error information in XML format as the response’s content.

Edit message
------------

* `GET /posts/#{id}/edit.xml` returns an XML “template” for a single message record, prefilled with the existing values for that record, and ready to be resubmitted via the “update message” action. 

This endpoint will also return a custom HTTP header, `X-Update-Action` indicating where and how the data may be submitted.

**Response:**

    <post>
      ...
    </post>


Update message
--------------

* `PUT /posts/#{id}.xml` updates an existing message, optionally sending notifications to a selected list of people.

Note: you can also upload files using this function, but you need to upload the files first and then attach them.

**Request:**

    <request>
      <post>
        <category-id>#{category_id}</category-id>
        <title>#{title}</title>
        <body>#{body}</body>
        <private>1</private> <!-- only for firm employees -->
        <notify-about-changes>1</notify-about-changes>
      </post>
      <notify>#{person_id}</notify>
      <notify>#{person_id}</notify>
      ...
    </request>

**Response:**

Returns HTTP status code 200 on success, or any other code (and possibly error information in XML format) on error.


Destroy message
---------------

* `DELETE /posts/#{id}.xml` destroys the given message and all of its associated comments.

Returns HTTP status code 200 on success.
