# Browsertrix-crawler (Webrecorder tools)

Quite different than our previous wget/httrack/static html approach, this
instead uses tools intended to generate WARC (Web ARChive) files.

The basic idea is that we "record" absolute web requests and store them in a
collection that we can later retrieve based on url and time. They do not intend
to deliver the feeling of a live website the way our existing gathering.org
archives do. Instead they focus on storing individual pieces of content and
rely on tooling to make them easier to navigate. This is the same way Wayback
machine (internet archive) works.

Specific tools used

- [browsertrix-crawler](https://github.com/webrecorder/browsertrix-crawler)
- [pywb](https://github.com/webrecorder/pywb)

## Capturing

In main folder there is a `craw-config.yaml` file that controls the crawl details.

To run with existing config

1. `docker pull webrecorder/browsertrix-crawler`
2. `docker run -p 9037:9037 -v $PWD/crawl-config.yaml:/app/crawl-config.yaml -v $PWD/crawls:/crawls/ webrecorder/browsertrix-crawler crawl --config /app/crawl-config.yaml`
3. While it is running open a web browser at `localhost:9037` to look at live crawling

This generates one or more collections under `crawls` folder. In our default
config we use a fixed collection name of `tg21`, but if we aim for a more
"live" scenario and run this on a regular basis we would probably use automatic
timestamps + context pre/post-fixes instead.

## Displaying

In `crawls` folder there is a `config.yaml` file that is used to control the
details of how collections are presented. See pywb docs for details on folder
structure, hosting tips and configuration options.

1. Install `pywb` (see their docs)
2. Run `wayback -d crawls`
3. Open `localhost:8080` to see results / browser collections

**PS!** We have added a custom `acl` rule to block loading of client side js.
This is to since page is effectively archived as "static" pages, and leaving
client side JS triggers fetches to non-archived API routes. The unmodified file
is still part of archive.
