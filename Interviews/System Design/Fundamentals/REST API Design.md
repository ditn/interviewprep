# REST API Design
- REST APIs are designed around `resources`, where any kind of object, data or service can be accessed by the client.
- Each resource has an identifier, which is a URI that uniquely identifies that resource.
- Clients interact with a service by exchanging _representations_ of resources - typically JSON.

## Queries
-  `GET` retrieves a representation of the resource at the specified URI. The body of the response message contains the details of the requested resource.
-  `POST` creates a new resource at the specified URI. The body of the request message provides the details of the new resource. Note that POST can also be used to trigger operations that don't actually create resources.
-  `PUT` either creates or replaces the resource at the specified URI. The body of the request message specifies the resource to be created or updated.
-  `PATCH` performs a partial update of a resource. The request body specifies the set of changes to apply to the resource.
-  `DELETE` removes the resource at the specified URI.

When passing data to a server via `POST` or `PUT`, you can choose between two methods:
- Content body (JSON)
- Query parameters, e.g. `v1/authors?name=orwell&year=1984`

Generally, content body is used for data that is to be uploaded or downloaded from the server. Query parameters on the other hand are used to specify the exact data requested.

For example, when you upload a file, you specify the name, MIME type etc in the body - but when fetching a list of files you use query parameters to filter the list by some property.

In general, query paramters are a property of the query, not the data.

## POST vs PUT
| PUT | POST |
| - | - |
| `PUT` requests store data under the supplied REST URI - e.g. update if existing, add if not<br>`PUT /questions/{question_id}` | `POST` requests that the origin server accept the enclosed entity as a new subordinate of the resource.<br>`POST /questions` |
| Idempotent. If you retry multiple times, a request would be equivalent to a single request modification. | NOT idempotent. If you retry `n` times, you end up with `n` resources with `n` different URIs created on the server. |
|Use `PUT` when you want to modify a singular resource which is already part of the resources collection. `PUT` replaces a resource in its entirety. Use `PATCH` if you must update a part of the resource.| `POST` when you want to add a child resource under the resources collection. |
| Despite idempotency, we shall not cache it's response.| `POST` is not cachable unless the response includes the appropriate Cache-Control or Expires headers. However you can redirect to a cacheable resource via a `303`.|
| Always use `PUT` for `UPDATE` operations.| Always use `POST` for `CREATE` operations. |

## Versioning

All APIs should have versioning to allow us to modify the API surface and respond to requirements changes. This can be done via headers or via the API path, e.g. `someservice.com/1/whatever`.