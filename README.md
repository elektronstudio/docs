## About

elektron.studio is a set of web frameworks and APIs that power virtual performing arts venue http://elektron.live/ and other creative projects made by our residence program.

## General overview of the platform

The key pieces of the platform are:

### 1. Message broadcasting

where **clients** are sending _messages_ to the messaging **server** and the server is sending messages back to all other connected **clients**. The message is also sent back to the original client.

> This allows low-bandwith, real-time, two-way syncronizaton of data between each client but is not suitable to high-bandwidth video transmissions

The messages contents can be:

- a chat message
- a user location in X Y Z coordinates
- an encoded image file from the user webcam
- any data, really

### 2. Video streaming

There is also a web streaming platform where a **single client** can stream it's video and audio feed to a streaming server and all the other clients will receive the video as a HSL (MP4 for streaming) feed.

> Video streaming is high-bandwith media channel with noticable delay (starting from ~7 seconds until ~30 seconds) so it's not great for two-way realtime communication but great for one-side communication with large audiences. There can be exceptions of course, audience <-> performer interaction could work in some cases.

We are using the same streamkey for all the URLS and links. Here is the example where streamkey is `residence`:

#### Video stream upload (ingest)

Stream URL: `rtmp://165.227.149.4:1935/stream`
Streamkey: `residence`

#### Video stream download (broadcast)

`https://stream.elektron.studio:8443/live/residence.m3u8`

#### Event page with video stream

https://elektron.live/residence

## Getting out the stream

(ask for a full URL in residence chat)

## Example client code

There are several codebases and code examples that connect to the elektron.live messaging and broadcasting servers.
