application programming interface

## Why use APIs ?

- data integration: consuming or reacting to another applications api
- automation tasks: a script can call the api of another application
- functionality: integrate a functionality from one application into the other by the api

### Synchronous API
- the api will respond immediately to a request
- the data for the request is readily available
- after the client has send the request he is waiting and expecting a immediate response.

*Downside:*
The script or program that is sending the request to the API of the other program cannot execute other tasks when it is waiting to receive the result of his request.

### Asynchronous API
Like ordering food in a fastfood restaurant. Order -> wait -> receive
- the data is not readily available when the request have been made. The client knows that it is possible that he has to wait before he receives an answer.

*Benefit*
While waiting for the result of the request that has been send the requesting software can do other tasks.

## 6 Most popular API architecture patterns
- SOAP
- RESTful
- GraphQL
- gRPC
- WebSocket
- Webhook

## RPC
Remote procedure call

The RPC api style can be applied to different transport protocols like:
- XML-RPC
- JSON-RPC
- NIFS
- SOAP

## SOAP
Simple Object Access Protocol
- XML based messaging protocol

A soap message is in fact a XML document that may contains the following elements.
- enveloppe: the root element of the xml document
- header: application specific  information and authentication
- body: contains the data that needs to be transported to the client
- fault: provides error/fault information
## REST
- client and server should be independent of each other
- is stateless -> the server cannot contain session information
cache model:

Uniform interface:

#### Code-on-Demand
The rest message can include executional code. this will add functionality to the client. This offcourse can become a vulnerability.

# API rate limits
### Per-Client Rate Limits

- **Definition:**  
    Each client (identified by an API key, IP address, user account, etc.) has its own rate limit and window. Requests from different clients are counted independently.
- **Behavior:**
    - If a client exceeds its rate limit, only that client is throttled or blocked. Other clients are unaffected.
- **Use Cases:**
    - APIs where fair usage per client is essential.
    - Scenarios where clients have different usage tiers or quotas (e.g., free vs. paid plans).

**Example:**

- Rate limit: 100 requests per minute per client.
- If Client A makes 101 requests in a minute, only Client A is blocked; Client B can still send 100 requests in the same minute.
### Global Rate Limits

- **Definition:**  
    A global rate limit applies across all clients collectively. The total number of requests made by all clients must stay within the limit.
- **Behavior:**
    - If the total number of requests from all clients exceeds the limit, further requests are throttled or blocked, regardless of which client made them.
- **Use Cases:**
    - Protecting infrastructure from being overwhelmed.
    - Scenarios where system-wide resource usage is a concern (e.g., preventing API abuse).

**Example:**

- Rate limit: 1,000 requests per minute globally.
- If Clients A, B, and C together send 1,001 requests, the 1,001st request is rejected, even if individual clients haven't reached their own limits.

### Leaky bucket
#### How the Leaky Bucket Algorithm Works

1. **Structure:**
    
    - Imagine a bucket with a small hole at the bottom.
    - Water (representing incoming requests) is poured into the bucket.
    - The water leaks out of the bucket at a fixed rate.
2. **Processing Requests:**
    
    - Incoming requests add "water" to the bucket.
    - Requests are processed at a constant rate, simulating water leaking through the hole.
    - If the bucket overflows (too many incoming requests in a short time), the excess water (requests) is discarded.
3. **Key Parameters:**
    
    - **Bucket Size:** The maximum capacity of the bucket, representing the maximum burst of requests that can be handled.
    - **Leak Rate:** The rate at which requests are processed, controlling the steady flow of API consumption.
#### Steps of the Algorithm

1. When a new request arrives:
    
    - Check if the bucket has space:
        - If yes, add the request to the bucket and process it.
        - If no, reject the request (or return an error such as `429 Too Many Requests`).
2. Continuously leak water:
    
    - At regular intervals, remove water from the bucket at the leak rate, simulating request processing.
### Token bucket
- The algorithm gives each client a defined amount of tokens within a certain increment of time.

The **Token Bucket** algorithm is a widely used method for API rate limiting. It allows controlling the rate of requests while enabling bursts of traffic up to a predefined limit. This algorithm is highly flexible and well-suited for APIs that need to handle intermittent bursts of activity.


#### How the Token Bucket Algorithm Works

