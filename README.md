# Linkback

Linkback for Drupal 8, a rebuilt version of Vinculum.

This module is the backend to store received linkbacks and to fire Events to
be used by Rules or by handler modules. So without these modules it's not
very useful. 

## Install Linkback

Install like a normal module.

Go to Configure > Services > Linkbacks. From there you can
configure how sending linkbacks must work: if using cron or if using manual
process.

Already "registered" (i.e. saved, or created entities) linkbacks are controlled in a tab
in Content, at /admin/content/linkback . This includes both incoming and 
outgoing linkbacks.

### Configure content types to send and receive linkbacks

To activate Linkback functions you must add at least one field of type 
"Linkback handlers" to a node content type. 

If you keep the suggested default settings of "Send linkbacks" and
"Receive linkbacks" to true, nodes of these types will use each type of
linkback handler module that has been enabled.

* Known issue: [Two linkback handler fields of different names don't work](https://www.drupal.org/node/2847867)
 

## Changes from Vinculum in Drupal 7

Some substantial changes over how [Vinculum](https://drupal.org/project/vinculum) in Drupal 7 worked:
Changes:
  - Received and sent linkbacks are now an Entity called Linkback, so this module
    uses base interfaces such as the EntityListBuilder, the EntityViewsData
    to create custom views, and generally all the Entity API.
  - Linkback availability on each content type is enabled via Entity field. 
    So it can be configured generally via default field settings or on each
    bundle.
  - Trackbacks not implemented.
  - Validation of received linkbacks done in entity scope, so using new
    validation API (using Symfony constraints).
  - Crawling jobs using Symfony DomCrawler in Drupal 8 core.
  - Web spider curling jobs using guzzle library in Drupal 8 core.
  - Using Symfony EventDispatcher / EventSubcriber instead of hooks.
  
  What is not developed:
  - Allow altering source url and target when sending refbacks (
    hook_linkback_link_send ).
  - Check if linkback has been sent previously (always sends refback if
    sending is enabled).
  - Handler modules are not configured via general settings, simply enabling
    linkback handling modules. (Maybe it's better to plan enabled handlers to
    be configured in field settings).

## Development notes
 - [Issue queue](https://www.drupal.org/project/issues/linkback)
 - [Vinculum D8 planning notes](https://www.drupal.org/node/2687129)
 - You can see a working handler module in [linkback-d8-pingback]( https://github.com/aleixq/vinculum-d8_pingback ).
 - [Pingback development issue](https://www.drupal.org/node/2846844)
 - [Webmention development issue](https://www.drupal.org/node/2846789)