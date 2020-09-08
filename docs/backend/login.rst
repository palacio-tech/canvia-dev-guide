.. _backend-login:

Logging In
==============

There are two use cases

* End users who wish to login through API using
  their own credentials should continue reading
  in this section.
* Third party applications who wish to login on
  behalf of a user should look into 
  :ref:`backend-oauth` section.



.. rubric:: Logging in using email and password


Example request:

.. code-block:: http

    POST /authenticate HTTP/1.1
    Host: {{URL}}
    Content-Type: application/json

    {
        "email" : "{{user-email}}",
        "password" : "{{user-password}}"
    }


Example response:

.. code-block:: json


    {
      "_id": "<user_id>",
      "first_name": "<First Name of User>",
      "last_name": "<Last Name of User>",
      "email": "{{user-email}}",
      "message": "{{user-email}}",
      "token": "{{auth-token}}",
      "expiresIn": 604800
    }

