# ZeroMQ

**ZeroMQ** (also spelled **ØMQ**, **0MQ** or **ZMQ**) is a high-performance asynchronous messaging library, aimed at use in distributed or concurrent applications. It provides a message queue, but unlike message-oriented middleware, a ZeroMQ system can run without a dedicated message broker. The library's API is designed to resemble that of Berkeley sockets.

The ZeroMQ API provides sockets (a kind of generalization over the traditional IP and Unix domain sockets), each of which can represent a many-to-many connection between endpoints. Operating with a message-wise granularity, they require that a messaging pattern be used, and are particularly optimized for that kind of pattern.

The basic ZeroMQ patterns are:

- Request–reply

  Connects a set of clients to a set of services. This is a remote procedure call and task distribution pattern.

  ![](https://github.com/imatix/zguide/raw/master/images/fig2.png)

- Publish–subscribe

  Connects a set of publishers to a set of subscribers. This is a data distribution pattern.

  ![](https://github.com/imatix/zguide/raw/master/images/fig4.png)

- Push–pull (pipeline)

  Connects nodes in a fan-out / fan-in pattern that can have multiple steps, and loops. This is a parallel task distribution and collection pattern.

  ![](https://github.com/imatix/zguide/raw/master/images/fig5.png)

- Exclusive pair

  Connects two sockets in an exclusive pair. (This is an advanced low-level pattern for specific use cases.)

## Architecture

![](images/zmq-arch.png)

> http://www.cnblogs.com/rainbowzc/p/3357594.html

![](http://www.aosabook.org/images/zeromq/aosa9.png)

> http://www.aosabook.org/en/zeromq.html

## Process

![](images/zmq-process.png)

> http://www.cnblogs.com/rainbowzc/p/3357594.html

## Comparison

![](images/zmq-comp.png)

> http://www.cnblogs.com/rainbowzc/p/3357594.html

## Reference

- http://zeromq.org
- http://zeromq.org/community
- http://zguide.zeromq.org/page:all
- http://api.zeromq.org
- https://en.wikipedia.org/wiki/ZeroMQ
