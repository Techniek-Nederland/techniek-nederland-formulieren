Service invocation
-------------------

The previous tutorial explained how to fetch information from the IDP itself using the access token. This last
tutorial on authentication briefly shows the same example, but this time for an external resource server. The
FGO Plus Webservice is used as an example.

#. Open your workspace "Techniek Nederland" in Postman and navigate to the collection "Identity Service Provider".
#. Click on "New".
#. Choose "Request".
#. Select the HTTP method "GET".
#. Enter the URL "https://api.fgoplus.nl/api/v1/Fgo/Product/Search".
#. Click on "Save" and save the request in the "Identity Service Provider" collection.
#. Switch to the "Authorization" tab. You will see that the "Type" is now set to "Inherit auth from parent", which in this case refers to the collection. This means that the access token will be applied.
#. Go to the Params tab and at a parameter "SearchString" with a value like "Pump"
#. Click on "Send".
#. The data will now be sent, and you will receive a JSON response containing search results

Below you find an example of the HTTP call.


.. http:get:: https://api.fgoplus.nl/api/v1/Fgo/Product/Search

    Search the FGO Plus database for products

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Provide the access token: `Bearer <INSERT TOKEN HERE>`

    .. sourcecode:: http

        GET /api/v1/Fgo/Product/Search HTTP/1.1
        Host: api.fgoplus.nl
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>


    **Example response**

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        {
            "items": [],
            "took": 30,
            "total": 4922
        }

The response is outside of scope for this tutorial. Please see the other tutorials on requesting the webservices
or take a look at the Swagger documentation of the FGO Webservice (https://api.fgoplus.nl/swagger/index.html). For
the forms API, which is used to retrieve all forms other than checklists, please refer to https://formsapi.technieknederland.nl/swagger/index.html.
