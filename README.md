# VBox Gateway PVR Client

Warning: this addon is still work in progress!

This repository provides a [Kodi] (http://kodi.tv) PVR addon for interfacing with the VBox Communications XTi Gateway devices. This README serves as a quick overview of the functionality and architecture of the addon, to make it easier for others to possible contribute.

### Architecture

This addon has been built from the ground up using C++11. The main functionality is contained within the `vbox` namespace, the only file outside that is `client.cpp` which bridges the gap between the Kodi API and the API used by the main library class, `vbox::VBox`. The idea is to keep the addon code as decoupled from Kodi as possible.

The addon communicates with a VBox gateway using the gateway's HTTP API. Since the structure of the responses vary a little bit, a factory is used to construct meaningful objects to represent the various responses. All response-related code is located under the `vbox::response` namespace.

The addon requires XMLTV parsing since that's the format the gateway provides EPG data over. The classes and utilities for handling this are located under `vbox::xmltv`.

The `vbox::VBox` class which `client.cpp` interfaces with is designed so that an exception of base type `VBoxException` (which is an extension of `std::runtime_error`) is thrown whenever ever a request fails. A request can fail for various reasons:

* the request failed to execute, i.e. the backend was unavailable
* the XML parsing failed, i.e. the response was invalid
* the request succeeded but the response represented an error

### Useful links

* [Kodi's PVR user support] (http://forum.kodi.tv/forumdisplay.php?fid=167)
* [Kodi's PVR development support] (http://forum.kodi.tv/forumdisplay.php?fid=136)

###  License

The code is licensed under the GNU GPL version 2 license.
