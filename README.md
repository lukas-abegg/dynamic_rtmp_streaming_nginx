# Dynamic Streaming via nginx

This project should explain how to create high scalable streaming solutions based on nginx and Wowza Media Systems.


## What should be achieved by this project
As initial state, there was the requirement to create a high scalable dynamic streaming
solution (CDN) for Live-Broadcasts offered by smartphones, cameras and other mobile devices.


## Which resources are used?
We are using the following resources:
### Amazon Web Services
Our CDN solution is implemented as Cloud solution
based on AWS.
The advantage of this solution is to use as much
hardware instances as we want at what time we
want.
AWS offers already Auto Scaling (scalable instance
count based on rules), and Load Balancing (fair
sharing of offered server instances).
### Wowza Media Systems
We are using Wowza Media System as basic CDN
for delivery the content.
Wowza already offers testing VOD content without
any further configurations and is used by many
streaming solutions.
### NGINX
It is a very small webserver solution for
implementing any web solutions.
This server implements many web protocolls. For
our requirements we are using HTTP(redirecting)
and RTMP(streaming) protocol.
### Lua Scripts
Lua Scriptings offers many HTTP functions to read
request body arguments and a driver to handling
database queries.
NGINX does not offer the requested functionalities
by himself. So we are using Lua Scripts to get this
functionalities.
### Mongolab
Mongolab offers MongoDB’s to testing our CDN.
It offers many drivers to different programming
languages, also to Lua Scripts.
So we can use this driver for reading our stream
offering Wowza Server node to a requested stream
via a MongoDB.

## Installation Guide OpenResty
This an installation guide to install and configure nginx based streaming edges for Wowza
streaming solutions.
### What is OpenResty?
OpenResty is nginx based bundle of software including a standard nginx core, LuaJIT, many
carefully written Lua libraries, lots of 3rd-party nginx modules, and most of their external
dependencies.

[Web-Link to Openresty](https://openresty.org/#Download)
### What is Lua?
Lua is a small scripting language which allows to handle and manage http-requests on
nginx. In our case, we will use Lua to dynamically pull or push streams with on_play and
on_publish from nginx rtmp-module.
What is the nginx rtmp module?
This module is needed to stream videos to rtmp-clients. In our case we use a flash-player to
stream Adobe RTMP.

[Github-Link to nginx-rtmp-module](https://github.com/arut/nginx-rtmp-module)
### What is the nginx lua-resty-mongol module?
This module is a mongo driver to connect to a MongoDB. We use a MongoDB to save our
streaming servers (Wowza’s) identity and assigning specific streams to the Wowza-server
which offers the stream. This is a security issues to make sure, our nginx edges are not
open CDNs(Content Delivery Networks), to stream from wherever the client want, whatever
the client want.

[Github-Link to lua-resty-mongol](https://github.com/aaashun/lua-resty-mongol)
### How it should work?
When a client send a rtmp-request to nginx to receive a stream, nginx connects to the
MongoDB via this driver and try to find the Wowza server which offers this stream. If nginx
find a Wowza server, he takes the IP of the Wowza-Server and redirects to this IP with the rtmp-request he receives from the client. The nginx streams only streams, which are
documented in the MongoDB.


## What files are included in this Repository
* Term Paper - Dynamic Streaming  via nginx.pdf
 * Full installation guide including all instruction how to build and test this streaming solution
* Presentation - Dynamic Streaming via nginx.pptx
 * Short presentation of this solution 
* nginx.conf
 * Example of config file for nginx
