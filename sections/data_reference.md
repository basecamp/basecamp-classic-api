Data Reference
==============

Account
-------

``` xml
<account>
  <id type="integer">1</id>
  <name>Your Company</name>
  <account-holder-id type="integer">1</account-holder-id>
  <ssl-enabled type="boolean">true</ssl-enabled>
  <email-notification-enabled type="boolean">true</email-notification-enabled>
  <time-tracking-enabled type="boolean">true</time-tracking-enabled>
  <updated-at type="datetime">2009-10-09T17:52:46Z</updated-at>
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
```

Attachment
----------

``` xml
<attachment>
  <id type="integer">#{id}</id>
  <name>#{name}</name>
  <description>#{description}</description>
  <byte-size type="integer">#{byte_size}</byte-size>
  <download-url>#{download_url}</download-url>

  <project-id type="integer">#{project_id}</project-id>
  <category-id type="integer">#{category_id}</category-id>
  <person-id type="integer">#{person_id}</person-id>
  <private type="boolean">#{private}</private>
  <created-on type="datetime">#{created_on}</created-on>

  <!-- if the attachment belongs to a message or comment -->
  <owner-id type="integer">#{owner_id}</owner-id>
  <owner-type>#{owner_type}</owner-type>

  <!-- for attachments with multiple versions, collection specifies
    the id of the "parent" attachment (version 1), and current will
    be true for the most recent version -->
  <collection type="integer">#{collection}</collection>
  <version type="integer">#{version}</version>
  <current type="boolean">#{current}</current>
</attachment>
```

Calendar entry
--------------

``` xml
<calendar-entry>
  <id type="integer">#{id}</id>
  <title>#{title}</title>
  <type>#{Milestone|CalendarEvent}</type>
  <start-at type="date">#{start_at}</start-at>
  <deadline type="{date|datetime}">#{deadline}</deadline>
  <project-id type="integer">#{project_id}</project-id>
  <created-on type="datetime">#{created_on}</created-on>
  <creator-id type="integer">#{creator_id}</creator-id>
  <creator-name>#{creator_name}</creator-name>
  <commented-at type="datetime">#{commented_at}</commented-at>
  <comments-count type="integer">#{comments_count}</comments-count>

  <!-- if the entry is a milestone -->
  <completed type="boolean">#{true|false}</completed>
  <responsible-party-id type="integer">#{responsible_party_id}</responsible-party-id>
  <responsible-party-type>#{responsible_party_type}</responsible-party-type>
  <responsible-party-name>#{responsible_party_name}</responsible-party-name>

  <!-- if the milestone has been completed -->
  <completed-on type="datetime">#{completed_on}</completed-on>
  <completer-id type="integer">#{completer_id}</completer-id>
  <completer-name>#{completer_name}</completer-name>
</calendar-entry>
```

Category
--------

``` xml
<category>
  <id type="integer">#{id}</id>
  <name>#{name}</name>
  <project-id type="integer">#{project_id}</project-id>
  <elements-count type="integer">#{elements_count}</elements-count>
  <type>#{type}</type>
</category>
```

Comment
-------

``` xml
<comment>
  <id type="integer">#{id}</id>
  <author-id type="integer">#{author_id}</author-id>
  <author-name>#{author_name}</author-name>
  <commentable-id type="integer">#{commentable_id}</commentable-id>
  <commentable-type>#{commentable_type}</commentable-type>
  <body>#{body}</body>
  <emailed-from nil="true">#{emailed_from}</emailed-from>
  <created-at type="datetime">#{created_at}</created-at>

  <attachments-count type="integer">#{attachments_count}</attachments-count>
  <attachments type="array">
    <attachment>
      ...
    </attachment>
    ...
  </attachments>
</comment>
```

Company
-------

