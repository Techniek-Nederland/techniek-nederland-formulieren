Authentication
--------------

To utilize the web services and applications provided by Techniek Nederland, users are required to have an account
with Techniek Nederland. This requirement also applies when third-party software utilizes these web services.
In such cases, the users must still log in with their Techniek Nederland account so that the services can be
accessed on their behalf.

Authentication is performed using the OAuth (and OIDC) protocol. Users can log in through the Identity Service
Provider (IDP) of Techniek Nederland, which can be accessed at https://inlog.tnl.nu/. Third-party software can
refer to this IDP using the OAuth protocol.

Third-party software needs a `client_id` and `client_secret` to use the Identity Service Provider. These credentials
can be requested from Bart Molmans by sending an email to b.molmans@technieknederland.nl.

The following tutorials provide detailed instructions for enabling third-party software to allow users to log in
and access Techniek Nederland's web services on their behalf. Additionally, the tutorials explain how to retrieve
user data and invoke Techniek Nederland's services on behalf of the user.


.. toctree::
    user_authentication
    user_data_retrieval
    service_invocation




For any further assistance or inquiries, please contact our support team at fgoplus@2ba.nl.

Note: This documentation assumes a basic understanding of web development and authentication protocols such as OAuth.
Should you require more info, please have a look at for instance https://auth0.com/docs/authenticate/protocols/oauth
for an in depth and thorough explanation.
