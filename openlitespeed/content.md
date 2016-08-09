
# What is OpenLiteSpeed?

OpenLiteSpeed is a high-performance, lightweight, open source HTTP server developed and copyrighted by LiteSpeed Technologies. Users are free to download, use, distribute, and modify OpenLiteSpeed and its source code in accordance with the precepts of the GPLv3 license.

> [wikipedia.org/wiki/LiteSpeed_Technologies_Inc.#OpenLiteSpeed](https://en.wikipedia.org/wiki/LiteSpeed_Technologies_Inc.#OpenLiteSpeed)

![logo](https://github.com/litespeedtech/docker-library-docs/blob/add_openlitespeed/openlitespeed/logo.png)

# How to use this image

## hosting static content or php sites

```console
$ docker run --name my-ols -v /site/content/dir:/usr/local/lsws/Example/html:rw -d openlitespeed 
```

Alternatively, a simple `Dockerfile` can be used to generate a new image that includes the necessary content (which is a cleaner solution than the bind mount above):

```dockerfile
FROM openlitespeed
COPY my-site-directory /usr/local/lsws/Example/html
```

Place this file in the same directory as your directory of content ("my-site-directory"), run `docker build -t my-customized-openlitespeed.`, then start your container:

```console
$ docker run --name my-ols -d my-customized-openlitespeed
```

## exposing the port

```console
$ docker run --name my-ols -d -p 80:80 -p 7080:7080 my-customized-openlitespeed
```

Then you can hit `http://host-ip` in your browser for the site content and `https://host-ipi:7080` for the OLS WebAdmin interface.
The initial credential for admin is admin/123456, please log into WebAdmin and change it accordingly.


## complex configuration

```console
$ docker run --name my-ols -v /my/ols/confile:/usr/local/lsws/conf/httpd_config.conf:rw -d openlitespeed
```

For information on the configuration guide of OpenLiteSpeed, please refer to [the OpenLiteSpeed configuration guides page](http://open.litespeedtech.com/mediawiki/index.php/Help:Configuration) 


If you wish to adapt the default configuration, use something like the following to copy it from a running OpenLiteSpeed container:

```console
$ docker cp my-ols:/usr/local/lsws/conf/httpd_config.conf /my/own/ols/httpd_config.conf
```

As above, this can also be accomplished more cleanly using a simple `Dockerfile`:

```dockerfile
FROM openlitespeed
COPY httpd_config.conf /usr/local/lsws/conf/httpd_config.conf
```

Then, build with `docker build -t my-customized-openlitespeed.` and run:

```console
$ docker run --name my-ols -d my-customized-openlitespeed
```
