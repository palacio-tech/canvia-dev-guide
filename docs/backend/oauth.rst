.. _backend-oauth:

OAuth Support
=================

.. highlight:: shell

As of now, we have implemented an authorization code flow. 

The steps involved are

* Your application opens a browser window to send a Canvia user to 
  our login screen
* The user logs in and see the authorization prompt. She approves the request.
* The user is redirected back to the application along with an authorization
  code in the query string of the page URL. 
* The application reads the authorization code.
* The application sends a request to the access token end point of our OAuth server
  to receive an actual access token.
* The application can use the access token to access our API on behalf of the user.

In order to align OAuth with our existing API, we have one more step.

* The application uses the access token to login through our Backend REST API
  and get our regular JWT access token.

At the moment, when your app is authorized, it gets full access to the
user's account. Users are properly notified before confirming access about it.
We are still working on implementing separate scopes so
that applications can limit their requirements.


Client Applications
------------------------

OAuth allows for two types of applications

* Confidential applications (which can safely use both client id and client secret)
* Public applications (which can only work with client id)

At the moment we only provide support for confidential applications.



Registering Your Application
-------------------------------------


Application registration process is manual at the moment.
Please contact us with following information, we will generate
a client id and client secret for your application.

.. list-table::
    :header-rows: 1

    * - Field
      - Description
    * - Name
      - Name of your application
    * - Organization
      - Name of the organization which is developing the application
    * - Home page
      - URL of the home page for your application or organization
    * - Description
      - A small description about your application
    * - Privacy Policy
      - URL of the page where the privacy policy for your application is maintained.
    * - Redirect URIs
      - List of URIs which are acceptable where the authorization code will be sent

Optionally, you can also send an icon for your application (square shape). 

This information will be verified and displayed in the OAuth consent screen where
users will confirm or deny their user account access to your application.

If you don't have any suitable Redirect URL with your application, you can use
one of ours:

* https://prod.palacio.life/backend/oauth/success.html
* https://prod.palacio.life/backend/api/v1/


Building the Login Flow
--------------------------

Following end-points are key to the login flow.

.. list-table::
    :header-rows: 1

    * - End-point
      - Purpose
    * - https://prod.palacio.life/backend/oauth/login.html
      - Canvia OAuth Login Screen
    * - https://prod.palacio.life/backend/oauth/token
      - Canvia end-point for obtaining access token from authorization code
    * - https://prod.palacio.life/backend/api/v1/auth/login/token
      - Canvia end-point for obtaining regular JWT token from OAuth access code.

  


Your application must initiate a redirect (or open a browser window) to 
our login end point which will display the login dialog.

.. rubric:: Parameters


.. list-table::
    :header-rows: 1

    * - Name
      - 
      - Description
    * - client_id
      - required
      - Id assigned to your client application
    * - redirect_uri
      - required
      - The URI where the authorization code will be sent
    * - grant_type
      - required
      - This must be *authorization_code* for now
    * - response_type
      - required
      - This must be *code* for now
    * - state
      - optional
      - An optional string which will be transparently forwarded along with code


.. rubric:: Initiating the login screen

A typical login request URL will look like:

.. code-block:: shell

    https://prod.palacio.life/backend/oauth/login.html?
      client_id={app-id}
      &redirect_uri={redirect-uri}
      &grant_type=authorization_code
      &response_type=code
      &state={state-value-string}

* The *redirect_uri* must be one of the registered redirect URIs when your client was
  created. If you want to introduce a new redirect URI, please send us its URI 
  along with your application client id.
* The *state* parameter should be used for preventing cross-site request forgery.
  Your application should generate some string unique to the specific invocation
  of the login flow. Once your application receives the authorization code at
  the redirected URL, it should verify that the state matches.


.. rubric:: Retrieving authorization code

Once the user approves your application, the browser will be
redirected to your redirect URI. 

It will look like::

    {redirect_uri}?code={authorization_code}&state={state-value-string}

Some sample code for retrieving the code is available in 
a nice tool `here <https://github.com/lapwinglabs/oauth-open>`_.

An authorization code is short-lived and you must convert it to 
an access token immediately.


.. rubric:: Obtaining the access token

For obtaining the access token, you need to provide

* client id
* client secret
* authorization code
* redirect URI
* Grant type

The request would look like

.. code-block:: http

    POST /oauth/token HTTP/1.1
    Host: https://prod.palacio.life/backend
    Content-Type: application/x-www-form-urlencoded

    client_id={your-app-client-id}
    &client_secret={your-app-client-secret}
    &redirect_uri={redirect-uri}
    &code={received authorization code}
    &grant_type=authorization_code


* The data for this POST request must be *x-www-form-urlencoded*.
* *grant_type* must be *authorization_code*.
* *redirect_uri* must match the URI in the original login request.


.. code-block:: json

    {
        "access_token": "{access token}",
        "token_type": "Bearer",
        "expires_in": 86399,
        "refresh_token": "{refresh token}",
        "clientId": "{your app client id}",
        "userId": "[user id]",
    }


Logging in using the OAuth access token
--------------------------------------------

This step is similar to the :ref:`Normal login <backend-login>` process. 
In place of email and password, we send the OAuth access token as follows.

.. code-block:: http

    POST /auth/login/token HTTP/1.1
    Host: https://prod.palacio.life/backend/api/v1
    Authorization: Bearer c1fbcace72c64b654fbeaff9fd3aeca398906d36


* The access token is sent in *Authorization* HTTP header.
* The response is identical to :ref:`normal login <backend-login>`.




Refreshing access token
--------------------------

You can use the refresh token received in the original request for
access token for refreshing your access token.

The end point is same */oauth/token*. Two parameters are changed.

* In *grant_type*, specify *refresh_token*.
* In place of *code*, specify *refresh_token* parameter with the value of refresh token.

References
-----------------

* `An introduction to OAuth 2.0 <https://oauth.net/2/>`_
* `What is the OAuth 2.0 Authorization Code Grant Type? <https://developer.okta.com/blog/2018/04/10/oauth-authorization-code-grant-type>`_
* `Refreshing access tokens <https://www.oauth.com/oauth2-servers/access-tokens/refreshing-access-tokens/>`_
