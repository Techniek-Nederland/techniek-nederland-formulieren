Retrieving Installation Information
-----------------------------------

This guide will walk you through the process of accessing various details, including the name, serial number,
power rating, safety instructions, and any additional remarks related to the installations and its maintenance.
This tutorial aims to provide a comprehensive understanding of how to retrieve product information using
the FGO webservice. It covers the following key topics:

.. contents::
   :depth: 2
   :local:
   :backlinks: none


Before diving into the tutorial, ensure that you have the necessary credentials and access to the FGO webservice.
Familiarize yourself with the authentication process, as mentioned in the
documentation page on :ref:`tutorials/authentication/index:authentication`.

It is also helpful to have a basic understanding of web services and how they function. This will enable you to follow
along with the tutorial more effectively. For an example of how to configure Postman, see
:ref:`tutorials/authentication/user_data_retrieval:User Data Retrieval`

And last but not least: have a look at the Swagger documentation available at https://api.fgoplus.nl/swagger/.

Querying Products
=================

The first step in retrieving product information from the FGO webservice is to search the catalog using specific
product names or properties (Type, Brand, model etc).


Please ensure that you include the mandatory parameters in your requests to effectively search and retrieve the desired product information.
Some of the query parameters have been omitted in this tutorial, check the `Swagger <https://api.fgoplus.nl/swagger/index.html>`_ for
an extensive list.


.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Product/Search

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Access token provided by IDP
    :query SearchString: *(Required)* Represents the search term or keyword you want to use to filter the products. For a complete list without any filtering, use the value *
    :query Size: *(Required)* The number of results you want to retrieve per page
    :query From: The offset from which the results should begin. It is used for navigating through the paginated results.

    **Example request**

    We are searching for products with the term "boiler," requesting 10 results per page, and starting from the first result (offset 0).


    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Search?SearchString=boiler&Size=10&From=0 HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>

    **Example response**

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        {
            "items": [
                {
                    "publish": true,
                    "id": 38610,
                    "shortDescription": "Documentation Boiler",
                    "manufacturerGln": "123456789",
                    "manufacturerName": "Fluxility",
                    "productCode": "12345678",
                    "gtin": "987654321",
                    "brand": "Fluxility",
                    "model": "X-class",
                    "version": "FLX-100",
                    "category": "CV-toestellen",
                    "etimClass": {
                        "code": "EC010231",
                        "description": "Boiler Direct Gestookt"
                    },
                    "status": {
                        "code": "94E",
                        "description": "Uitlopend"
                    },
                    "changeDate": "2023-06-07T12:00:00.000+00:00",
                    "startDate": "1989-03-06T00:00:00+00:00",
                    "isDeleted": false,
                    "isDummy": true,
                    "hasImage": true,
                    "recordCreateDate": "1989-03-06T00:00:00+00:00"
                }
            ],
            "took": 20,
            "total": 1
        }


The response is a JSON object with a property 'total'. The property 'took' is the time it took and can be ignored. The
property `items` is an array of search results. We list the most relevant properties.

:shortDescription:      The human readable (en bekend in martk) name of the product
:manufacturerName:      The Manufacturer
:brand:                 The Brand
:model:                 The Model
:version:               The Version
:id:                    Identifier; ID within the FGO Database
:productCode:           Identifier; ID within the Manufacturers own systems
:manufacturerGln:       Identifier of the manufacturer. Combination of `manufacturerGln` and `productCode` is unique
:gtin:                  Identifier; `Global Trade Item Number <https://www.gs1.org/standards/id-keys/gtin>`_
:etimClass:             The classification of the product using `ETIM <https://www.etim-international.com/>`_


Retrieving available filters and their options
==============================================
In addition to free-text searching, the FGO webservice also provides the capability to filter results based
on specific properties. This feature, known as faceted search, allows you to refine your search results further
based on various criteria. Before you can filter the product search, we have to retrieve the list of
available options.

.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Product/Filters

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Access token provided by IDP
    :query SearchString: *(Required)* Represents the search term or keyword you want to use to filter the products. For a complete list without any filtering, use the value *

    **Example request**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Filters?SearchString=* HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>

    **Example response**

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        [
            {
                "code": "Brand",
                "portCode": 0,
                "values": [
                    {
                        "active": false,
                        "code": "Some brand",
                        "count": 122
                    },
                    {
                        "active": false,
                        "code": "Some other brand",
                        "count": 132
                    }
                ]
            },
            {
                "code": "Category",
                "portCode": 0,
                "values": [
                    {
                        "active": false,
                        "code": "CV-toestellen",
                        "count": 3841
                    },
                    {
                        "active": false,
                        "code": "Warmtepompen",
                        "count": 3121
                    },
                    {
                        "active": false,
                        "code": "Zon-PV",
                        "count": 524
                    }
                ]
            }
        ]

