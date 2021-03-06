Building Distributed Systems with Node.js and ØMQ
=============

VIDEO! [Building Distributed Systems with Node.js and ØMQ](https://www.youtube.com/watch?v=zgDjaJdAB9c)

A talk for [Node.js in the Wild](http://www.meetup.com/Node-js-in-the-wild/events/188786272/)

## whoami

* Jim R. Wilson
* author: [Node.js the Right Way](http://pragprog.com/book/jwnode/node-js-the-right-way) ([on Amazon](http://www.amazon.com/Node-js-Right-Way-Server-Side-JavaScript/dp/1937785734))
* github: [jimbojw](https://github.com/jimbojw)
* twitter: [@hexlib](https://twitter.com/hexlib)

## Talk Roadmap

* Why ØMQ?
* Installing ØMQ (skip)
* Naive publish/subscribe using Sockets
* PUB/SUB
* REQ/REP
* DEALER/ROUTER
* PUSH/PULL
* Questions?

## Why ØMQ?

* Distributed
* Low latency, low-overhead
* Event driven, non-blocking
* Patterns!
* Scalability / Philosophy of Ø

## The Network Onion

* Application, Presentation, Session
 * SSL, HTTP, SMTP, ØMQ
* Transport --- TCP, UDP
* Network --- IP
* Data Link --- MAC
* Physical --- wires

## Installing ØMQ

Mac OSX

```sh
brew install zmq
```

Ubuntu

```sh
sudo apt-get install libtool autoconf automake uuid-dev build-essential
wget http://download.zeromq.org/zeromq-3.2.2.tar.gz
tar zxvf zeromq-3.2.2.tar.gz && cd zeromq-3.2.2
./configure
make
sudo make install
```

Testing the base library.

```sh
man zmq
```

Install the zmq node module.

```sh
npm install zmq
```

Testing the module.

```sh
node --harmony -p -e 'require("zmq")'
```

First pass at troubleshooting (update system library cache):

```sh
sudo ldconfig
```

## Naive PUB/SUB with Sockets

Beacon application: fires an event once a second.

```js
{
  "pid": 12345,
  "timestamp": 1404168475695
}
```

PUB program: [net-beacon-pub.js](net-beacon-pub.js)

SUB program: [net-beacon-sub.js](net-beacon-sub.js)

## What's Wrong With That?

* Listener bias.
* Fault intolerant.
* Leaky buffers.
* Directionality (Publisher = Listener).

## PUB/SUB with ØMQ

Same beacon application.

PUB program: [zmq-beacon-pub.js](zmq-beacon-pub.js)

SUB program: [zmq-beacon-sub.js](zmq-beacon-sub.js)

## REQ/REP with ØMQ

Application requests the current time.

REP program: [zmq-time-rep.js](zmq-time-rep.js)

REQ program: [zmq-time-req.js](zmq-time-req.js)

## DEALER/ROUTER cluster with ØMQ

DEALER = parallel REQ

ROUTER = parallel REP

![Figure of REP cluster using DEALER/ROUTER](rep-cluster.png)

Cluster responds to time requests just like the previous example.

REP cluster program: [zmq-time-rep-cluster.js](zmq-time-rep-cluster.js)

## PUSH/PULL with ZMQ

Simple work queue using PUSH/PULL.

PUSH program: [zmq-work-push.js](zmq-work-push.js)

PULL program: [zmq-work-pull.js](zmq-work-pull.js)

Cluster to demonstrate the First Joiner problem.

PULL cluster program: [zmq-work-pull-cluster.js](zmq-work-pull-cluster.js)

## Wrap Up

* Why ØMQ?
* PUB/SUB
* REQ/REP
* DEALER/ROUTER
* PUSH/PULL

## Thank You!

For your kind attention.

## Questions?

If there are any?

