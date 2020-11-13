# About

Here are the set of web frameworks and APIs that power virtual performing arts venue http://elektron.live/ and other creative projects made by the elektron residence program.

# General overview of the platform

The key pieces of the platform are:

## 1. 2D homepage for elektron.live

It is the main entrypoint to the platform, it is used both for public events and residence experiments. Implemented in VueJS 3 with no Javascript compiling / bundling.

Link: https://elektron.live

Github: https://github.com/elektronstudio/live

> You can set up your own experimentation space to use any kind of indentifier in the URL, for example:
> https://elektron.live/mysecretspace

## 2. Experimental 3D homepage for elektron.live

### First prototype

Implemented in ReactJS.

Link: https://elektron-foyer.netlify.app/

Github: https://github.com/elektronstudio/foyer

### Second prototype

Implemented in VueJS and sharing a lot of code with elektron.live. Will be intergrated into the elektron.live in the future.

Link: https://elektron-foyer2.netlify.app/

Codesandbox: https://codesandbox.io/s/github/elektronstudio/foyer2?file=/index.js

Github: https://github.com/elektronstudio/foyer2

## 3. Message broadcasting

Github: https://github.com/elektronstudio/ws

Server instance: `wss://ws-fggq5.ondigitalocean.app`

The heart of the elektron.live platform is a Websocket server where **clients** are sending _messages_ to the **server** and the server is sending messages back to all other connected clients.

> This allows low-bandwith, real-time, two-way syncronizaton of data between each client but is not suitable to high-bandwidth video transmissions

The messages contents can be:

- a chat message
- a user location in X Y Z coordinates
- an encoded image file from the user webcam
- any data, really

## 4. Video broacasting / steaming

There is also a web streaming platform where a client can stream it's video and audio feed to a streaming server and all the other clients will receive the video as a HSL (MP4 for streaming) feed.

> Video streaming is high-bandwith media channel with noticable delay (starting from ~7 seconds until ~30 seconds) so it's not great for two-way realtime communication but great for one-side communication with large audiences. There can be exceptions of course, audience <-> performer interaction could work in some cases.

### Using steaming

We are using the same streamkey for all the URLS and links. Here is the example where streamkey is `residence`:

**Video stream upload (ingest)**

Stream URL: `rtmp://165.227.149.4:1935/stream`

Streamkey: `residence`

**Video stream download (broadcast)**

`https://stream.elektron.studio:8443/live/residence.m3u8`

**Event page with video stream**

https://elektron.live/residence

### Streaming implementation

There are multiple streaming video servers:

#### Custom server

Custom serveris based on Docker image https://github.com/alfg/docker-nginx-rtmp

#### Streaming provider server

We also use https://babahh.com streaming services that maintain a custom https://flussonic.com server instance.

## 5. Image processing / statistics server

There is also a server for server-side audience image analysis and statistics gathering at https://elektron.live/area51/ (source code not yet public)

## 6. Video conferencing server

There is also an experimental WebRTC-based video conferencing server in the works at https://elektron.live/videotest (the rightmost link).

It is based on https://openvidu.io/ Docker image and currently hosted at https://elektron.studio.

# Example client code

There are code examples that connect to the elektron.live messaging server:

### Max integration

Download: https://github.com/elektronstudio/example_max/archive/master.zip

Github: https://github.com/elektronstudio/example_max

### Javascript / p5 integration

Codesandbox demo: https://codesandbox.io/s/github/elektronstudio/example_p5/tree/master?file=/index.js

Github: https://github.com/elektronstudio/example_p5

### Javascript / ToneJS integration

Codesandbox demo: https://codesandbox.io/s/github/elektronstudio/example_tonejs?file=/index.js

Github: https://github.com/elektronstudio/example_tonejs
