Basecamp Classic API
====================

This is the API for Basecamp Classic (basecamphq.com). Check out the API for the all new Basecamp (basecamp.com) [on GitHub](https://github.com/37signals/bcx-api).

The Basecamp Classic API is implemented as vanilla XML over HTTP using all four verbs (GET/POST/PUT/DELETE). Every resource, like Post, Comment, or TodoList, has their own URL and are manipulated in isolation. We've tried to make the API follow the REST principles as much as we can.


Wrappers and example code
-------------------------

* [Ruby basecamp-wrapper by anibalcucco](https://github.com/anibalcucco/basecamp-wrapper)
* [Python Basecamp Wrapper by Jochen](http://homework.nwsnet.de/products/3cd4_basecamp-wrappera)
* [Python basecampreporting by cmheisel](http://github.com/cmheisel/basecampreporting/)
* [PHP API Wrapper by sirprize](http://github.com/sirprize/basecamp)
* [Java API Wrapper by johndavidjohn](API Wrapper by johndavidjohn)

Wrote your own API wrapper? Feel free to open a pull request and add to this list!


Authentication
--------------

If you're making a private integration with Basecamp Classic for your own purposes, you can use HTTP Basic authentication. This is secure since all requests in the new Basecamp use SSL.

If you're making a public integration with Basecamp Classic for others to enjoy, you must use OAuth 2. This allows users to authorize your application to use Basecamp Classic on their behalf without having to copy/paste API tokens or touch sensitive login info.

Read the [37signals API Authentication Guide](https://github.com/37signals/api/tree/master/sections/authentication.md) for more info on using OAuth.

Your API token can be found by logging into your Basecamp Classic account, clicking on the "My Info" link in the upper-right, and then clicking the "Show your tokens" at the bottom (under "Authentication tokens").


Making a request
---------------

Be sure to set both the 'Content-Type' and 'Accept' headers to 'application/xml' to identify the request and response format. Example with Curl:

    curl -H 'Accept: application/xml' -H 'Content-Type: application/xml' \
      -u hoodlum:up2n0g00d \
      -d '<todo-item><content>...</content></todo-item>' \
    https://url/todo_lists/123/todo_items.xml

API Endpoints
-------------

* [Account](https://github.com/37signals/basecamp-classic-api/blob/master/sections/account.md)
* [Projects](https://github.com/37signals/basecamp-classic-api/blob/master/sections/projects.md)
* [People](https://github.com/37signals/basecamp-classic-api/blob/master/sections/people.md)
* [Companies](https://github.com/37signals/basecamp-classic-api/blob/master/sections/companies.md)
* [Categories](https://github.com/37signals/basecamp-classic-api/blob/master/sections/categories.md)
* [Messages](https://github.com/37signals/basecamp-classic-api/blob/master/sections/messages.md)
* [Comments](https://github.com/37signals/basecamp-classic-api/blob/master/sections/comments.md)
* [Todo Lists](https://github.com/37signals/basecamp-classic-api/blob/master/sections/todo_lists.md)
* [Todo List Items](https://github.com/37signals/basecamp-classic-api/blob/master/sections/todo_list_items.md)
* [Calendar Entries](https://github.com/37signals/basecamp-classic-api/blob/master/sections/calendar_entries.md)
* [Time Tracking](https://github.com/37signals/basecamp-classic-api/blob/master/sections/time_tracking.md)
* [Attachments](https://github.com/37signals/basecamp-classic-api/blob/master/sections/attachments.md)
* [Files](https://github.com/37signals/basecamp-classic-api/blob/master/sections/files.md)

(Hint: Press `t` to enable the file finder and type out the endpoint you need!)

Need a sample of each XML blob will look like? Check out the [Data Reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md).


Responses
---------

If a request succeeds, it will return a status code in the 200 range and often, an XML-formatted response. Note that, in general, if a request causes a new record to be created (like a new message, or to-do item, etc.), the response will use the "201 Created" status. Any other successful operation (like a successful query, delete, or update) will return a 200 status code.


Rate limiting
-------------
You can perform up to 500 requests per 10 second period from the same IP address for the same account. If you exceed this limit, you'll get a 503 response for subsequent requests. Check the Retry-After header to see how many seconds to wait before trying again.


SSL Usage
---------

A non-SSL request made against an account that has SSL enabled (and vice versa) will receive a "302 Found" response. The Location header will contain the correct URI.

If SSL is enabled for your account, ensure that you're using https. If it's not, ensure you're using http.


Documentation Conventions
-------------------------

To make things easier to understand, the following notation is used:

* `#{text}`: Indicates text that should be replaced by your own data
* `...`: Indicates content from the response has been elided for brevity in documentation. See the list of data responses at the end of the page for a full description of the format of that response type.


Help us make it better
----------------------

Please tell us how we can make the API better. If you have a specific feature request or if you found a bug, please use GitHub issues. Fork these docs and send a pull request with improvements.

To talk with us and other developers about the API, subscribe to the [37signals-api mailing list](http://groups.google.com/group/37signals-api).
