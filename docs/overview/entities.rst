Key Entities
==================

Artworks
----------

A work of art, artwork, art piece, piece of art or art object is an aesthetic physical item or artistic creation.
Canvia maintains digital renditions of these artworks in 
its repository. The digital renditions may be in the form
of images or videos.

We currently support following file formats for artworks:
JPEG, PNG, TIFF, MP4. Canvia devices don't support any
audio playback for now.

An artwork entity stored in our database consists of

* The high quality image or video rendition of the artwork.
* Its thumbnails for representation purposes in web or mobile
  user interfaces.
* Metadata associated with the artwork (title, artist, description,
  categorizations, etc.)
* Ownership information

There are two types of artworks

* Canvia artworks are prepared by Canvia curation team
  and made available on the platform for all customers.
  Some of these artworks are free for all and some are 
  available under various premium subscriptions.
* Personal artworks are uploaded by users and they are
  accessible only to the user who owns them.

Personal artworks are also called my artworks in
this guide. Users may just upload their personal 
images as personal artworks. They don't need to
provide detailed meta data information. However,
should the users choose to do so, they can categorize
and annotate their images just like regular artworks
in Canvia.

Artworks are categorized by Canvia curation team 
under following heads:

* Subject : Landscape, Figurative, Architecture, etc.
* Era: Ancient, 15th Century, etc.
* Medium: Watercolors, Photography, Textiles, etc.
* Movement: Classical, Romanticism, Surrealism, etc.
* Color: Red, Green, Blue, etc.

Playlists
--------------

Playlists are collections of artworks. One can arrange
a set of artworks into a playlist so that she can play
them in a sequence on a Canvia device.

There are following types of playlists.

* Canvia playlists are prepared by Canvia curation team and
  available to all Canvia customers.
* Personal playlists are prepared by users and are available
  to themselves.
* Some playlists are marked by our curation team as featured playlists.

Personal playlists are also called my playlists in this guide.

Users can bookmark specific playlists as their favorite
playlists.

Artists
----------

An artist is a person who created a particular artwork.
We maintain a database of artists associated with the
artworks in Canvia repository. 


Users
-------

A user is a person holding a Canvia device. All
APIs are accessible only to logged in users.

A user's data includes

* Profile information [name, email, password etc.]
* One or more Canvia devices she owns
* Favorite artworks [from Canvia collection]
* Favorite playlists [from Canvia collection]
* Favorite artists [from Canvia collection]
* Personal artworks
* Personal playlists
* Preferences [subject, color, era, medium, movement]

User preferences are helpful in making recommendations
to users about artworks matching their taste.

Users may subscribe to different tiers

* Free tier
* Premium tier

Devices
----------

In the backend, information about a Canvia device
owned by a user is maintained.

* A user can own one or more Canvia devices.
* The devices must be registered with the backend 
  before they can be used for artwork display.
* A user can send playlists or artworks to be played
  on a Canvia device.
* A user can give play/pause/next/previous navigation
  commands to a Canvia device.
* A user can define scheduled events for playback of
  artworks or playlists at specific times on
  periodic basis (daily, weekly, monthly, etc.)
* A user can change different device settings 
  (orientation, text overlay, etc.)
