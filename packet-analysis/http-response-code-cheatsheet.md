# HTTP Response Code Cheatsheet

## **HTTP Server Response Codes Cheat Sheet**&#x20;

HTTP response codes indicate the status of a request between a client (browser, app) and a web server. These codes help analysts and defenders troubleshoot issues and understand server behavior.

### **1xx – Informational Responses** (Request Received, Continuing Process)

| **Code**                    | **Meaning**                | **Description**                                     |
| --------------------------- | -------------------------- | --------------------------------------------------- |
| **100 Continue**            | Request received, continue | Server received headers, waiting for body.          |
| **101 Switching Protocols** | Switching to new protocol  | Used for WebSockets or HTTP/2 upgrades.             |
| **102 Processing**          | Request is being processed | Used in WebDAV to indicate long request processing. |
| **103 Early Hints**         | Preload resources          | Server suggests resources for faster loading.       |

***

### **2xx – Success** (Request Was Successfully Received, Understood, and Accepted)

| **Code**                              | **Meaning**                        | **Description**                                     |
| ------------------------------------- | ---------------------------------- | --------------------------------------------------- |
| **200 OK**                            | Request successful                 | Standard response for successful HTTP requests.     |
| **201 Created**                       | Resource successfully created      | Used for POST requests when a new resource is made. |
| **202 Accepted**                      | Request accepted but not completed | The request is being processed asynchronously.      |
| **203 Non-Authoritative Information** | Altered response                   | Proxy-modified response (e.g., CDN caching).        |
| **204 No Content**                    | Successful but no response body    | Common for DELETE requests.                         |
| **205 Reset Content**                 | Reset user input                   | Often used in forms, resets document view.          |
| **206 Partial Content**               | Partial content sent               | Used for resume downloads, streaming.               |

***

### **3xx – Redirection** (Further Action Required)

| **Code**                           | **Meaning**                          | **Description**                                          |
| ---------------------------------- | ------------------------------------ | -------------------------------------------------------- |
| **300 Multiple Choices**           | Multiple options available           | The user must select a preferred response (rarely used). |
| **301 Moved Permanently**          | Resource permanently moved           | Clients and search engines should update URLs.           |
| **302 Found (Temporary Redirect)** | Temporary redirect                   | Redirects user but keeps the original URL.               |
| **303 See Other**                  | Redirects using GET                  | Used for API responses after a POST request.             |
| **304 Not Modified**               | Cached resource is up-to-date        | The client should use the cached version instead.        |
| **307 Temporary Redirect**         | Similar to 302, but preserves method | POST remains POST, unlike 302.                           |
| **308 Permanent Redirect**         | Like 301, but keeps request method   | Ensures method (POST, PUT) doesn’t change.               |

***

### **4xx – Client Errors** (Request Issues From User’s Side)