1. **Structure:**
    
    - Imagine a bucket that holds tokens.
    - Each token represents permission to process one request. A token is not linked to a user.
    - The rate limit process itself adds Tokens to the bucket at a fixed rate up to a maximum bucket capacity.

1. **Processing Requests:**
    
    - A incoming request is processed if there is at least one token in the bucket. One token is removed for each processed request.
    - If the bucket is full with tokens,  the system can handle a burst of incoming requests.
    - If the bucket is empty (no tokens left), the request is either denied (rate-limited) or queued until a token becomes available.

1. **Key Parameters:**
    
    - **Bucket Size (Capacity):** Maximum number of tokens the bucket can hold, which defines the allowed burst size.
    - **Refill Rate:** The rate at which tokens are added to the bucket over time, controlling the sustained request rate.
#### Advantages of the Token Bucket Algorithm

1. **Supports Bursts:**
	- Allows short bursts of requests (up to the bucket size) without immediate throttling.
1. **Flexible Rate Limiting:**
	- Handles varying traffic patterns by combining steady refill rates with burst handling.
1. **Efficient and Simple:**
	- Easy to implement and computationally efficient.
1. **Better User Experience:**
	- Unlike the leaky bucket algorithm, it allows users to make several requests in quick succession, as long as tokens are available.

#### Drawbacks

1. **Excessive Bursts if Not Configured Properly:**
	- If the bucket size is too large, the system may experience large bursts that strain resources.
1. **Complexity for Time-Based Policies:**
	- While flexible, tracking and synchronizing token refills across distributed systems can be challenging.
### Fixed window counter
- A max amount of requests is set for each period of time
	- for example 20 requests/min

#### How the Fixed Window Counter Algorithm Works

1. **Define a Time Window:**
    - Divide time into fixed intervals or "windows" (e.g., every minute or hour).
    - A certain number of requests are allowed within each window.
2. **Track Requests Per Window:**
    - Maintain a counter that tracks the number of requests made during the current window.
    - Reset the counter at the start of the next window.
3. **Enforce Limits:**
    - If the counter exceeds the allowed limit within the current window, reject additional requests (e.g., return an HTTP `429 Too Many Requests` status).

#### Drawbacks of Fixed Window Counter

1. **Burst Traffic at Window Boundaries:**
    - A client can exploit the boundary between two windows by making requests at the end of one window and the beginning of the next.
    - Example: If the limit is 100 requests per minute, a client could send 100 requests at 0:59 and another 100 requests at 1:00, effectively sending 200 requests within 2 seconds.
2. **Coarse Control:**
    - The algorithm lacks granularity and may not handle sudden traffic spikes well.
### Sliding window counter

The rate limit information is mostly given in the response header.

When the rate limit is reached the server will reject the request and sends a response containing - rate limit reached-
-> 403: forbidden or 429: to many requests

## Webhooks

- No more polling mechanism are needed.
- If an event occurs at the resource , it is the webhook on the resource that will send a HTTP POST or HTTP callback to a specified URL.
- Also known as reverse APIs. It is the client who will 'subscribe' to a webhook server by registering

Prerequisites:
- The client application needs to run all the time in order to be able to receive the HTTP POST requests.
- the client application need to register his URI on the webhook provider

A **webhook** is a way for one application to send real-time data or notifications to another application when a specific event occurs. It enables communication between systems, allowing an application to "push" updates to a recipient without the recipient needing to request them repeatedly (polling).

#### Key Features of Webhooks

1. **Event-Driven Communication:**
    - Webhooks are triggered by specific events, such as a file upload, payment completion, or a new comment on a post.
2. **Push Mechanism:**
    - Instead of requiring the receiving application to constantly check for updates (polling), the sender sends updates automatically.
3. **URL-Based Delivery:**
    - The sender (source application) sends an HTTP request, usually a POST, to a predefined URL (the webhook endpoint) provided by the receiving application.

### How Webhooks Work

1. **Setup:**
    - The recipient (client) provides a URL where it can receive webhook data.
    - The sender (server) is configured to send data to this URL when specific events occur.
2. **Trigger:**
    - An event happens in the sender application (e.g., a user makes a purchase).
3. **HTTP Request:**
    - The sender sends an HTTP POST request to the recipient's webhook URL, often with a JSON or XML payload containing event details.
4. **Processing:**
    - The recipient's application processes the incoming request and takes appropriate action (e.g., logging the event, sending a notification, or updating a database).

## Trouble shooting API calls
#### REST