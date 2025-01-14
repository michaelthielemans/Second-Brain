application programming interface

## Why use APIs ?

- data integration: consuming or reacting to another applications api
- automation tasks: a script can call the api of another application
- functionality: integrate a functionality from one application into the other by the api


### Synchronous API
- the api will respond immediately to a request
- the data for the request is readily available

*Downside:*
The script or program that is sending the request to the API of the other program cannot execute other tasks when it is waiting to receive the result of his request.


### Asynchronous API
Like ordering food in a fastfood restaurant. Order -> wait -> receive
- the data is not readily available when the request have been made

*Benifit*
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
the rest message can include executional code. this will add functionality to the client


# API rate limits

#### Leaky bucket

#### Token bucket
- The algorithm gives each client a defined amount of tokens within a certain increment of time.

#### Fixed window counter
- A max amount of requests is set for each period of time
	- for example 20 requests/min
#### Sliding window counter


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

## Trouble shooting API calls
#### REST