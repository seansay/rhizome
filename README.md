[![Build Status](https://travis-ci.org/sebpiq/rhizome.png)](https://travis-ci.org/sebpiq/rhizome)

rhizome
=========

**rhizome** is a web server for participative performances and installations.

**rhizome** is a solution for transmitting messages from **OSC** to a **web page** and back, therefore allowing you to control the user's devices with your installation, or allowing the participants to control your installation with their smartphones, computers or tablets **(2)**, **(3)**.

**rhizome** can also serve static content **(1)** (HTML, JavaScript files, images ...). 

![rhizome](https://raw2.github.com/sebpiq/rhizome/master/images/schema.png)

While **rhizome** provides you with a solid architecture for communication, you still have to implement what's on both ends of the chain :

- *the installation / performance setup*. It can be implemented with anything that supports **OSC** messaging (Pure Data, SuperCollider, openFrameworks, ...).

- *the web page*. It should be implemented with **JavaScript** and **HTML**. **rhizome** comes with a JavaScript client handling all the communication for you. So you shouldn't have to worry about this, and instead, focus on implementing a nice user interface / cool visuals / cool sounds.


Status of the project
----------------------

This project is brand new, and it is currently under heavy development. There is currently no documentation as the API is not yet stable.

In the next few days, the situation should improve and I will update the examples. Meanwhile, don't hesitate to contact me if you have any questions. 


Getting started
-----------------

##### 1) Install Node.js and npm

The simplest and nicest way to do this is probably by installing [nvm](https://github.com/creationix/nvm). You can also download an installer directly from [Node.js website](http://nodejs.org/download/).


##### 2) Install rhizome

Open a terminal, and simply run `npm install -g rhizome-server`. If this succeeded, you can try to run `rhizome`. This should print **rhizome** help message.


##### 3) Implement your thing 

More documentation will come soon. But for the moment, you can check-out the [examples](https://github.com/sebpiq/rhizome/tree/master/examples).


##### 4) That's it!

Please if you have any feedback, any problem, if you need help, don't hesitate to drop a message in the [issue tracker](https://github.com/sebpiq/rhizome/issues).

Also, if you would like to share your projects realized with **rhizome**, please contact me, or add them directly in the gallery!


Gallery
-----------

**rhizome** was used to realize the following projects :

- *The Projectionist Orchestra*. Live audio-visual performance, where the audience can control sound and visuals with their smartphones.
- *Fields*. Diffusion of field recordings through the smartphones from people in the audience. The connected devices become a giant granular synthesizer that the performers can manipulate live with a midi controller.


Transferring files
-------------------

**rhizome** supports transferring [OSC blobs](http://opensoundcontrol.org/spec-1_0) and [JavaScript blobs](https://developer.mozilla.org/en-US/docs/Web/API/Blob) without any problem. This means that you can transfer files (audio, images, ...) between your OSC application and the web page.

However, some OSC applications have bad support for OSC blobs (for example Pure Data). To solve this problem, **rhizome** comes with a tool that can handle the transfer for you. To see how to use it, check-out [this example](https://github.com/sebpiq/rhizome/tree/master/examples/drawing-wall).


For contributors
------------------


#### Activate logging

```
export DEBUG=rhizome.*
```


#### Running tests and code coverage

You need to install *mocha* for running the tests and *istanbul* for the test coverage : 

```
npm install -g mocha
npm install -g istanbul
```

Then from the root folder of the project, run tests like so :

```
mocha --recursive
```

And generate a coverage report like so :

```
istanbul cover _mocha -- test --recursive
```


Changelog
-----------

- 0.3.1

  - Server:
    - now sends messages to `/broadcast/websockets/open` and `/broadcast/websockets/open` when a websocket connection is opened or closed

  - Web client:
    - throws an error if trying to send invalid args

- 0.3.0

  - App clients:
    - clients must now subscribe by sending to `/sys/subscribe`
    - to send a blob, now clients must send to `/sys/blob`

  - Web client:
    - blobs are now handled like any other argument
    - can now both send and receive blobs
    - `message` renamed to `send`
    - `listen` renamed to `subscribe`

  - Bins:
    - config is now validated and displayed when starting the binaries

- 0.2.0 

  - Web client:
    - removed `blob`, now blob sent with `message`
    - renamed `client.config.retry` to `client.config.reconnect`

  - Blob client for sending blobs web client <-> OSC
  - Added address validation

- 0.1.1 
  - Fixed bugs with retry
  - In web-client : added `client.status()`

- 0.1.0 Initial release