| **Code**                                | **Meaning**                              | **Description**                                                |
| --------------------------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| **400 Bad Request**                     | Invalid request                          | The client sent malformed or invalid data.                     |
| **401 Unauthorized**                    | Authentication required                  | Credentials missing or incorrect (API tokens, login).          |
| **402 Payment Required**                | Reserved for future use                  | Originally intended for online payments.                       |
| **403 Forbidden**                       | No permission to access                  | The client lacks authorization, even with credentials.         |
| **404 Not Found**                       | Resource not found                       | URL doesn’t exist or is incorrect.                             |
| **405 Method Not Allowed**              | Wrong HTTP method                        | Example: Sending POST to a GET-only endpoint.                  |
| **406 Not Acceptable**                  | Cannot fulfill request                   | Content requested is unavailable in the desired format.        |
| **407 Proxy Authentication Required**   | Authenticate with proxy                  | Similar to 401, but for proxy servers.                         |
| **408 Request Timeout**                 | Server timed out waiting for request     | Client took too long to send data.                             |
| **409 Conflict**                        | Conflict in resource state               | Example: Editing a document that was already updated.          |
| **410 Gone**                            | Resource permanently removed             | Unlike `404`, this confirms the resource was deleted.          |
| **411 Length Required**                 | Missing Content-Length header            | Required for certain POST requests.                            |
| **412 Precondition Failed**             | Condition in headers not met             | Used in conditional requests (If-Modified-Since).              |
| **413 Payload Too Large**               | Request body too big                     | Server rejects oversized data uploads.                         |
| **414 URI Too Long**                    | URL is too long                          | Common when sending too much data in query parameters.         |
| **415 Unsupported Media Type**          | Content type not supported               | Example: Uploading an image in an unsupported format.          |
| **417 Expectation Failed**              | `Expect` header requirement not met      | Rarely used; server can’t meet expectations.                   |
| **418 I'm a Teapot**                    | Easter egg joke                          | Defined in RFC 2324 (Hyper Text Coffee Pot Control Protocol ). |
| **421 Misdirected Request**             | Sent to the wrong server                 | Common with misconfigured load balancers.                      |
| **422 Unprocessable Entity**            | Request format correct, but invalid data | Often used in REST APIs.                                       |
| **425 Too Early**                       | Server refuses early data                | Helps prevent replay attacks.                                  |
| **426 Upgrade Required**                | Client must switch protocol              | Example: Enforcing an HTTPS upgrade.                           |
| **428 Precondition Required**           | Requires conditional headers             | Used for safe resource modifications.                          |
| **429 Too Many Requests**               | Client exceeded rate limit               | Used in API rate limiting (e.g., 100 requests per minute).     |
| **431 Request Header Fields Too Large** | Headers too big                          | Server rejects due to excessive headers.                       |

### **5xx – Server Errors** (Issues on the Server’s Side)

| **Code**                                | **Meaning**                                      | **Description**                                               |
| --------------------------------------- | ------------------------------------------------ | ------------------------------------------------------------- |
| **500 Internal Server Error**           | Generic server failure                           | Catch-all error when something goes wrong.                    |
| **501 Not Implemented**                 | Server doesn’t support request method            | Example: Sending `PATCH` to a server that doesn’t support it. |
| **502 Bad Gateway**                     | Server acting as a proxy got a bad response      | Common with reverse proxies and load balancers.               |
| **503 Service Unavailable**             | Server overloaded or in maintenance              | Temporary issue—try again later.                              |
| **504 Gateway Timeout**                 | Server didn’t get a response from another server | Common in cloud environments.                                 |
| **505 HTTP Version Not Supported**      | Server doesn’t support the HTTP version used     | Example: Using HTTP/1.0 on an HTTP/2-only server.             |
| **506 Variant Also Negotiates**         | Misconfiguration in server content negotiation   | Rarely seen outside experimental setups.                      |
| **507 Insufficient Storage**            | Server lacks space to store request              | Common in file upload services.                               |
| **508 Loop Detected**                   | Infinite request loop detected                   | Usually caused by misconfigured redirects.                    |
| **510 Not Extended**                    | Additional extensions needed                     | Experimental, rarely used.                                    |
| **511 Network Authentication Required** | Login required before access                     | Seen on public Wi-Fi portals.                                 |

### **Common Troubleshooting Steps**

| **Issue**                     | **Likely Cause**            | **Fix**                                   |
| ----------------------------- | --------------------------- | ----------------------------------------- |
| **404 Not Found**             | URL incorrect, page deleted | Double-check URL or restore the resource. |
| **403 Forbidden**             | No permission               | Verify authentication and access rights.  |
| **500 Internal Server Error** | Server misconfiguration     | Check logs for application errors.        |
| **502 Bad Gateway**           | Proxy issue                 | Restart proxy/load balancer.              |
| **429 Too Many Requests**     | Rate limiting               | Reduce request frequency or wait.         |
| **504 Gateway Timeout**       | Backend server is down      | Check backend availability.               |

### **Summary**

✔ **1xx:** Information (Request in progress)\
✔ **2xx:** Success (Request completed)\
✔ **3xx:** Redirection (New location or method)\
✔ **4xx:** Client error (Request issue)\
✔ **5xx:** Server error (Backend failure)
