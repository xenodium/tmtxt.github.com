---
layout: post
title: "Basic Logging & Debugging in Microservices - Part 3"
description: ""
categories: []
tags: []
thumbnail:
---

# ElasticSearch for storing the log data

At this time, you might have a good logging library that you built on your own. Your application
probably produced a bunch of log entries and you can debug your application using `cat` and `tail`
command. You can also open the log file in your favorite text editor and search for the log entries
that you want. However, there should be a better solution for that. Imagine when your log file grows
to thousands or millions or even billions of lines, that's not feasible to debug using the manual
way like that.

Fortunately, **ElasticSearch** is a good choice for organising all the log entries.
Setting up **ElasticSearch** is a quite straight forward
task. There is even pre-built docker image for it. Our team at AR doesn't even care about
optimising it because we rarely face the problem with it. Of course, our **ElasticSearch** instance
goes down sometimes, but since it's not a critical module of the system, doesn't affect main
application's status, we don't need to invest time on optimising it. What we do is to
setup restart policy so that Docker can recover the process after the OOM. Another thing we
need to do is to setup a script for deleting the old log entries to save the disk space. The
script is setup to run every day. You can find installation instruction for ElasticSearch on its
official Docker image page

- [ElasticSearch](https://hub.docker.com/_/elasticsearch/)

# fluentd for pushing the log data to ElasticSearch

Now you have an **ElasticSearch** server up and running. The next thing you need to do is to push
the log data to it. **fluentd**, an open source data collector for unified logging layer, allows you
to unify data collection and consumption for a better use and understanding of data. If your application
writes all the log entries into a file or to standard output from inside Docker,
you can setup **fluentd** to tail the log files and push to **ElasticSearch** every time one line is
finished. In case you don't know, Docker redirect the standard output to a file. You can find a
sample **fluentd** setup
here
[https://github.com/tmtxt/clojure-pedigree/tree/master/images/fluentd](https://github.com/tmtxt/clojure-pedigree/tree/master/images/fluentd).
The important thing that you need to notice is its configuration file, the `td-agent.conf` file. You
will need to modify it to fit your requirements

```xml
<source>
  type tail
  # configure the path to your log files here
  path /var/log/*.log
  pos_file /var/log/services.log.pos
  # other configurations
  ...
</source>

<match **>
   type elasticsearch
   log_level info
   include_tag_key true
   # configure the elastic-search connection here
   host log.elasticsearch
   port 9200
   # other configurations
   ...
</match>
```

# Kibana for searching and displaying the log

Everything is on track now, you will need an UI for searching and displaying all the log data.
**Kibana** is a simple solution that can serve all those requirements. Again, setting it up is an
extremely easy task, especially with Docker. Just pull it from the
[official Docker page](https://hub.docker.com/_/kibana/), start it with the environment variables
pointing to your running **ElasticSearch** server and you are done. Here are some sample images from
my personal project, quite nice, huh?

![Kibana](/files/2016-08-24-implement-a-simple-log-trace-in-clojure-ring/kibana1.png)

![Kibana](/files/2016-08-24-implement-a-simple-log-trace-in-clojure-ring/kibana2.png)

# Some Notes for Logging

Writing and organising the log, of course, take computer resources to perform.
