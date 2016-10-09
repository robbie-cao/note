# Logging

## Syslog

In computing, `syslog` is a standard for message logging. It permits separation of the software that generates messages, the system that stores them, and the software that reports and analyzes them. Each message is labeled with a facility code, indicating the software type generating the message, and assigned a severity label.

![](http://1.bp.blogspot.com/-7isWLJSi_Eg/T73KindfCaI/AAAAAAAAAik/YnL0RQ_3-qI/s1600/syslog.png)

The information provided by the originator of a syslog message includes the facility code and the severity level. The syslog software adds information to the information header before passing the entry to the syslog receiver. Such components include an originator process ID, a timestamp, and the hostname or IP address of the device.

> https://en.wikipedia.org/wiki/Syslog

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
