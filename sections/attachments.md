Attachments
===========

For accessing files on a given project, please see the [Files API](https://github.com/37signals/basecamp-classic-api/blob/master/sections/files.md).

Attaching files via the API
---------------------------

Some operations, like creating messages or comments, or updating existing messages or comments, allow you to attach a file to the record. To do this via the API, you need to send a POST request to the `/upload` URI, with the HTTP Accept header set to `application/xml`. The body of the request should be the content of the file you want to attach:

    POST /upload HTTP/1.0
    Accept: application/xml
    Content-Type: application/octet-stream
    Content-Length: 23123

    ... (file contents go here)

If the upload succeeds, you'll get an XML response back, telling you the ID of your upload. (Your upload is not yet associated with any record, and if you do not do anything with it, it will be deleted sometime within the next 30 minutes.)

    HTTP/1.0 201 OK
    Content-Type: application/xml

    <?xml version="1.0" encoding="UTF-8"?>
    <upload><id>441b2cec.eve.21267</id></upload>

Armed with the ID, your next step is to attach the file to a record. Using the "Create message" action, for instance, you pass an array of attachment data in. Assuming you had two files you wanted to attach (which you had previously uploaded, as described), your attachment data would look something like this (formatted as XML):

``` xml
<attachments>
  <name>A pretty sunset</name>
  <file>
    <file>441b2cec.eve.21267</file>
    <content-type>image/jpg</content-type>
    <original-filename>sunset.jpg</original-filename>
  </file>
</attachments>
<attachments>
  <name>The ocean</name>
  <file>
    <file>441b2fff.log.21285</file>
    <content-type>image/png</content-type>
    <original-filename>ocean.png</original-filename>
  </file>
</attachments>
```
