# REST

[TOC]

# REST API

* Representation State Transfer
* An architectural pattern for creating an API that uses HTTP as its communication method
* for designing network based application
* Resource: 
    * If we have endpoint/URI(URL or URN), lets say https://127.0.0.1/coders then we have resource. Here coders is a resource.
    * Its nothing new, we already used to make URLs that way
* Representation:
    * When a client makes a GET request to coders/toran/ client gets following JSON response
    ```JSON
    {
    "nickname": "toran",
    "powerLevel": 5
    }
    ```
    * so, this is representation in the form of JSON having metadata
    * representation also could be XML, HTML
    * the same applies when a client sends a request which contains a 'coder' data, its sends representation
* Representational State:
    * like browsing the web
    * a HTML page is a representation of a resource at current state (or current data) of that resource.
    * When we submit a form, we just send a representation back to the server
* Representational State Transfer
    * a client and server exchange representations of a resource, which reflects its current state or desired state.
    * So, REST is a way for two machines to transfer the state of a resource via representations.

**Note:** There is a very common confusion in terminology. **"Resource"**
- In URI "app/questions/1" here "1" is also know as resource and at the same time "questions" is also know as resource.
- Some people around the globe also use "1" as record/entity & "questions" as resource.
- We could generalize "1" as "resource object" and "questions" as "resource class"


# HTTP Request Methods (HTTP verbs)
HTTP defines a set of request methods to indicate the desired action to be performed for a given resource

## GET

```
GET /questions/:question_id HTTP/1.1
Host: www.example.com
```

- The GET method requests a representation of a specified resource.
- GET request should only used for data retrieval. (But can also be used for submit/posting/sending data)
- a resource is mentioned in URL.

## POST

```
POST /questions/<existing_question> HTTP/1.1
Host: www.example.com/
```

- Used to modify/update an existing entity of a specified resource.
    - Do mention the object/entity of the resource in the URL to update
    - we should use PUT and PATCH for update
        - PUT would create a new unwanted resource when the resouce doesn't exists while updating that particular resource
        - PATCH is perfect for partial updation
    - But there is no restrictions using POST for updates

```
POST /questions/ HTTP/1.1
Host: www.example.com
```    

- Used to submit a new entity/data to a specified resource.
    - Do not mention the object/entity of the resource in the URL while creating it. Otherwise it will give "Resource Not Found" error.
    - Use this if you want server to let the name, the URL object while creating a new one
- Causes change in state of the resource
- Two simultaneous POST requests works fine (lets say, 1st request is updating some part & 2nd request is updating other part of an object) 
- The `UPDATE` performed by the POST method might not result in a resource that can be identified by a URI.

## PUT
- Used to create a new resource entity or **overrite** (Completely replaces) the existing one.
- For a new resource entity:
    ```
    PUT /questions/:new_question_id HTTP/1.1
    Host: www.example.com
    ```
- To overrite an existing one:
    ```
    PUT /questions/:existing_question_id HTTP/1.1
    Host: www.example.com
    ```    
- Usefull when you know the name of the entity/object
- Use this if you want to name the URL object while creating a new one
- PUT is idempotent, so if you PUT the same object twice, it has no effect (will overrite)
- Can create or update an object with the same URL

## DELETE

```
DELETE /api/resource/:id HTTP/1.1
Host: www.example.com/
```

- Deletes/destroyes a specified resource object/entity/record


## PATCH

```
PATCH /users/1 HTTP/1.1
Host: www.example.com
Content-Type: application/example
If-Match: "c0b42b66e"
Content-Length: 120

{changes}
```

where [changes] could be JSON/XML like {email:'toran.sahu@yahoo.com'}

- Used to make partial modification to an existing resource object/entity.
- Works differently than POST & PUT for update
- Need to have URL object known

## HEAD

```
$ curl http://0.0.0.0:8010/ --head

HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.7.3
Date: Sat, 23 Aug 2020 17:14:52 GMT
Content-type: application/json; charset=utf-8
Content-Length: 13306
```

- Ask for the response same as GET but without response/message body.
    - i.e. returns Header & Status Code, except Body
- Usages?
    - to fetch headers, or to verify the API by status code
    - to get the content size of a media file - without fetcching it actually
- request has body? No
    - can send query params only
- successful response has body? No
- safe? Yes
- idempotent? Yes
- cacheable? Yes
- allowed in HTML forms? No

## OPTIONS

```
$ curl /api/resource -X OPTIONS -i

# responds with header; and empty body
HTTP/2 200 OK
date: Sat, 07 Aug 2021 16:48:46 GMT
content-length: 0
vary: Origin
access-control-allow-origin: https://api.toran.com
access-control-allow-credentials: true
access-control-allow-headers: Accept,Accept-Version,Content-Length,Content-MD5,Content-Type,Date,X-Auth-Token,x-requested-with,x-csrftoken,x-page-total,Accept-Language,Connection,x-page-limit,Accept-Encoding,x-page-page,cache-control
access-control-allow-methods: GET,HEAD,POST,PATCH,PUT,DELETE
access-control-max-age: 3600
content-security-policy: default-src 'self'; object-src 'none'; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline';
strict-transport-security: max-age=31536000; includeSubDomains; preload
referrer-policy: strict-origin-when-cross-origin
permissions-policy: geolocation=()
server: kong/2.1.4

# (optional) Body, btw DRF sends body by default
{"name":"Api Resource","description":"","renders":["application/json","text/html"],"parses":["application/json","application/x-www-form-urlencoded","multipart/form-data"]}
```

- Used to describe the communication option for the target resource 
- tell the capabilities of the API server, like list of supported:
    - HTTP methods by the server
    - header keys
    - `Content-Type`
    - `Accepts`
- request has body? No
    - can send query params only
- successful response has body? Yes (optional)
- safe? Yes
- idempotent? Yes
- cacheable? No 
- allowed in HTML forms? No
- usage?
    - to communicate with server during CORS case (preflight)
    - tell the server that I will do this, do you support those?
        ```
        OPTIONS /resources/post-here/ HTTP/1.1
        Host: bar.example
        Access-Control-Request-Method: POST
        Access-Control-Request-Headers: X-PINGOTHER, Content-Type
        ```
        meaning, I'll do `POST` and with headers `X-PINGOTHER` and `Content-Type`. do you supposet those?

        Response:

        ```
        HTTP/1.1 204 No Content
        Access-Control-Allow-Methods: POST, GET, OPTIONS
        Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
        ```

## CONNECT
- starts two-way communications with the requested resource
- it can be used to open a tunnel
- ref
    - https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/connect
    - https://reqbin.com/Article/HttpConnect


## TRACE
- Performs message loop-back test along the path to the target resource


# HTTP Response Codes
- 1XX informational
    - 101 switching protocol
- 2XX Success
    - 200 (Ok)
    - 201 (Created)
    - 204 (No Content)
- 3XX Redirection
    - 304
- 4XX Client Error
    - 404
- 5XX Server Error
    - 501 (Not Implemented)
