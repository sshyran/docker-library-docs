# Supported tags and respective `Dockerfile` links

-	[`latest`, `1`, `1.4`, `1.4.21` (*stable/jessie/Dockerfile*)](https://github.com/litespeedtech/docker-ols/blob/e4891aae2499fe41604b81106ee48044e8dc372c/stable/jessie/Dockerfile)

[![](https://badge.imagelayers.io/openlitespeed:latest.svg)](https://imagelayers.io/?images=openlitespeed:latest)

For more information about this image and its history, please see [the relevant manifest file (`library/openlitespeed`)](https://github.com/docker-library/official-images/blob/master/library/openlitespeed). This image is updated via [pull requests to the `docker-library/official-images` GitHub repo](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Fopenlitespeed).

For detailed information about the virtual/transfer sizes and individual layers of each of the above supported tags, please see [the `openlitespeed/tag-details.md` file](https://github.com/docker-library/docs/blob/master/openlitespeed/tag-details.md) in [the `docker-library/docs` GitHub repo](https://github.com/docker-library/docs).

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


# Supported Docker versions

This image is officially supported on Docker version 1.11.1.

Support for other versions is provided on a best-effort basis.

Please see [the Docker installation documentation](https://docs.docker.com/installation/) for details on how to upgrade your Docker daemon.

# User Feedback

## Documentation

Documentation for this image is stored in the [`openlitespeed/` directory](https://github.com/docker-library/docs/tree/master/openlitespeed) of the [`docker-library/docs` GitHub repo](https://github.com/docker-library/docs). Be sure to familiarize yourself with the [repository's `README.md` file](https://github.com/docker-library/docs/blob/master/README.md) before attempting a pull request.

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/litespeedtech/docker-ols/issues). If the issue is related to a CVE, please check for [a `cve-tracker` issue on the `official-images` repository first](https://github.com/docker-library/official-images/issues?q=label%3Acve-tracker).

You can also reach many of the official image maintainers via the `#docker-library` IRC channel on [Freenode](https://freenode.net).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/openlitespeed/docker-ols/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
