**RE**presentational **S**tate **T**ransfer
- Rest is the set of rule that defines the communication between two systems.
- ![[Pasted image 20260415221436.png]]
- API that follows the REST standards is call **RESTful**
- REST differentiate the resource sharing by using unique URL
- ![[Pasted image 20260415221652.png]]
- #### There are Main four HTTP Verb
	- POST: <font color="#ff0000">C</font>REATE
	- GET: <font color="#ff0000">R</font>EAD
	- PUT : <font color="#ff0000">U</font>PDATE
	- DELETE : <font color="#ff0000">R</font>EMOVE
	- These requested basically covers the CURD operations

Optional HTTP Request Body: 
this contains the custom payload of the data in JSON format

Response:
Status Code:
It tells what happened to the response
🌐 Common HTTP Status Codes

| Code    | Name                   | Meaning                                                     |
| ------- | ---------------------- | ----------------------------------------------------------- |
| **200** | OK                     | Request successful, everything worked fine                  |
| 201     | Created                | Resource created successfully (e.g., new user, post)        |
| 204     | No Content             | Success, but no data returned                               |
| 301     | Moved Permanently      | Resource moved to a new URL permanently                     |
| 302     | Found                  | Temporary redirect                                          |
| 304     | Not Modified           | Data not changed (used for caching)                         |
| **400** | Bad Request            | Invalid request (wrong input, missing fields)               |
| 401     | Unauthorized           | Authentication required (login needed)                      |
| 403     | Forbidden              | Access denied (no permission)                               |
| 404     | Not Found              | Resource doesn’t exist                                      |
| 405     | Method Not Allowed     | Wrong HTTP method used (e.g., GET instead of POST)          |
| 409     | Conflict               | Request conflicts with current state (e.g., duplicate data) |
| 415     | Unsupported Media Type | Wrong content type (e.g., sending XML instead of JSON)      |
| 422     | Unprocessable Entity   | Validation error (data format correct but invalid values)   |
| 429     | Too Many Requests      | Rate limit exceeded                                         |
| **500** | Internal Server Error  | Something broke on server                                   |
| 502     | Bad Gateway            | Server got invalid response from another server             |
| 503     | Service Unavailable    | Server down or overloaded                                   |
| 504     | Gateway Timeout        | Server didn’t respond in time                               |

Pagination: This basically splits the large amount of data into small small chunks (pages). It makes fast requested - response.

REST API Versioning: 
it means managing changes in your API without breaking existing clients
When you update your API, you don't want old app to crash
It allows the backward compatibility

There are other API options as well
GraphQL
gRPC