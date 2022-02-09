Get product information using 2BA API
-------------------------------------

In order to easily get all information on a Product, you can query the 2BA database. This tutorial will only cover
the calls to make. To get started with 2BA (create account, get subscription, get keys etc) we kindly refer to `2BA's
documentation <https://www.2ba.nl/nl/documentatie/webservices>`_.

.. NOTE::

    Some of the calls are a 'POST' in 2BA and will be transformed into GET calls (#BBAFGOSL-576)



Search for a product
++++++++++++++++++++

.. http:post:: https://apix.2ba.nl/api/V1/Product/Search

   Returns a list of products that met your query.

   .. note::
       Please note to *always* a default filter for `Tags`, for otherwise
       you'll search through **all** products including kitchen sinks. See example for the list of default tags.

   **Example request**:

   .. sourcecode:: http

      POST /api/V1/Product/Search HTTP/1.1
      Host: apix.2ba.nl
      Accept: application/json
      Authorization: OAuth token to authenticate

      {
        "languagecode": 1,
        "from": 0,
        "size": 1,
        "searchstring: "nefit",
        "filters": [
            {
                "code": "Tags",
                "values": [
                    {"code": "FGO-CV"},
                    {"code": "FGO-PV"},
                    {"code": "FGO-WP"}
                ],
            }
        ]
      }

   **Example response (excerpt)**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: text/javascript

      {
         "items": [
            {
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
                "etimClass": {
                  "code": "EC011396",
                  "description": "Gaswand combiketel"
                },
                "status": {
                  "code": "126",
                  "description": "Regulier beschikbaar"
                },
                "weightQuantity": 19.65,
                "weightMeasureUnit": {
                  "code": "KGM",
                  "description": "Kilogram"
                },
                "features": [
                  {
                    "code": "EF020003",
                    "description": "Materiaal warmtewisselaar",
                    "alphaNumericValue": {
                      "code": "EV000166",
                      "description": "Roestvaststaal (RVS)"
                    },
                    "type": "A",
                    "isModelling": false,
                    "isRegular": true,
                    "orderNumberModelling": 0,
                    "orderNumberRegular": 1,
                    "portCode": 0,
                    "changeCodeRegular": "Unchanged",
                    "changeCodeModelling": "Unchanged"
                  },
                  {
                    "code": "EF001257",
                    "description": "Kwaliteitsklasse",
                    "type": "A",
                    "isModelling": false,
                    "isRegular": true,
                    "orderNumberModelling": 0,
                    "orderNumberRegular": 2,
                    "portCode": 0,
                    "changeCodeRegular": "Unchanged",
                    "changeCodeModelling": "Unchanged"
                  }
                ]
              }
         ]
         "took": 1,
         "total": 257
      }

   :reqheader Authorization: OAtuh token to authenticate
   :<json integer languagecode: The requested language code (1 for Dutch)
   :<json integer from: Offset to start from (0-based)
   :<json integer size: Number of results to return
   :<json string searchstring: Filter string
   :<json object filters: A set of filters. Please see `2BA Swagger <https://apix.beta.2ba.nl/swagger/index.html>`_ for a full list of filters. Always include the Tags!


Filter fields
++++++++++++++++++++

.. http:post:: Product/FiltersForField?field={some-field}

   Returns a list of models, series and versions that can be used to filter down the list of products.

   .. note::
       Please note to *always* a default filter for `Tags`, for otherwise
       you'll search through **all** products including kitchen sinks.

   **Example request**:

   .. sourcecode:: http

      POST /Product/FiltersForField?field=Model HTTP/1.1
      Host: apix.2ba.nl
      Accept: application/json
      Authorization: OAuth token to authenticate

      {
        "filters": [
            {
                "code": "Tags",
                "values": [
                    {"code": "FGO-CV"},
                    {"code": "FGO-PV"},
                    {"code": "FGO-WP"}
                ],
            }
        ]
      }

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
                "code": "Warmteopwekkers",
                "count": 239
            }
        ]
      }

   :reqheader Authorization: OAuth token to authenticate
   :<json object filters: A set of filters. Please see `2BA Swagger <https://apix.beta.2ba.nl/swagger/index.html>`_ for a full list of filters. Always include the Tags!

