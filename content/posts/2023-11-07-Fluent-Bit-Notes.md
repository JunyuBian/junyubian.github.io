---
title: Fluent Bit Client Notes
date: 2023-11-07 21:53:43
categories: 
- Notes
tags:
- Fluent-bit
- Logging
---

# What is Fluent Bit

One day, the Insurance Management System Tom built crashed. Good news is the system recovered through rebooting, bad news is Tom did not know what had gone wrong. Tom's dad comes by and says to Tom "Fluent Bit is a telemetry agent designed to collect and process telemetry data from constrained systems to cloud infrastructures. Why don't you give it a try?"

# Structural Sketch

Tom is a good listener. He listened to his dad and checked the Fluent Bit website https://docs.fluentbit.io, and found one great picture shows the rough structure of Fluent Bit:
![Structural Sketch](https://github.com/JunyuBian/PicsForBlogs/blob/main/iShot_2023-11-08_22.24.51.png)

# How to Set it Up

Tom told his dad there're two different methods to config Fluent Bit:

## Through Config File

Fluent Bit could use config file to set Input sources, Filters, Output destinations, etc. Sample config file, which locates in `/etc/fluent-bit/fluent-bit.conf` by default:

``` 
[INPUT]
    Name    forward
    Listen  0.0.0.0
    Port    24224
    Tag     sampleTag

[FILTER]
    Name    rewrite_tag
    Match   sampleTag
    Rule    $name ^\/.+[-_]([a-z\-]+)[-_][0-9]+$ esp-$1 false

[OUTPUT]
    Name    stdout
    Match   *
```

To use a specific config file instead of the default one, we could use this command: `bin/fluent-bit -c example.conf`, `-c` will indicate a new config file.

## Though Command Line Parameters

Instead of a config file, we could directly reveal INPUTs, FILTERs and OUTPUTs in command line, one example would be:

```
bin/fluent-bit -i systemd \
        -p systemd_filter=_SYSTEMD_UNIT=docker.service \
        -p tag='sampletag' \
        -o forward://${fording_server}:24224
```

# Other Notes

While using fluent-bit, Tom also found it has below characteristics:
1. It could recive forwarded logs from other fluent-bit client, and together forward or output to other destinations.
2. If we're going to install two deb packages including fluent-bit on one same machine, it may incur resource race. Since both fluent-bit will leverage `/etc/fluent-bit/fluent-bit.conf`. One way to resolve this is, ask one of the client to use different config file or passing config through command line, and while installing the other client, adding `--force-overwrite`.

Tom is not complete happy, he thinks there should be more to discover for this topic.