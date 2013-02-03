Feedbin API
===========

Making Requests
---------------

The base URL for all requests is `https://feedbin.me/api/v1/` Only https is supported.

The Feedbin API uses HTTP Basic authentication

Using cURL you would make a request like: 

```shell
curl -u 'example@example.com:password' https://feedbin.me/api/v1/subscriptions.json
```

When creating or updating a record you must set `application/json; charset=utf-8` as the `Content-Type` header.

```shell
curl -u 'example@example.com:password' \
-H "Content-Type: application/json; charset=utf-8" \
-X POST -d '{"feed_url":"http://daringfireball.net"}' \
http://feedbin.dev/api/v1/subscriptions.json
```

Without this header you'll wind up with a `415 Unsupported Media Type` response.

HTTP Caching, Use It
--------------------
For extra speed, please use HTTP Caching. `GET` request set ETag and a Last-Modified headers. 

```shell
curl -v -u 'example@example.com:password'  https://feedbin.me/api/v1/subscriptions/3.json
< ETag: "c7d001e87bda1f0d3745b6bd2811b055"
< Last-Modified: Sat, 02 Feb 2013 15:20:46 GMT
```

You can use these headers in subsequent requests like:

```shell
curl -v -u 'example@example.com:password' --header 'If-Modified-Since:Sat, 02 Feb 2013 15:20:46 GMT' --header 'If-None-Match:"c7d001e87bda1f0d3745b6bd2811b055"' https://feedbin.me/api/v1/subscriptions/3.json
< HTTP/1.1 304 Not Modified
```

Pagination
----------
Entries use pagination. Each page has a limit of 100 items. Paginated request will include a link header like:

```
Link: <https://feedbin.me/api/v1/feeds/1/entries.json?page=2>; rel="next", <https://feedbin.me/api/v1/feeds/1/entries.json?page=5>; rel="last"
```

The possible rel values are:

- `first` The URL of the first page of results.
- `prev` The URL of the previous page of results.
- `next` The URL of the next page of results.
- `last` The URL of the last page of results.


API Objects
-----------

- [Subscriptions](content/subscriptions.md)
- [Feeds](content/feeds.md)
- [Entries](content/entries.md)
- [Entry States](content/entry-states.md)

