# Using `libubox`, `ubus` and `uci` on Ubuntu

## `libubox`

```
$ git clone git://git.openwrt.org/project/libubox.git
$ cd libubox

$ cmake .
-or-
$ cmake -f CMakeLists.txt

$ make
$ sudo make install
```

## `ubus`

```
$ git clone git://git.openwrt.org/project/ubus.git
$ cd ubus
$ cmake -f CMakeLists.txt
$ make
$ sudo make install
```

## `uci`

```
$ git clone git://git.openwrt.org/project/uci.git
$ cd uci
$ cmake .
$ make
$ sudo make install
$ sudo ldconfig
```

> https://wiki.openwrt.org/doc/techref/uci

## Sample Code

**`uloop`**

```c
// uloop-timer.c
#include <stdio.h>
#include <sys/time.h>
#include <unistd.h>

#include <libubox/uloop.h>

static void timer_cb(struct uloop_timeout *timeout)
{
    static int i = 0;

        fprintf(stderr, "%d - %d\n", __LINE__, i++);

        uloop_timeout_set(timeout, 1000);
}

static struct uloop_timeout timer = {
        .cb = timer_cb,
};

int main(int argc, char **argv)
{
    uloop_init();

    uloop_timeout_set(&timer, 2000);

    uloop_run();

    uloop_done();

    return 0;
}
```

Compile with:

```
$ gcc uloop-timer.c -lubox -o uloop-timer
```

**`ubus`**

```c
// ubus-sample.c

#include <unistd.h>
#include <signal.h>
#include <stdio.h>

#include <libubox/uloop.h>
#include <libubox/blobmsg_json.h>
#include <libubus.h>

static struct ubus_context *ctx;
static struct blob_buf b;

static int value = 0;

static int
status_handler(struct ubus_context *ctx, struct ubus_object *obj,
        struct ubus_request_data *req, const char *method,
        struct blob_attr *msg)
{
    blob_buf_init(&b, 0);
    blobmsg_add_string(&b, "result", "ok");
    blobmsg_add_u16(&b, "value", value);

    ubus_send_reply(ctx, req, b.head);

    return 0;
}

enum {
    ADD_VALUE,
    __ADD_MAX
};

static const struct blobmsg_policy add_policy[__ADD_MAX] = {
    [ADD_VALUE] = { .name = "value", .type = BLOBMSG_TYPE_INT16 },
};

static int add_handler(struct ubus_context *ctx, struct ubus_object *obj,
        struct ubus_request_data *req, const char *method,
        struct blob_attr *msg)
{
    struct blob_attr *tb[__ADD_MAX];
    int v = 0;

    blobmsg_parse(add_policy, __ADD_MAX, tb, blob_data(msg), blob_len(msg));
    if (!tb[ADD_VALUE]) {
        return UBUS_STATUS_INVALID_ARGUMENT;
    }

    v = blobmsg_get_u16(tb[ADD_VALUE]);
    value += v;

    blob_buf_init(&b, 0);
    blobmsg_add_string(&b, "result", "ok");
    blobmsg_add_u16(&b, "add", v);
    blobmsg_add_u32(&b, "value", value);
    ubus_send_reply(ctx, req, b.head);

    return 0;
}

static const struct ubus_method methods[] = {
    { .name = "status" , .handler = status_handler } ,
    UBUS_METHOD("add", add_handler, add_policy),
};

static struct ubus_object_type sample_object_type = UBUS_OBJECT_TYPE("sample", methods);

static struct ubus_object smaple_object = {
    .name = "sample",
    .type = &sample_object_type ,
    .methods = methods,
    .n_methods = ARRAY_SIZE(methods),
};


int main(int argc, char **argv)
{
    const char *ubus_socket = NULL;
    int ret;
    int ch;

    while ((ch = getopt(argc, argv, "cs:")) != -1) {
        switch (ch) {
        case 's':
            ubus_socket = optarg;
            break;
        default:
            break;
        }
    }

    argc -= optind;
    argv += optind;

    uloop_init();
    signal(SIGPIPE, SIG_IGN);

    ctx = ubus_connect(ubus_socket);
    if (!ctx) {
        fprintf(stderr, "Failed to connect to ubus\n");
        return -1;
    }

    ubus_add_uloop(ctx);

    ret = ubus_add_object(ctx, &smaple_object);
    if (ret) {
        fprintf(stderr, "Failed to add object: %s\n", ubus_strerror(ret));
    }
    uloop_run();

    ubus_free(ctx);
    uloop_done();

    return 0;
}
```

Compile with:

```
$ gcc ubus-sample.c -lubox -lubus -o ubus-sample
```

Run:

```
$ sudo ubusd &
$ sudo ./ubus-sample

# in another shell
$ sudo ubus call sample status
$ sudo ubus call add '{"value" : 1234}'
```

## Reference

