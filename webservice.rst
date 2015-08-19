Webservice for Physiome Repository
==================================

Overview
--------

This document describes how the webservices are provided by the
Physiome Repository.  Generally, using the webservice is simply
providing the ``Accept`` header to any URL within the instance.

Current Version
---------------

The webservice communicates using JSON, and by default sending the
header ``Accept: application/json`` to resource endpoints that support
this protocol will return the requested content as JSON.  However, it is
highly encouraged that consumers provide version specific header, in
this case it will be::

    Accept: application/vnd.physiome.pmr2.json.1

In other words, there are no dedicated API servers or alternative URLs
to access resources within the Physiome Repository as a webservice.
Clients have to negotiate the intended content type they desire to
consume through the usage of this ``Accept`` header.

Schema
------

All data are communicated using the `Collection\+JSON`_ hypermedia type.
Please refer to the specification as to how this might be used.  As this
standard is designed as a proper hypermedia type a browser that sends
and interpret Collection+JSON can be used to navigate the repository
much like how an end-user might navigate the repository with their web
browser.  One such example is through the `Collection\+JSON Browser`_
with the root endpoint of the repository (however, the example link uses
the URL to the welcome page as the browser does not support redirection
to that on its own).

.. _Collection\+JSON: http://amundsen.com/media-types/collection/
.. _Collection\+JSON Browser: http://collection-json-browser.herokuapp.com/
  ?proxy&uri=http:%2F%2Fstaging.physiomeproject.org%2Fwelcome

However, as implemented the restricted views are not necessarily readily
available by those links, which PMR2 implements an alternative end point
specific for this purpose.  The `PMR2 Dashboard`_ was created for this
purpose but in the future it may be linked directly to the root end
point of the repository.

.. _PMR2 Dashboard: http://collection-json-browser.herokuapp.com/
  ?proxy&uri=http:%2F%2Fstaging.physiomeproject.org%2Fpmr2-dashboard

Authentication
--------------

For third-party applications that are interested in accessing private
content belonging to its users, Physiome Repository supports the use
`OAuth`_ for client authentication.  Applications must be registered
manually by the system administrators.  An example demo application
(using the previous version of the JSON-based protocol) is provided by
the package `pmr2.client`_.

.. _pmr2.client: https://github.com/PMR2/pmr2.client/
.. _Oauth: http://tools.ietf.org/html/rfc5849
