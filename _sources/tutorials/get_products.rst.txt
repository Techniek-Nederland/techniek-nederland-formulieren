Get product information using 2BA API
-------------------------------------

In order to easily get all information on a Product, you can query the 2BA database. This tutorial will only cover
the calls to make. To get started with 2BA (create account, get subscription, get keys etc) we kindly refer to `2BA's
documentation <https://www.2ba.nl/nl/documentatie/webservices>`_.

Search for a product
++++++++++++++++++++

.. http:get:: https://apix.2ba.nl/api/v1/Fgo/Product/Search

   Returns a list of products that met your query.

   **Example request**:

   .. sourcecode:: http

      GET /api/v1/Fgo/Product/Search?From=0&Size=1&SearchString=nefit&Filters[0].Code=Model&Filters[0].Values[0].Code=ProLine HTTP/1.1
      Host: apix.2ba.nl
      Accept: application/json
      Authorization: OAuth token to authenticate

   **Example response (excerpt)**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: text/javascript

      {
         "items": [
            {
                "publish": true,
                "id": 2769945,
                "shortDescription": "Nefit ProLine NxT HRC 24/CW4",
                "manufacturerGln": "8712423018495",
                "manufacturerName": "Bosch Thermotechniek",
                "productCode": "7746901851",
                "gtin": "04054925005042",
                "deeplink": "https://www.nefit.nl/professioneel/producten_pro/categorie-overzicht-pro_719",
                "brand": "Nefit",
                "model": "ProLine",
                "version": "NxT HRC 24/CW4",
                "category": "CV-toestellen",
                "etimClass": {
                  "code": "EC011396",
                  "description": "Gaswand Combiketel"
                },
                "status": {
                  "code": "126",
                  "description": "Actueel"
                },
                "weightQuantity": 19.65,
                "weightMeasureUnit": {
                  "code": "KGM",
                  "description": "Kilogram"
                },
                "changeDate": "2022-02-16T00:00:00+00:00",
                "isDeleted": false,
                "isDummy": false,
                "hasImage": true,
                "serviceMenuLoginDescription": "nvt",
                "serviceMenuLoginCode": "nvt",
                "recordCreateDate": "2014-09-01T11:20:45.067+00:00"
            }
        ],
        "took": 16,
        "total": 6
      }

   :reqheader Authorization: OAtuh token to authenticate
   :query integer From: Offset to start from (0-based)
   :query integer Size: Number of results to return
   :query string SearchString: Filter string
   :query object Filters: A set of filters. Please see `2BA Swagger <https://apix.beta.2ba.nl/swagger/index.html>`_ for a full list of filters.


Filter fields
++++++++++++++++++++

.. http:get:: https://apix.2ba.nl/api/v1/Fgo/Product/FiltersForField

   Returns a list of models, series and versions that can be used to filter down the list of products.

   **Example request**:

   .. sourcecode:: http

      GET /Fgo/Product/FiltersForField?field=Model HTTP/1.1
      Host: apix.2ba.nl
      Accept: application/json
      Authorization: OAuth token to authenticate

   **Example response (excerpt)**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: text/javascript

      {
        "code": "Model",
        "count": 200,
        "portCode": 0,
        "type": "Model",
        "values": [
            {
                "active": false,
                "code": "Gasgestookte Stralingsverwarmring",
                "count": 40
            },
            ...
        ]
      }

   :reqheader Authorization: OAuth token to authenticate
   :query string Field: The field you want to retrieve filters for. Choices are Category, Brand, Model and Version.
   :query object Filters: A set of filters. Please see `2BA Swagger <https://apix.beta.2ba.nl/swagger/index.html>`_ for a full list of filters.
