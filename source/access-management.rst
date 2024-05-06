Access Management
-----------------

The Techniek Nederland Forms API can be accessed by your application by using the OAUth protocol. Gaining
access involves requesting an API key, authenticating users, and obtaining a token. This section will guide you through
the process of accessing the API using the OAuth protocol. At the bottom of this section your will find the
`Authentication parameters`_ for setting up the connection.

Requesting an API Key
======================

To begin, you'll need to request an API key at Techniek Nederland. The API key acts as a unique identifier for your
client application and allows you to make authenticated requests to the Identity Service API (IDP). Please send an email
to p.zwakhals@technieknederland.nl to request access. Please state your name, organisation, goal and provide us with the
`redirect_url` (or multiple) for you application.

Authenticating Users
=====================
Once you have an API key for the IDP, your application needs permission from your user before you can access the API
resources on behalf of them. OAuth provides a secure way to authenticate users through an Identity Service Provider (IDP),
using the `Authorization Code Flow  <https://datatracker.ietf.org/doc/html/rfc6749#section-4.1>`_.

Below are the steps for authenticating a user. Some technical details have been left out for these are usually
described in documentation of your own OAuth library.

    1.  **Redirect Users to Techniek Nederland IDP (`https://inlog.tnl.nu/`)** When a user wants to access the API through
        your application, the user must authorize your application in the IDP. This page typically requires the user to
        enter their credentials.
    2.  **Authorization** After successful authentication, the IDP will present the user with a consent screen.
        This screen explains the permissions (actually scopes) your application is requesting, such as accessing
        specific forms or data on behalf of the user. The user must grant your application permission to access
        these resources. By default you will want to request the *profile* and *openid* scope, supplemented with
        the FGO and Form-specific scopes like *FGO*, *FGOWS*, *FORMS* and *FORMSWS*. Please see list of services
        for more detailed info on the scopes.
    3.  **Obtaining Authorization Code**: Once the user grants permission, the IDP will redirect the user back
        to your application, providing an `authorization code` as a parameter in the redirect URL.
    4.  **Exchanging Authorization Code for Access Token** Your application must securely exchange the
        `authorization code` with the IDP to obtain an access token.
        This access token represents the user's authorization to access the API on their behalf.

If you want more info on the OAuth flow, please have a look at our tutorial on
:ref:`tutorials/authentication/user_authentication:User Authentication`.


Requesting Data from the API
============================
With the user's access token in hand, your application can make requests to the API on behalf of the user. Include
the access token in the request headers to authenticate and authorize your application to access the API's resources
at https://api.fgoplus.nl and https://formsapi.technieknederland.nl.

Remember, the access token has an expiration time. If the token expires, your application will need to use a
refresh token or follow the authentication process again to obtain a new access token.

Authentication parameters
============================

Connecting to identity service provider:

:authorization_endpoint:    https://inlog.tnl.nu/o/authorize/
:token_endpoint:            https://inlog.tnl.nu/o/token/
:userinfo_endpoint:         https://inlog.tnl.nu/o/userinfo/
:openid-configuration:      https://inlog.tnl.nu/o/.well-known/openid-configuration/
:client_id:                 To be requested p.zwakhals@technieknederland.nl
:client_secet:              *Not applicable for client applications*
:grant_type:                Authorization code (make sure to use PKCE)
:scopes:                    openid, profile, FGO, FGOWS



