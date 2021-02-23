# REST API Design and Best Practices

[stackoverflow.blog](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)

REST APIs should be easy to understand for anyone consuming them, future-proof, secure, and fast.

## Accept and Respond with JSON

REST APIs should accept JSON for request payload and also send responses to JSON. Form data is good for sending data, especially to send files.

To make sure that when our REST API app responds with JSON that clients interpret it as such, we should set `Content-Type` in the response header to `application/json` after the request is made. Many server-side app frameworks set the response header automatically. Some HTTP clients look at the `Content-Type` response header and parse the data according to that format.

```yaml
Content-Type: application/json; charset=utf-8
```

## Nouns > Verbs In Endpoint Paths

Don't use verbs in endpoint paths. Instead, use the nouns which represent the entity that the endpoint is retrieving or manipulating as the pathname.

The HTTP request method already has the verb. Having verbs in the API endpoint paths isn’t useful and it makes it unnecessarily long since it doesn’t convey any new information.

The action should be indicated by the HTTP request method making the request. The most common methods include GET, POST, PUT, and DELETE.

> __GET__ — retrieves resources  
> __POST__ — submits new data to the server  
> __PUT__ — updates existing data  
> __DELETE__ — removes data

__Examples:__ GET `/articles/`, POST `/articles/`, DELETE `/articles/:id`

Verbs map to the [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) operations.

## Name Collections with Plural Nouns

Name collections with plural nouns — rarely endpoints get a single item.

Tables usually have more than one entry and are named to reflect that, so to be consistent with them use the same language as the table the API accesses.

## Nesting Resources for Hierarchical Objects

The path of the endpoints that deal with nested resources should be done by appending the nested resource as the name of the path that comes after the parent resource.

```javascript
app.get('/articles/:articleId/comments', (req, res) => {
  const { articleId } = req.params;
  const comments = [];
  // code to get comments by articleId
  res.json(comments);
});
```

__Example:__ An endpoint to get the comments for a news article, append the /comments path to the end of the /articles path.

*This is assuming that we have comments as a child of an article in our database.*

## Handle Errors Gracefully and Return Standard Error Codes

Handle errors gracefully and return HTTP response codes that indicate what kind of error occurred. Errors shouldn't bring down the system, so they can't be left unhandled, which means that the API consumer has to handle them.

Common error HTTP status codes include:

- __400 Bad Request__ — client-side input fails validation
- __401 Unauthorized__ — user is not authorized to access resource or has failed auth
- __403 Forbidden__ — user is authenticated but is not allowed to access a resource
- __404 Not Found__ — resource is not found
- __500 Internal Server Error__ — generic server error
- __502 Bad Gateway__ — invalid response from an upstream server
- __503 Service Unavailable__ — something unexpected happened on server side

Error codes should have an accompanying messages with them so that maintainers have enough information to troubleshoot the issue.

## Filtering, Sorting, and Pagination

The databases behind a REST API can get very large. Sometimes, there’s so much data that it shouldn’t be returned all at once because it’s way too slow or will bring down systems. Therefore, we need ways to filter items.

Paginate data so that the api only returns a few results at a time. We don’t want to tie up resources for too long by trying to get all the requested data at once.

Filtering and pagination both increase performance by reducing the usage of server resources. As more data accumulates in the database, the more important these features become.

__Example:__ `/employees?lastName=Smith&sort=+author,-datepublished&page=2`

> `+` *ascending sort*  
> `-` *descending sort*  
> `lastName` *filter*  
> `page` *pagination*

## Use Good Security Practices

Use SSL/TLS, duh.

## Cache Data When Possible

Caching lets users get data faster. However, the data that users get may be outdated. Use a caching solution (Cloudflare, Express APICache Middleware, Redis, Etc.).

## Versions

A new version API should be issued when making any changes that may break clients. The versioning can be done according to semantic version.

__Example:__ 2.1.6 (major version 2, minor version 1, and patch 6)

Gradually phase out old endpoints instead of forcing everyone to move to the new API at the same time. The v1 endpoint can stay active for people who don’t want to change, while the v2, with its new features, can serve those who are ready to upgrade. This is especially important if the API is public.

Versioning is usually done with /v1/, /v2/, etc. added at the start of the API path.
