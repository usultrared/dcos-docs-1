---
post_title: How to use NGINX
nav_title: NGINX
menu_order: 7
---

[NGINX](https://www.nginx.com) is a high-performance HTTP server, reverse proxy, and an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption. DC/OS allows you to quickly configure, install and manage NGINX. 

**Terminology**

- **Docker**: Docker is a piece of software that helps package an application with all of its dependencies into a standardized unit for software development.

**Scope**

In this tutorial you will learn:
* How to install NGINX on DC/OS to serve a static website

**Table of Contents**

## Prerequisites

- A running DC/OS cluster, with atleast 1 node having atleast 1 CPUs and 1 GB of RAM available.
- [DC/OS CLI](https://docs.mesosphere.com/usage/cli/install/) installed

### Installing NGINX to serve a static website

Assuming you have a DC/OS cluster up and running, we are going to install NGINX on DC/OS to serve up a [hello-nginx website](http://mesosphere.github.io/hello-nginx/). Let's get started by creating a file called `options.json` with following contents:

```json
{
  "nginx": {
    "cpus": 1,
    "mem": 1024,
    "bridge": true,
    "contentUrl":"https://github.com/mesosphere/hello-nginx/archive/master.zip",
    "contentDir":"hello-nginx-master/"
  }
}
```

Next, we are going to install nginx using this `options.json` file:

```bash
dcos package install nginx --options=options.json
```

Once you run above command, you'll see following output:

```bash
Preparing to install nginx.
Installing Marathon app for package [nginx] version [1.8.1]
Nginx is getting installed.
```

To verify that our NGINX instance is up and running, we can use `dcos task` command:

```bash
$ dcos task
NAME   HOST        USER  STATE  ID
nginx  10.0.0.161  root    R    nginx.b1e20ff3-0500-11e6-83da-8a8d57d7c81f
```

Let's try to access the hello-world website that our NGINX server is hosting by hitting the URL: http://<YOUR-DCOS-MASTER-HOSTNAME>/service/nginx. You should see a webpage similar to this:

![Hello World NGINX on DC/OS](img/hello-nginx-dcos.png)