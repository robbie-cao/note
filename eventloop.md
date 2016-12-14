# Event Loop

In computer science, the **event loop**, **message dispatcher**, **message loop**, **message pump**, or **run loop** is a programming construct that waits for and dispatches events or messages in a program.

It works by making a request to some internal or external "event provider" (that generally blocks the request until an event has arrived), and then it calls the relevant event handler ("dispatches the event").

The event-loop may be used in conjunction with a reactor, if the event provider follows the file interface, which can be selected or 'polled' (the Unix system call, not actual polling).

The event loop almost always operates asynchronously with the message originator.

![](http://berb.github.io/diploma-thesis/original/resources/ev-server.svg)

![](http://michaelkuty.github.io/vertx-gdg/img/eventloop.png)

![](https://softwareengineeringdaily.com/wp-content/uploads/2015/07/event-loop.jpg)

![](https://scr.sad.supinfo.com/articles/resources/164862/2204/1.png)

## libevent

## libev

## libuv

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



## Reference

- https://en.wikipedia.org/wiki/Event_loop