``` xml
<company>
  <id type="integer">#{id}</id>
  <name>#{name}</name>
  <address-one>#{address_one}</address-one>
  <address-two>#{address_two}</address-two>
  <city>#{city}</city>
  <state>#{state}</state>
  <zip>#{zip}</zip>
  <country>#{country}</country>
  <web-address>#{web_address}</web-address>
  <phone-number-office>#{phone_number_office></phone-number-office>
  <phone-number-fax>#{phone_number_fax}</phone-number-fax>
  <time-zone-id>#{time_zone_id}</time-zone-id>
  <can-see-private type="boolean">#{can_see_private}</can-see-private>

  <!-- for non-client companies -->
  <url-name>#{url_name}</url-name>
</company>
```

Milestone
---------

``` xml
<milestone>
  <id type="integer">#{id}</id>
  <title>#{title}</title>
  <deadline type="date">#{deadline}</deadline>
  <completed type="boolean">#{true|false}</completed>
  <project-id type="integer">#{project_id}</project-id>
  <created-on type="datetime">#{created_on}</created-on>
  <creator-id type="integer">#{creator_id}</creator-id>
  <creator-name>#{creator_name}</creator-name>
  <responsible-party-id type="integer">#{responsible_party_id}</responsible-party-id>
  <responsible-party-type>#{responsible_party_type}</responsible-party-type>
  <responsible-party-name>#{responsible_party_name}</responsible-party-name>
  <commented-at type="datetime">#{commented_at}</commented-at>
  <comments-count type="integer">#{comments_count}</comments-count>

  <!-- if the milestone has been completed -->
  <completed-at type="datetime">#{completed_at}</completed-at>
  <completer-id type="integer">#{completer_id}</completer-id>
  <completer-name>#{completer_name}</completer-name>
</milestone>
```

Person
------

``` xml
<person>
  <id type="integer">#{id}</id>
  <first-name>#{first_name}</first-name>
  <last-name>#{last_name}</last-name>
  <title>#{title}</title>
  <email-address>#{email_address}</email-address>
  <im-handle>#{im_handle}</im-handle>
  <im-service>#{im_service}</im-service>
  <phone-number-office>#{phone_number_office}</phone-number-office>
  <phone-number-office-ext>#{phone_number_office_ext}</phone-number-office-ext>
  <phone-number-mobile>#{phone_number_mobile}</phone-number-mobile>
  <phone-number-home>#{phone_number_home}</phone-number-home>
  <phone-number-fax>#{phone_number_fax}</phone-number-fax>
  <company-id type="integer">#{company_id}</company-id>
  <client-id type="integer">#{client_id}</client-id>
  <time-zone-name>#{time_zone_name}</time-zone-name>

  <avatar-url>#{avatar_url}</avatar-url>

  <!-- if user is an administrator, or is self -->
  <user-name>#{user_name}</user-name>

  <!-- if user is an administrator -->
  <administrator type="boolean">#{administrator}</administrator>
  <deleted type="boolean">#{deleted}</deleted>
  <has-access-to-new-projects type="boolean">#{has_access_to_new_projects}</has-access-to-new-projects>
</person>
```

Post
----

``` xml
<post>
  <id type="integer">#{id}</id>
  <title>#{title}</title>
  <body>#{body}</body>
  <display-body>#{display_body}</display-body>
  <posted-on type="datetime">#{posted_on}</posted-on>
  <commented-at type="datetime">#{commented_at}</commented-at>
  <project-id type="integer">#{project_id}</project-id>
  <category-id type="integer">#{category_id}</category-id>
  <author-id type="integer">#{author_id}</author-id>
  <author-name>#{author_name}</author-name>
  <milestone-id type="integer">#{milestone_id}</milestone-id>
  <comments-count type="integer">#{comments_count}</comments-count>
  <use-textile type="boolean">#{use_textile}</use-textile>
  <extended-body deprecated="true">#{extended_body}</extended-body>
  <display-extended-body deprecated="true">#{display_extended_body}</display-extended-body>

  <attachments-count type="integer">#{attachments_count}</attachments-count>
  <attachments type="array">
    <attachment>
      ...
    </attachment>
    ...
  </attachments>

  <!-- if user can see private posts -->
  <private type="boolean">#{private}</private>
</post>
```

Post (Abbreviated)
------------------

