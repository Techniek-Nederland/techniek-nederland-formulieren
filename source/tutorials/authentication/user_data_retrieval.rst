User Data Retrieval
--------------------

In the previous tutorial, you authorized the application to retrieve user data on behalf of the user.
In this step, we will retrieve the same user data from the IDP's API using the access token. (nb. To get the user
profile, you can extract the `id_token`, but that is beyond the scope of this tutorial.)

User data can be requested via the endpoint https://inlog.tnl.nu/o/userinfo/. We will first explain how
to do this using Postman, followed by an example using HTTP.

#. Open your workspace "Techniek Nederland" in Postman and navigate to the collection "Identity Service Provider".
#. Click on "New".
#. Choose "Request".
#. Select the HTTP method "GET".
#. Enter the URL "https://inlog.tnl.nu/o/userinfo/".
#. Click on "Save" and save the request in the "Identity Service Provider" collection.
#. Switch to the "Authorization" tab. You will see that the "Type" is now set to "Inherit auth from parent", which in this case refers to the collection. This means that the access token will be applied.
#. Click on "Send".
#. The data will now be sent, and you will receive a JSON response containing the user's information.

Below you find an example of the HTTP call.


.. http:get:: https://inlog.tnl.nu/o/userinfo/

    Request the user profile

    :reqheader Accept: Response to accept, eg. application/json
    :reqheader Authorization: Provide the access token: `Bearer <INSERT TOKEN HERE>`

    .. sourcecode:: http

        GET /o/userinfo/ HTTP/1.1
        Host: inlog.tnl.nu
        Accept: application/json
        Authorization: Bearer <INSERT ACCESS TOKEN>


    **Example response**

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Content-Type: application/json

        {
            "sub": "999",
            "livits_id": "12345678",
            "name": "Wouter Klein Heerenbrink",
            "companies": [
                "Fluxility"
            ]
        }


The response contains the following information:

:sub:            The id of the client the requested the access token (your app)
:livits_id:      The member ID at Techniek Nederland
:name:           The full name of the user
:companies:      A list of company names that the user is linked to (at Techniek Nederland)
