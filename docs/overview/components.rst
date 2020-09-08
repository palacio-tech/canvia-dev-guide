Key Components
====================

The key components in the Canvia System are

* Backend API Server
* Web Sockets Server for real time communication
* Canvia Device 
* Canvia Web Application 
* Canvia Mobile Application (iOS and Android)
* Canvia Desktop Application (Windows and Mac)


Backend API Server
--------------------------

Backend API is the heart of Canvia operations. 
It is hosted at
`https://prod.palacio.life/backend/ <https://prod.palacio.life/backend/>`_. 

All client applications in the following are built on top of the
backend API.


Canvia devices interact with the backend API to access artworks and
playlists to display them on screen.


Web Sockets Server
-----------------------

Real-time interaction between Canvia devices and our web application
is achieved through the web socket server. 


Canvia Device
---------------------------

Canvia devices are the physical frames purchased by our
customers and installed in their premises. 

A Canvia device joins the local Wi-Fi network and interacts
with the backend through backend API and web socket channels.

Each Canvia device also runs a local web service accessible
at http://<canvia-device-ip> where <canvia-device-ip> is
the IP address assigned to the device by the local Wi-Fi network.

This web service runs the **Device REST API**. The Device API 
is used by the mobile and desktop applications for direct 
access to the device. 

The Device API provides features like:

* Device software maintenance and upgrade
* Device playback control and playback queue access
* Ability to upload photos directly to the device

Device is capable of operating even if Internet is inaccessible.

Canvia Web Application
------------------------------------

Canvia web application for end users is hosted at
`my.canvia.art <https://my.canvia.art/>`_ 

It is built on top of 

* Backend API
* Web Sockets

It allows owners of Canvia devices to

* Explore artworks and playlists available on Canvia platform
* Create their own playlists
* Upload their own images
* Play artworks and playlists on their devices
* See what is playing and what's in the queue on their devices
* Control playback on their devices (previous, next, pause, resume, etc.)
* Setup events for playing artworks, playlists on their devices on a 
  well-defined schedule 

It has a lot of features to make
the device playback user experience pleasant.  


Canvia Mobile Application
----------------------------------

Canvia mobile applications are available for both
iOS and Android platforms from corresponding app stores.

These applications are built on top of the backend API
and the device API. They allow you to control a device
from the comfort of your phone.

Canvia Desktop Application
---------------------------------------

Canvia desktop applications are available for both 
Windows and Mac operating systems. 

The desktop app is quite similar to web application.
However, since it runs as a native application
locally within the Wi-Fi network, hence it has
direct access to the device. Thus, it can exploit
the device API for closer integration with the device.


It provides full support for working with a Canvia device



It is built on top of 

* Backend API
* Device API
* Web Sockets
