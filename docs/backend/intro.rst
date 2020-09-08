Introduction
==============

.. highlight:: shell

Applications working on behalf of end-users can
use the backend API for a number of features. 
Here is a basic listing. More details are there
in other sections.


* User registration and user login
* Working with playlists
* Working with artworks
* Working with artists
* Working with user preferences
* Working with Canvia devices


.. note::

    Backend API allows you to interact with the
    devices through a bridge implemented by
    web sockets. Some device specific functionality
    is not available through backend API.



Conventions
--------------------

A few conventions have been followed in this guide. 
A prior understanding of these conventions will be helpful in 
making sense of the API.


The following table describes the essential variables 
used in the guide.

.. list-table::
    :header-rows: 1

    * - Variable
      - Description
      - Value
    * - URL
      - Base URL for the Palacio Backend API
      - https://prod.palacio.life/backend/api/v1
    * - user-email
      - Email address of the user for authentication
      - 
    * - user-password
      - Password of user for authentication
      - 
    * - auth-token
      - JWT authentication token
      - 

In all requests, the base URL is **{{URL}}**.


Authentication and JWT Token
-------------------------------

Authentication is essential for accessing all the APIs. 
A user most login first before she can access
artworks, playlists, etc.. 
The **{{user-email}}** and **{{user-password}}** variables are used
in login request examples.

The login API returns a JWT token. 
This token must be preserved and sent in all following API calls
as an HTTP request header. 
The variable **{{auth-token}}** should be filled with the JWT token 
received during authentication.
The JWT token should be sent in an HTTP header named **x-access-token**.


Search APIs with Pagination
------------------------------------


We provide search APIs for playlists, artworks, artists,
etc.

* All the search APIs are GET requests.
* All search APIs are paginated.
* There are two essential parameters `limit` and `page`.
* `limit` defines the number of results per page.
* `page` defines the page number.
* `limit` defaults to 10.
* `page` starts with 1.
* Search parameters are specified through `param=value` 
  syntax in search query string.
* It is possible to specify which attributes of individual
  search results should be returned from backend.
* Use `p=attr1&p=attr2` syntax to specify that you want
  `attr1` and `attr2` attributes to be returned.

Example query:: 

 {{URL}}/artworks/search?artist=Albert&page=2&limit=4&p=artist

* We are searching over artworks
* The query parameter is `artist=Albert`.
* `limit=4` means 4 results per page will be returned.
* `page=2` means 2nd page of result (i.e. results 5-8)
  will be returned.
* `p=artist` means that return the `artist` attribute of
  each artwork in the search results.

Here is the search result

.. code-block:: JSON

    {
        "docs": [
            {
                "_id": "5cc0aef07c5a9419bc2e6a19",
                "title": "Evening on the Prairie",
                "artist": "Albert Bierstadt",
                "artist_ref": {
                    "_id": "5bd9d7489c4bbf6313311411",
                    "display_name": "Albert Bierstadt"
                },
            },
        ],
        "total": 15,
        "limit": 4,
        "offset": 4
    }
  
* The search results is a JSON object.
* The `docs` array is the array of results.
* The `total` field informs us of the total number of
  search results.
* `docs.length` tells us the number of search results
  in this page of result.
* `limit` is the number of search results requested per
  page.
* `offset` is the 0-based index of the first result
  in this page of results. `offset=limit*(page-1)`.
* Second page means result number 4-7 [in 0 based indexing].
* We have skipped 3 of the results from response sample
  above to focus on main points.
* Since `p=artist` was specified, hence `artist` attribute
  is returned in each search result 
  (if filled in database). 
* Some attributes are always returned no matter the 
  query (based on resource type).
* For `artworks` queries, `title` and `_id` are always
  returned in results. These are default attributes.
* In case of artists, we store both artist name with
  each artwork and a reference to `artist` resource
  in database if it exists.
* As a special case, whenever `artist` attribute
  is returned, `artist_ref` attribute is also returned
  for each artwork.
* However, this is special case. Usually, only the
  specified attributes and default attributes will
  be returned.

