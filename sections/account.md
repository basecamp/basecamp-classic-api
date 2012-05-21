Account
=======

`GET /account.xml` returns info about the current Basecamp Classic account, its subscription, and the default post and attachment categories.

This endpoint includes:

* account id and name
* account holder’s person id
* primary company’s id
* whether SSL is enabled
* whether email notification is enabled
* whether time tracking is enabled
* subscription: plan name, maximum number of projects and writeboards, maximum storage in bytes, availability of SSL and time tracking
* last-update timestamp

**Response:**

    <account>
      <id type="integer">1</id>
      <name>Your Company</name>
      <account-holder-id type="integer">1</account-holder-id>
      <primary-company-id type="integer">1</primary-company-id>
      <ssl-enabled type="boolean">true</ssl-enabled>
      <email-notification-enabled type="boolean">true</email-notification-enabled>
      <time-tracking-enabled type="boolean">true</time-tracking-enabled>
      <updated-at type="datetime">2009-10-09T17:52:46Z</updated-atcription>
      <subscription>
        <name>Premium</name>
        <writeboards type="float">Infinity</writeboards>
        <projects type="integer">100</projects>
        <storage type="integer">32212254720</storage>
        <ssl type="boolean">true</ssl>
        <time-tracking type="boolean">true</time-tracking>
      </subscription>
      <default-attachment-categories>
        <category>Documents</category>
        <category>Pictures</category>
        <category>Sounds</category>
      </default-attachment-categories>
      <default-post-categories>
        <category>Design</category>
        <category>Code</category>
        <category>Copywriting</category>
        <category>Transcripts</category>
        <category>Assets</category>
        <category>Miscellaneous</category>
      </default-post-categories>
    </account>
