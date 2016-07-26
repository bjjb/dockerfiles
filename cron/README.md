# cron in a box

A small [Alpine][] box with [apk-cron][]. Exposes the `/etc/crontabs/` and
`/etc/periodic/`, so you can tell it what to do. Runs in UTC.

## Usage

You'll probably want a cron daemon running, so that's what it does by default.

    docker run -d bjjb/cron

That's not much good by itself, as it will do exactly nothing (since its
crontab is empty, and even if it weren't, there's not a lot you can do
periodically on a bare-bones Alpine box).

Slightly more useful is to base another image on it:

```
# Dockerfile
FROM bjjb/cron
RUN echo "* * * * * date" > /etc/crontabs/root
```

    docker run $(docker build -q .)

and you'll see the date printed out every minute. (Not terribly useful, but
you get the idea).

Even more useful is to install your own crontabs and tools in your base image.
You could, for example, trigger a web-service call at 01:01 every day.

```
# Dockerfile
FROM bjjb/cron
RUN apk install --no-cache curl
RUN echo "1 1 * * * curl https://webservice/ping" > /etc/crontabs/nobody
```

(The above will be run as nobody in the container).
Or write in your own more complicated crontabs and scripts.

Most useful is to set up crontabs in a volume.

    V=$(docker create volume)
    docker run -it -v --rm $V:/_ bjjb/cron vi /etc/crontabs/nobody
    # edit your crontabs and exit
    docker run -d -v $V:/etc/crontabs bjjb/cron

...or do the same with a plain old container.

## Caveats

* `crontab` is in the box, but won't work as expected unless it's suid.
