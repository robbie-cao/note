# Logging

## Kernel logging

Kernel logging ecosystem and major components

![](http://www.ibm.com/developerworks/library/l-kernel-logging-apis/figure1.gif)

Kernel logging stack identifying the major components

![](http://www.ibm.com/developerworks/library/l-kernel-logging-apis/figure2.gif)

> http://www.ibm.com/developerworks/library/l-kernel-logging-apis/

> http://elinux.org/Debugging_by_printing

> http://lxr.free-electrons.com/source/include/linux/printk.h?v=3.3

## Syslog

In computing, `syslog` is a standard for message logging. It permits separation of the software that generates messages, the system that stores them, and the software that reports and analyzes them. Each message is labeled with a facility code, indicating the software type generating the message, and assigned a severity label.

Syslog is used on UNIX, Linux and BSD based operating systems as the default mechanism for logging.

![](http://1.bp.blogspot.com/-7isWLJSi_Eg/T73KindfCaI/AAAAAAAAAik/YnL0RQ_3-qI/s1600/syslog.png)

The information provided by the originator of a syslog message includes the facility code and the severity level. The syslog software adds information to the information header before passing the entry to the syslog receiver. Such components include an originator process ID, a timestamp, and the hostname or IP address of the device.

> https://en.wikipedia.org/wiki/Syslog

> http://man7.org/linux/man-pages/man3/syslog.3.html

> https://linux.die.net/man/8/syslogd

> https://tools.ietf.org/html/rfc5424

## Android Logging System

The Android system has a logging facility that allows system-wide logging of information, from applications and system components. This is separate from the Linux kernel's own logging system, which is accessed using 'dmesg' or '/proc/kmsg'.

The logging system consists of:

- a kernel driver and kernel buffers for storing log messages
- C, C++ and Java classes for making log entries and for accessing the log messages
- a standalone program for viewing log messages (`logcat`)
- ability to view and filter the log messages from the host machine (via eclipse or `ddms`)

![](http://elinux.org/images/c/c9/Android-logging-kmc-kobayashi.png)

> http://elinux.org/Android_Logging_System

## Apache Logging Services - Log4j

Apache Log4j is a Java-based logging utility.

![](http://logging.apache.org/log4j/2.x/images/Log4jClasses.jpg)

The following table defines the built-in log levels and messages in Log4j, in decreasing order of severity. The left column lists the log level designation in Log4j and the right column provides a brief description of each log level.

Level |	Description
------|-------------
OFF	  | The highest possible rank and is intended to turn off logging.
FATAL	| Severe errors that cause premature termination. Expect these to be immediately visible on a status console.
ERROR	| Other runtime errors or unexpected conditions. Expect these to be immediately visible on a status console.
WARN	| Use of deprecated APIs, poor use of API, 'almost' errors, other runtime situations that are undesirable or unexpected, but not necessarily "wrong". Expect these to be immediately visible on a status console.
INFO	| Interesting runtime events (startup/shutdown). Expect these to be immediately visible on a console, so be conservative and keep to a minimum.
DEBUG	| Detailed information on the flow through the system. Expect these to be written to logs only. Generally speaking, most lines logged by your application should be written as DEBUG.
TRACE	| Most detailed information. Expect these to be written to logs only. Since version 1.2.12.[11]

> http://logging.apache.org/log4j/2.x/

> http://logging.apache.org/log4j/2.x/manual/architecture.html

> https://en.wikipedia.org/wiki/Log4j

## Windows Event Tracing

> https://msdn.microsoft.com/en-us/library/aa964766(v=VS.85).aspx

![](https://blogs.endjin.com/wp-content/uploads/2014/04/etw-architecture_thumb.gif)

> https://blogs.endjin.com/2014/04/getting-started-with-semantic-logging/

![](http://cdn.ttgtmedia.com/rms/misc/event_tracing_fig1.JPG)

> http://searchwindowsserver.techtarget.com/tip/Event-Tracing-for-Windows-A-fresh-look-at-an-old-tool

![](http://windowsitpro.com/content/content/40707/figure_01.gif)

> http://windowsitpro.com/systems-management/inside-event-tracing-windows
