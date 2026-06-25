# HTTP

HyperText Transfer Protocol

## Anatomy

Request body

- URL
- Method type
- Headers
- Body

Response body

- Status code
- Headers
- Body

# Versions of HTTP

## HTTP v1.0

- TCP connection is closed after completing request.
- Buffers for large index.html
- Survived 1 year

![HTTP v1.0](../media/df1f07c4.jpg)

## HTTP v1.1

- invented the `Keep Alive` header sent by client to server.
- Etags was introduced.
- Persisted TCP Connection
- Streaming with chucked transfer instead of buffering
- Pipelining can be used, requests can be sent parrallely, leads to ordering issue. (not used generally)

![HTTP v1.1](../media/71ce6908.jpg)

### E-Tags

- stands for "Entity Tags"
- For caching, implementation
    1. Client does a request
    2. Server sends a `ETag: "<value>"` with a response.
    3. Client makes a subsequent request to same resource.
    4. This request has `If-None-Match: "<etag>"` header
    5. If resource is not changed, Server responds with `304 Not Modified`

- For consistency,
    - Modification requests have correct etag for resource -> good
    - Otherwise, resource has been changed already, request can be failed.
    - For conflict we send `412 Precondition Failed`

- Can be used for user tracking, by always sending 304. (since ETags are removed as cookies)

## HTTP v2.0

- Multiplexing (multiple req/res sent simultaneously over single TCP connection)
- This resolved the "head-of-line" blocking issue (1st item stalls all subsequents items)
- Binary format is used
- Protocol negotiation during TLS

### Multiplexing

- Also called HTTP streams.
- Multiple requests can be sent over same TCP connection
- Pipelining (HTTP v1.1), requires server to respond in FIFO order
- Multiplexing has no constraint on response order.
- Data is broken down into binary encoded frames tagged with stream IDs.

### HPACK

- Headers are compressed using HPACK.
- It works by having
    1. Static dictionary of 61 commonly used headers
    2. Dynamic dictionary, list of headers encountered during connection
    3. Huffman code

- dictionaries map headers (name:value or name or value) to bytes
- In subsequent requests, value of headers like cookie or referer are taken from dynamic dictionary
- Works againsts CRIME attacks (Manipulate requests & check resulting compressed payload size)

### Server Push

- Server proactively sends assets (JS, CSS, etc) to client's cache before the requests
- Deprecated in favor of 103 Early Hints

## HTTP v3.0

- Replace TCP with QUIC
- QUIC is on top of UDP and adds congestion control
- QUIC runs in user-space (TCP runs in kernal space)
