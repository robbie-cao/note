# D-Bus

## Overview

**D-Bus** is a message bus system, a simple way for applications to talk to one another. In addition to interprocess communication, D-Bus helps coordinate process lifecycle; it makes it simple and reliable to code a "single instance" application or daemon, and to launch applications and daemons on demand when their services are needed.

D-Bus supplies both a **system daemon** (for events such as "new hardware device added" or "printer queue changed") and a **per-user-login-session daemon** (for general IPC needs among user applications). Also, the message bus is built on top of a general one-to-one message passing framework, which can be used by any two apps to communicate directly (without going through the message bus daemon).

![](http://dbus.freedesktop.org/doc/diagram.png)

D-Bus is an Inter-Process Communication (IPC) and Remote Procedure Calling (RPC) mechanism specifically designed for efficient and easy-to-use communication between processes running on the same machine.

There are two primary use-cases for which D-Bus is designed:

- As a "system bus" for communicating between system applications and user sessions
- As a "session bus" for exhanging data between applications in a desktop environments

## Code Example

http://www.matthew.ath.cx/misc/dbus

## Reference

- https://www.freedesktop.org/wiki/Software/dbus/
- https://dbus.freedesktop.org/doc/dbus-specification.html
- https://pythonhosted.org/txdbus/dbus_overview.html
- https://www.freedesktop.org/wiki/IntroductionToDBus/
- https://en.wikipedia.org/wiki/D-Bus
- http://www.360doc.com/content/12/0810/09/168576_229347825.shtml