The response is a list of available filters. In the case `Brand` and `Category`. For each of these filters the Top 20
options are listed including the number of results in case this option is applied. Should you require all options,
then you should use the FiltersForField-endpoint.

:code:              The name of the filter
:values.[].code:     The name of the filter option
:values.[].count:    The number of search replies in case this filter option is applied


Apply the filters to product query
===================================

After retrieving the filters, you can proceed with querying products and incorporating filter options.
The filters are constructed using an array of filter objects, following the format described below:

.. code-block:: typescript

    Filters = Array<{
        Code: string;
        Values: [{
            Code: string;
        }]
    }>

In the above structure, the Code at the root-level represents the name of the filter obtained from the /Filters/
endpoint. The Values field is an array of objects, each containing a single property called Code, which represents
the name of the FilterOption obtained from the /filters/ endpoint. This array determines the selected filter options.

To convert the above object into a GET query, use the following format:

.. code-block::

    Filters[0].Code=string&Filters[0].Values[0].Code=SomeCode

Let's consider a real-life example. Suppose you only want to query elements from the 'CV-Toestellen' and 'Warmtepompen'
categories. In that case, your filter object would be constructed as follows:

.. code-block:: typescript

    Filters = [{
        Code: 'Category',
        Values: [
            { Code: 'CV-toestellen' },
            { Code: 'Warmtepompen' },
        ];
    }];

This translates into the following GET query:

.. code-block::

    Filters[0].Code=Category&Filters[0].Values[0].Code=CV-toestellen&Filters[0].Values[1].Code=Warmtepompen




.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Product/Search?Filters[0].Code=Category&Filters[0].Values[0].Code=CV-toestellen&Filters[0].Values[1].Code=Warmtepompen

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Access token provided by IDP
    :query SearchString: *(Required)* Represents the search term or keyword you want to use to filter the products. For a complete list without any filtering, use the value *
    :query Filters: The filter string as described above
    :query Size: *(Required)* The number of results you want to retrieve per page
    :query From: The offset from which the results should begin. It is used for navigating through the paginated results.

    **Example request**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Search?SearchString=*&Size=10&Filters[0].Code=Category&Filters[0].Values[0].Code=CV-toestellen&Filters[0].Values[1].Code=Warmtepompen HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>

    **Example response**

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        {
            "items": [
                {
                    "publish": true,
                    "id": 38610,
                    "shortDescription": "Documentation Boiler",
                    "manufacturerGln": "123456789",
                    "manufacturerName": "Fluxility",
                    "productCode": "12345678",
                    "gtin": "987654321",
                    "brand": "Fluxility",
                    "model": "X-class",
                    "version": "FLX-100",
                    "category": "CV-toestellen",
                    "etimClass": {
                        "code": "EC010231",
                        "description": "Boiler Direct Gestookt"
                    },
                    "status": {
                        "code": "94E",
                        "description": "Uitlopend"
                    },
                    "changeDate": "2023-06-07T12:00:00.000+00:00",
                    "startDate": "1989-03-06T00:00:00+00:00",
                    "isDeleted": false,
                    "isDummy": true,
                    "hasImage": true,
                    "recordCreateDate": "1989-03-06T00:00:00+00:00"
                }
            ],
            "took": 20,
            "total": 1
        }


Retrieve full product
=======================================
The search results only provide a limited amount of information about products. To obtain more detailed information,
you need to query the specific product using either the FGO product ID (referred to as the `id` field in the search
results) or a combination of the manufacturer's GLN code and the manufacturer's product code (referred to as the
`manufacturerGln` and `productId` fields in the search results). Both methods will yield the same response.

.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Product/{productId}

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Access token provided by IDP

    **Example request using only FGO ID**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/1234 HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>

    **Example request using only tuple of Manufacturer GLN and product id**

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/{manufacturerGln}/{productId} HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>


The response contains comprehensive information about the requested product. In this tutorial, we will cover a few
specific items

:features:          This is a list of features based on ETIM feature codes
    :code:          The ETIM feature code.
    :description:   The human-readable value of this ETIM feature
    :logicalValue:  Present if feature is a boolean field
    :numericValue:  Present if feature is a numeric value

:attachments:        A list of documents attached to this product
    :location:      The URI to download the document/image (not URL encoded!).
    :title:         The title of the document.

:checklist:         A list of available checklists for this product
:faultCodes:        Known fault codes associated this device
