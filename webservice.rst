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

Schema/Payload format
---------------------

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

Example
-------

Generally, all end points that can be accessible by a web browser should
also be accessible by the web service.  For instance, loading the front
page of the official repository can be done like so, using ``curl`` with
the follow location flag (``-L``)::

    $ curl -sL -H 'Accept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/ |python -m json.tool

The result of the above command should show something like so::

    {
        "collection": {
            "href": "https://staging.physiomeproject.org/welcome/document_view",
            "items": [
                {
                    "data": [
                        {
                            "name": "contents",
                            ...
                        }
                    ],
                }
            ],
            "links": [
                {
                    "href": "https://staging.physiomeproject.org/exposure",
                    "prompt": "Main model listing",
                    "rel": "bookmark"
                },
                ...
            ]
        }
    }

Your client can simply follow the ``href`` inside any of the sections,
especially the ``links`` section, for the links with a ``bookmark``
relationship.  For instance::

    $ curl -sL -H 'Accept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/exposure |python -m json.tool

Output may look something like::

    {
        "collection": {
            "href": "https://staging.physiomeproject.org/exposure/listing/pmr1_folder_listing",
            "links": [
                {
                    "href": "https://staging.physiomeproject.org/e/105",
                    "prompt": "\r\n      A Quantitative Model of Human Jejunal Smooth Muscle Cell Electrophysiology\r\n    ",
                    "rel": "bookmark"
                },
                ...
            ]
        }
    }

An exposure may look like so::

    $ curl -sL -H 'Accept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/e/c1 |python -m json.tool
    {
        "collection": {
            "href": "https://staging.physiomeproject.org/e/c1/exposure_info",
            "links": [
                {
                    "href": "https://staging.physiomeproject.org/e/c1/beeler_reuter_1977.cellml/view",
                    "prompt": "Reconstruction of the action potential of ventricular myocardial fibres",
                    "rel": "bookmark"
                },
                {
                    "href": "https://staging.physiomeproject.org/workspace/beeler_reuter_1977",
                    "prompt": "Workspace URL",
                    "rel": "via"
                }
            ],
            "version": "1.0"
        }
    }

Note that there are two links, one of them containing a link to the
object inside (TODO: note that v2 will change this to items), and also
a ``"rel": "via"`` highlighting the fact that this link is derived from
the associated ``href``, in this case it would be the source workspace
URL.  Many other details within the repository can be gathered by
progressively navigating through these links.

One thing that is currently not linked is the search form, which users
of the site through the web browser will find on the upper-right hand
corner as a search bar.  This function is also replicated by navigating
directly to that link::

    $ curl -sL -H 'Accept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/search |python -m json.tool

The result will be a template that looks like this::

    {
        "collection": {
            "href": "https://staging.physiomeproject.org/search",
            "template": [
                {
                    "name": "SearchableText",
                    "prompt": "SearchableText",
                    "value": ""
                },
                {
                    "name": "Title",
                    "prompt": "Title",
                    "value": ""
                },
                {
                    "name": "Description",
                    "prompt": "Description",
                    "value": ""
                },
                {
                    "name": "Subject",
                    "options": [
                        {
                            "value": "CellML Model"
                        },
                        {
                            "value": "FieldML Model"
                        }
                    ],
                    "prompt": "Subject",
                    "value": ""
                },
                {
                    "name": "portal_type",
                    "options": [
                        {
                            "value": "Exposure"
                        },
                        ...
                    ],
                    "prompt": "portal_type",
                    "value": ""
                }
            ],
            "version": "1.0"
        }
    }

Submission is done using the Collection+JSON format also.  For example::

    $ curl -sL -H 'Accept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/search -d '{
    >         "template": {"data": [
    >             {"name": "SearchableText", "value": "Beeler"}
    >         ]}
    >     }' | python -mjson.tool

Results will be contained in the ``links`` section::

    {
        "collection": {
            "href": "https://staging.physiomeproject.org/search",
            "links": [
                {
                    "href": "https://staging.physiomeproject.org/exposure/8123cbe00754b718a39fed5eb9bfb4a2/skouibine_trayanova_moore_1999.cellml/view",
                    "prompt": "Anode/cathode make and break phenomena in a model of defibrillation",
                    "rel": "bookmark"
                },
                {
                    "href": "https://staging.physiomeproject.org/w/miller/beeler_reuter_1977_uncertexample",
                    "prompt": "Beeler, Reuter, 1977",
                    "rel": "bookmark"
                },
                ...
            ]
        }
    }

This does the same raw text-based search, however with this service it
is possible to make use of the other fields to further refine the
results by using them, for example, to search for only workspaces with
``Beeler`` in its title::

    $ curl -sL -H 'Aecept: application/vnd.physiome.pmr2.json.1' \
    >     https://staging.physiomeproject.org/search -d '{
    >         "template": {"data": [
    >             {"name": "Title", "value": "Beeler"},
    >             {"name": "portal_type", "value": "Workspace"}
    >         ]}
    >     }' | python -mjson.tool

Results sould look like so::

    {
        "collection": {
            "href": "https://staging.physiomeproject.org/search",
            "links": [
                {
                    "href": "https://staging.physiomeproject.org/w/miller/beeler_reuter_1977_uncertexample",
                    "prompt": "Beeler, Reuter, 1977",
                    "rel": "bookmark"
                },
                {
                    "href": "https://staging.physiomeproject.org/w/tommy/my_beeler_model",
                    "prompt": "My Beeler Model",
                    "rel": "bookmark"
                },
                {
                    "href": "https://staging.physiomeproject.org/workspace/beeler_reuter_1977",
                    "prompt": "Beeler, Reuter, 1977",
                    "rel": "bookmark"
                },
                ...
            ]
        }
    }

Note how the results is much more specific.  For all othe searches and
forms/endpoints that display a ``template`` section, you can follow the
standard as such to submit data.  This includes authenticated forms that
one can access after being granted write-access through OAuth and such
to create workspaces and exposures.
