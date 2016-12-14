# Event Loop

In computer science, the **event loop**, **message dispatcher**, **message loop**, **message pump**, or **run loop** is a programming construct that waits for and dispatches events or messages in a program.

It works by making a request to some internal or external "event provider" (that generally blocks the request until an event has arrived), and then it calls the relevant event handler ("dispatches the event").

The event-loop may be used in conjunction with a reactor, if the event provider follows the file interface, which can be selected or 'polled' (the Unix system call, not actual polling).

The event loop almost always operates asynchronously with the message originator.

![](http://berb.github.io/diploma-thesis/original/resources/ev-server.svg)

![](http://michaelkuty.github.io/vertx-gdg/img/eventloop.png)

![](https://softwareengineeringdaily.com/wp-content/uploads/2015/07/event-loop.jpg)

![](https://scr.sad.supinfo.com/articles/resources/164862/2204/1.png)

## `libevent`

A software library that provides asynchronous event notification.

![](http://www.cppblog.com/images/cppblog_com/xguru/libevent1.jpg)

The `libevent` API provides a mechanism to execute a callback function when a specific event occurs on a file descriptor or after a timeout has been reached. `libevent` also supports callbacks triggered by signals and regular timeouts.

Programs using `libevent`:
<ul>
<li><a href="http://www.chromium.org/Home">Chromium</a> &ndash; Google's open-source web browser (uses Libevent on Mac and Linux)</li>
<li><a href="http://www.memcached.org">Memcached</a> &ndash; a high-performance, distributed memory object caching system</li>
<li><a href="http://www.transmissionbt.com/">Transmission</a> &ndash; a fast, easy, and free BitTorrent client</li>
<li><a href="http://www.ntp.org">NTP</a> &ndash; the network time protocol that makes your clock right (uses Libevent in SNTP)</li>
<li><a href="http://tmux.sourceforge.net">tmux</a> &ndash; A clean, modern, BSD-licensed terminal multiplexer, similar to GNU screen</li>
<li><a href="https://www.torproject.org/">Tor</a> &ndash; an anonymous Internet communication system.</li>
<li><a href="https://github.com/ellzey/libevhtp">libevhtp</a> &ndash; A fast and flexible replacement for libevent's httpd API</li>
<li><a href="http://prosody.im/">Prosody</a> &ndash; A Jabber/XMPP server written in Lua</li>
<li><a href="http://wiki.postgresql.org/wiki/PgBouncer">PgBouncer</a> &ndash; Lightweight connection pooler for PostgreSQL</li>
<li><a href="http://darkk.net.ru/redsocks/">redsocks</a> &ndash; a simple transparent TCP -> Socks5/HTTPS proxy daemon.</li>
<li><a href="http://monkey.org/~provos/vomit/">Vomit</a> &ndash; Voice Over Misconfigured Internet Telephones</li>
<li><a href="http://monkey.org/~provos/crawl/">Crawl</a> &ndash; A Small and Efficient HTTP Crawler</li>
<li><a href="http://monkey.org/~provos/libio/">Libio</a> &ndash; an input/output abstraction library</li>
<li><a href="http://www.honeyd.org/">Honeyd</a> &ndash; a virtual honeynet daemon &ndash; can be used to <a href="http://www.honeyd.org/worms.php">fight Internet worms</a>.</li>
<li><a href="http://www.monkey.org/~dugsong/fragroute/">Fragroute</a> &ndash; an IDS testing tool</li>
<li><a href="http://monkey.org/~marius/nylon/">Nylon</a> &ndash; nested proxy server</li>
<li><a href="http://monkey.org/~provos/disconcert/">Disconcert</a> &ndash; a Distributed Computing Framework for Loosely-Coupled Workstations.</li>
<li><a href="http://monkey.org/~marius/trickle/">Trickle</a> &ndash; a lightweight userspace bandwidth shaper.</li>
<li><a href="http://oss.digirati.com.br/watchcatd/">watchcatd</a> &ndash;software watchdog designed to take actions not as drastic as the usual solutions, which reset the machine.</li>
<li><a href="http://monkey.org/~provos/scanssh/">ScanSSH</a> &ndash; a fast SSH server and open proxy scanner.</li>
<li><a href="http://www.honeyd.org/tools.php#nttlscan">Nttlscan</a> &ndash; a network topology scanner for Honeyd.</li>
<li><a href="http://nch.sourceforge.net/">NetChat</a> &ndash; a combination of netcat and ppp's chat.</li>
<li><a href="http://www.iolanguage.com/">Io</a> &ndash; a small programming language; uses libevent for network communication.</li>
<li><a href="http://www.systrace.org/">Systrace</a> &ndash; a system call sandbox.</li>
<li><a href="http://www.spybye.org/">SpyBye</a> &ndash; detect malware on web pages.</li>
<li><a href="http://www.greensql.net/">GreenSQL</a> &ndash; an SQL database firewall.</li>
<li><a href="http://monkey.org/~provos/dnsscan/">dnsscan</a> &ndash;  a fast scanner for identifying open recursive dns resolvers</li>
<li><a href="http://code.google.com/p/kargo-event/">Kargo Event</a> &ndash; a PHP extension for libevent.</li>
<li><a href="http://maximelabelle.bitbucket.org/">Scytale</a> &ndash; a database encryption tool.</li>
</ul>

> http://libevent.org

![](http://my.csdn.net/uploads/201205/25/1337938985_6431.jpg)

## `libev`

A full-featured and high-performance event loop that is loosely modelled after `libevent`, but without its limitations and bugs.

It supports eight event types:

- I/O
- real time timers
- wall clock timers
- signals
- child status changes
- idle
- check
- prepare handlers

It uses a priority queue to manage timers and uses arrays as fundamental data structure. It has no artificial limitations on the number of watchers waiting for the same event. It offers an emulation layer for libevent and optionally the same DNS, HTTP and buffer management (by reusing the corresponding libevent code through its emulation layer).

It is used in:

- [GNU Virtual Private Ethernet](http://software.schmorp.de/pkg/gvpe.html)
- [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html)
- [auditd](http://people.redhat.com/sgrubb/audit/)
- the [Deliantra MORPG](http://www.deliantra.net) Server and Client
- many other programs

> https://github.com/facebook/hhvm/issues/2047

```
// a single header file is required
#include <ev.h>

#include <stdio.h> // for puts

// every watcher type has its own typedef'd struct
// with the name ev_TYPE
ev_io stdin_watcher;
ev_timer timeout_watcher;

// all watcher callbacks have a similar signature
// this callback is called when data is readable on stdin
static void
stdin_cb (EV_P_ ev_io *w, int revents)
{
  puts ("stdin ready");
  // for one-shot events, one must manually stop the watcher
  // with its corresponding stop function.
  ev_io_stop (EV_A_ w);

  // this causes all nested ev_run's to stop iterating
  ev_break (EV_A_ EVBREAK_ALL);
}

// another callback, this time for a time-out
static void
timeout_cb (EV_P_ ev_timer *w, int revents)
{
  puts ("timeout");
  // this causes the innermost ev_run to stop iterating
  ev_break (EV_A_ EVBREAK_ONE);
}

int
main (void)
{
  // use the default event loop unless you have special needs
  struct ev_loop *loop = EV_DEFAULT;

  // initialise an io watcher, then start it
  // this one will watch for stdin to become readable
  ev_io_init (&stdin_watcher, stdin_cb, /*STDIN_FILENO*/ 0, EV_READ);
  ev_io_start (loop, &stdin_watcher);

  // initialise a timer watcher, then start it
  // simple non-repeating 5.5 second timeout
  ev_timer_init (&timeout_watcher, timeout_cb, 5.5, 0.);
  ev_timer_start (loop, &timeout_watcher);

  // now wait for events to arrive
  ev_run (loop, 0);

  // break was called, so exit
  return 0;
}
```

## `libuv`

A multi-platform support library with a focus on asynchronous I/O.

![](http://docs.libuv.org/en/v1.x/_images/architecture.png)

It was primarily developed for use by [Node.js](http://nodejs.org/), but it's also used by Mozilla's [Rust language](http://www.rust-lang.org/), [Luvit](http://luvit.io/), [Julia](http://julialang.org/), [pyuv](https://crate.io/packages/pyuv/), and [others](https://github.com/libuv/libuv/wiki/Projects-that-use-libuv).

![](https://pbs.twimg.com/media/Bt5ywJrIEAAKJQt.jpg)

Features:

- Full-featured event loop backed by epoll, kqueue, IOCP, event ports.
- Asynchronous TCP and UDP sockets
- Asynchronous DNS resolution
- Asynchronous file and file system operations
- File system events
- ANSI escape code controlled TTY
- IPC with socket sharing, using Unix domain sockets or named pipes (Windows)
- Child processes
- Thread pool
- Signal handling
- High resolution clock
- Threading and synchronization primitives

`libuv` (https://github.com/joyent/libuv) is a lightweight library which allows asynchronous IO across OpenBSD, Linux, Darwin, Windows etc by utilizing the fastest implementation on each system (`epoll`, `kqueue`, IOCP, event ports). These specialized IO polling methods are much faster on their respective platforms than just using `select()` like the RTS currently does.

Additionally, it also provides cross platform threads, mutex, condition vars, terminal input/output and term settings w/ cross platform ANSI escape code handling, thread pools, cross platform HRC's etc. It's currently significantly faster than `libevent` and slightly faster than `libev`. Because it's maintained and utilized heavily by **Node.js** it's in extremely active and maintained development.

> https://github.com/facebook/hhvm/issues/2047

> http://nikhilm.github.io/uvbook/

## GLib Event Loop

The GLib event loop manages all the sources of an event available for GLib. These events can come from different kinds of sources like file descriptors (plain file descriptors, sockets, or pipes), time-outs, or any kind of source that can be added.

![](https://developer.gnome.org/glib/stable/mainloop-states.gif)

Example:

```
#include <glib.h>
gboolean timeout_callback(gpointer data)
{
    static int i = 0;

    i++;
    g_print("timeout_callback called %d times\n", i);
    if (10 == i)
    {
        g_main_loop_quit( (GMainLoop*)data );
        return FALSE;
    }

    return TRUE;
}

int main()
{
    GMainLoop *loop;

    loop = g_main_loop_new ( NULL , FALSE );

    // add source to default context
    g_timeout_add (100 , timeout_callback , loop);
    g_main_loop_run (loop);
    g_main_loop_unref(loop);

    return 0;
}
```

> http://devlib.symbian.slions.net/s3/GUID-7FD05006-09C1-4EF4-A2EB-AD98C2FA8866.html

> https://developer.gnome.org/glib/stable/glib-The-Main-Event-Loop.html

## Qt Event Loop

## Boost ASIO

> http://www.slideshare.net/lukejfluo/phase1-45781850

## Reference

- https://en.wikipedia.org/wiki/Event_loop
- http://libevent.org
- http://www.wangafu.net/~nickm/libevent-book/
- http://libuv.org
- http://docs.libuv.org/en/v1.x/
- http://software.schmorp.de/pkg/libev.html
- http://pod.tst.eu/http://cvs.schmorp.de/libev/ev.pod
