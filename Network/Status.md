# HTTP Status Code
HTTP (Hypertext Transfer Protocol) status codes are three-digit codes that indicate the outcome of an HTTP request. Some common status codes include:

## 1xx (Informational):

### 100 Continue
The 100 Continue status code is used in HTTP 1.1 to indicate that the client should continue sending the request or ignore it if the request has already been sent. This status code is typically used to indicate that the server has received the request headers, and the client should proceed to send the request body.

A server may return a 100 Continue status code to indicate that it is ready to receive the request body, and it helps to avoid the client timing out if the server is taking a long time to process the request. The client should wait for the 100 Continue status code before sending the request body, and it can proceed to send the request body once it receives the 100 Continue status code.

In practice, you will receive a 100 Continue status code when you are sending a large request body to a server, and the server requires that you wait for a 100 Continue status code before sending the request body. If the server does not require this behavior, then you will not receive a 100 Continue status code.

The 100 Continue status code is still in use, but it is becoming less common as more and more servers are being configured to automatically send the request body without waiting for a 100 Continue status code. The 100 Continue status code was introduced in HTTP 1.1 as a way to optimize the request-response cycle, but with the increasing speed of network connections, the need for this optimization has become less important.

Additionally, many modern applications and libraries have implemented their own optimization strategies that make the 100 Continue status code redundant, and this has led to the decline in its use.

That being said, the 100 Continue status code is still a valid HTTP status code and can still be used in some situations where it is needed, such as in large file uploads or when working with slow networks. However, in most cases, it is not necessary, and you can send the request body directly without waiting for a 100 Continue status code.

### 101 Switching Protocols

The 101 Switching Protocols status code is used in HTTP to indicate that the server is switching to a different protocol, such as upgrading from HTTP 1.1 to HTTP 2.0.

This status code is typically used in conjunction with the Upgrade header, which specifies the protocol that the server is switching to. The Upgrade header is sent by the client in its initial request, indicating that it supports the specified protocol, and the server can then respond with a 101 Switching Protocols status code to indicate that it is switching to the requested protocol.

In practice, you will typically only see the 101 Switching Protocols status code in situations where you are upgrading the protocol used by your application or when you are working with a server that supports multiple protocols. This status code is not commonly used in general web traffic, as most servers and clients still use the traditional HTTP 1.1 protocol.

It's important to note that not all servers support the 101 Switching Protocols status code and the Upgrade header, so it's always a good idea to check the server's documentation to see if it supports this feature.

### 103 Early Hints

The 103 Early Hints status code is a relatively new status code that was introduced as part of HTTP/2. It is used to provide early hints about the resources that will be required to fully render a page.

The idea behind the 103 Early Hints status code is to give the client a head start on fetching the resources it needs to render a page, so that it can start downloading these resources before the full response is available. This can help to speed up page load times, as the client can start downloading resources even before the response headers have been received.

The 103 Early Hints status code is sent in the form of an HTTP header and is typically sent before the final response status code. It contains a list of link headers, each of which provides information about a resource that the client should fetch.

In practice, the 103 Early Hints status code is not widely used, as most web servers do not support it yet. However, it is a promising new development in the field of web performance optimization, and it is likely to become more common in the future as more web servers adopt it.

### 2xx (Successful):

### 200 OK

The 200 OK status code is one of the most commonly used HTTP status codes and indicates that the request was successful. It means that the client's request was accepted by the server and that the requested resource was successfully retrieved.

You can expect a 200 OK status code in a wide variety of situations, including:

When you make a GET request to retrieve a resource, such as a web page or an image.
When you make a POST request to submit data to a server, such as when filling out a form on a website.
When you make a PUT request to update a resource on the server.
When you make a DELETE request to delete a resource from the server.
In general, you should expect a 200 OK status code whenever you make a request to a server and the server is able to successfully complete the request. If the request is successful, the server will return a 200 OK status code along with the requested resource.

It's important to note that a 200 OK status code does not guarantee that the resource is error-free or that it meets the expectations of the client. For example, a 200 OK status code could be returned even if the requested resource is empty or if it contains errors. In these cases, the client should inspect the response payload to determine if it meets the requirements of the request.

### 201 Created

The 201 Created status code is used to indicate that a new resource has been successfully created as a result of a POST request. This status code is used to confirm that a client's request to create a new resource on the server was successful, and that the resource is now available for use.

You can expect a 201 Created status code in situations where you make a POST request to create a new resource on a server. For example, this could include creating a new user account on a website, creating a new blog post, or uploading a file to a server.

In addition to the status code, the server should also return a Location header that contains the URL of the newly created resource. This allows the client to easily access the new resource, and it provides a permanent URL that can be used to reference the resource in the future.

It's important to note that the 201 Created status code should only be used in response to a POST request. If you make a request using a different method, such as a GET request, you should expect a different status code, such as 200 OK.

A server might respond with a 200 OK status code instead of a 201 Created status code for a POST request in certain circumstances. This can happen when the server processes the request, but the creation of the resource is not the primary focus of the request.

For example, consider a scenario where a client makes a POST request to a server to update an existing resource. In this case, the server might return a 200 OK status code to indicate that the request was successful, but that the resource was updated, rather than created.

Another example could be a scenario where a client makes a POST request to a server to submit data for processing. The server might return a 200 OK status code to indicate that the request was successful, but that no new resource was created as a result of the request.

It's important to keep in mind that the HTTP status codes are intended to provide a high-level indication of the result of the request, rather than a detailed description of what happened. In general, you should expect a 201 Created status code when a new resource is created as a result of a POST request, and a 200 OK status code when the request was successful, but the creation of a new resource was not the primary focus of the request.

### 204 No Content



205 Reset Content
206 Partial Content
3xx (Redirection):

300 Multiple Choices
301 Moved Permanently
302 Found
303 See Other
304 Not Modified
307 Temporary Redirect
4xx (Client Error):

400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
405 Method Not Allowed
408 Request Timeout
409 Conflict
410 Gone
413 Payload Too Large
414 URI Too Long
429 Too Many Requests
5xx (Server Error):

500 Internal Server Error
501 Not Implemented
502 Bad Gateway
503 Service Unavailable
504 Gateway Timeout
505 HTTP Version Not Supported
These codes indicate whether a request was successful, or what type of error occurred. For example, a 200 OK status code indicates that the request was successful, while a 404 Not Found status code indicates that the requested resource could not be found on the server.