``` xml
<post>
  <id type="integer">#{id}</id>
  <title>#{title}</title>
  <author-name>#{author_name}</author-name>
  <posted-on type="datetime">#{posted_on}</posted-on>
  <commented-at type="datetime">#{commented_at}</commented-at>
  <attachments-count type="integer">#{attachments_count}</attachments-count>
  <category>
    <id type="integer">#{id}</id>
    <name>#{name}</name>
  </category>
</post>
```

Project
-------

``` xml
<project>
  <id type="integer">#{id}</id>
  <name>#{name}</name>
  <created-on type="datetime">#{created_on}</created-on>
  <status>#{status}</status>
  <last-changed-on type="datetime">#{last_changed_on}</last-changed-on>
  <company>
    <id type="integer">#{id}</id>
    <name>#{name}</name>
  </company>

  <!-- if user is administrator, or show_announcement is true -->
  <announcement>#{announcement}</announcement>

  <!-- if user is administrator -->
  <start-page>#{start_page}</start-page>
  <show-writeboards type="boolean">#{show_writeboards}</show-writeboards>
  <show-announcement type="boolean">#{show_announcement}</show-announcement>
</project>
```

Subscription
------------

``` xml
<subscription>
  <name>Premium</name>
  <writeboards type="float">Infinity</writeboards>
  <projects type="integer">100</projects>
  <storage type="integer">32212254720</storage>
  <ssl type="boolean">true</ssl>
  <time-tracking type="boolean">true</time-tracking>
</subscription>
```

Time entry
----------

``` xml
<time-entry>
  <id type="integer">#{id}</id>
  <project-id type="integer">#{project_id}</project-id>
  <person-id type="integer">#{person_id}</person-id>
  <person-name>#{person_name}</person-name>
  <date type="date">#{date}</date>
  <hours>#{hours}</hours>
  <description>#{description}</description>
  <todo-item-id type="integer">#{todo_item_id}</todo-item-id>
</time-entry>
```

Todo item
---------

``` xml
<todo-item>
  <id type="integer">#{id}</id>
  <todo-list-id type="integer">#{todo_list_id}</todo-list-id>
  <content>#{content}</content>
  <position type="integer">#{position}</position>
  <created-on type="datetime">#{created_on}</created-on>
  <creator-id type="integer">#{creator_id}</creator-id>
  <creator-name>#{creator_name}</creator-name>
  <completed type="boolean">#{completed}</completed>
  <updated-at type="datetime">#{updated_at}</updated-at>
  <commented-at type="datetime">#{commented_at}</commented-at>
  <comments-count type="integer">#{comments_count}</comments-count>

  <!-- if the item has a due date (in the company time zone) -->
  <due-at type="datetime">#{due_at}</due-at>

  <!-- if the item has a responsible party -->
  <responsible-party-type>#{responsible_party_type}</responsible-party-type>
  <responsible-party-id type="integer">#{responsible_party_id}</responsible-party-id>
  <responsible-party-name>#{responsible_party_name}</responsible-party-name>

  <!-- if the item has been completed -->
  <completed-at type="datetime">#{completed_at}</completed-at>
  <completer-id type="integer">#{completer_id}</completer-id>
  <completer-name>#{completer_name}</completer-name>
</todo-item>
```

Todo list
---------

``` xml
<todo-list>
  <id type="integer">#{id}</id>
  <name>#{name}</name>
  <description>#{description}</description>
  <project-id type="integer">#{project_id}</project-id>
  <milestone-id type="integer">#{milestone_id}</milestone-id>
  <position type="integer">#{position}</position>
  <completed type="boolean">#{completed}</completed>

  <!-- if user can see private lists -->
  <private type="boolean">#{private}</private>

  <!-- if the account supports time tracking -->
  <tracked type="boolean">#{tracked}</tracked>

  <!-- if todo-items are included in the response -->
  <todo-items type="array">
    <todo-item>
      ...
    </todo-item>
    <todo-item>
      ...
    </todo-item>
    ...
  </todo-items>
</todo-list>
```
