# Websocket

## Background

### Forms of I/O
- Blocking
	- write, read 	
- Non-blocking 	
	- write, read + poll / select
- Asynchronous 
	- aio_write, aio_read
	- mutual exclusion, semaphores

### Non-preemptive multitasking

### Event loops

### Subroutines 
Any callable unit - method, procedure, func etc.

### Coroutines 
- what
	- Subroutines for non-preemptive multitasking, by allowing execution to be suspended and resumed
- why
	- Coroutines ensure that the developer uses a blocking style of programming that is similar to threading, but provide the benefits of non-blocking I/O
- how
- to understand it better
	- http://web.archive.org/web/20071001004937/http://members.verizon.net/olsongt/stackless/why_stackless.html#the-real-world-is-concurrent

#### Implementation possible using:
- async/await
- Eventlet
- stackless python
	- Tasklet
- Greenlet
- gevent


### `select` / `poll` 
- Available almost anything else with a TCP/IP protocol stack that either utilizes or is modeled after the BSD implementation
- A variation on the theme of polling, a select loop uses the select system call to sleep until a condition occurs on a file descriptor (e.g., when data is available for reading), a timeout occurs, or a signal is received (e.g., when a child process dies)

## `gevent-websocket`
- dependencies graph
	- `gevent-websocket`
		- `gevent`
			- `greenlet`

## `gunicorn`

`Unicorn` port for Python. Pre-fork worker model.

### Pre-fork worker model

Pre-forking basically means a master creates forks which handle each request. A fork is a completely separate *nix process.

The pre in pre-fork means that these processes are forked before a request comes in. They can however usually be increased or decreased as the load goes up and down.

Pre-forking can be used when you have libraries that are NOT thread safe. It also means issues within a request causing problems will only affect the process which they are processed by and not the entire server.

Ref: https://stackoverflow.com/questions/25834333/what-exactly-is-a-pre-fork-web-server-model



### production-ready
- https://docs.gunicorn.org/en/stable/design.html
- https://medium.com/building-the-system/gunicorn-3-means-of-concurrency-efbb547674b7

## WebSocket Issue:
- fd leakage
	- https://stackoverflow.com/questions/561988/detect-file-handle-leaks-in-python
		- close it
		- garbage collector will eventually close it, but after a long time.. you may run out of it till then
	- a socket with select when its fileno is greater than FD_SETSIZE will raise the exception ValueError: filedescriptor out of range in select()
		- https://codeghar.com/blog/use-select-in-python-socket-programming-at-your-own-risk.html
	- Changed in version 3.5: The selector is now retried with a recomputed timeout when interrupted by a signal if the signal handler did not raise an exception (see PEP 475 for the rationale), instead of returning an empty list of events before the timeout.
		- https://docs.python.org/3.5/library/selectors.html#module-selectors
- Connection already closed:
	- https://stackoverflow.com/questions/10585355/sending-websocket-ping-pong-frame-from-browser
	- implement server-initiated ping
		- https://tools.ietf.org/html/rfc6455#section-5.5.2
	- DEBUG: Load balancers are the issue, as conn. kept alive for more time (55 hrs)
- [Errno 104] Connection reset by peer
	- may be core python sock issue
		- https://github.com/python/cpython/blob/3466922320d54a922cfe6d6d44e89e1cea4023ef/Modules/errnomodule.c#L558-L561
- 1 minute idle conn termination issue
	- ping/pong vs keep-alive
		- https://stackoverflow.com/questions/23238319/websockets-ping-pong-why-not-tcp-keepalive
			- both are not same
			- TCP endpoints and WebSocket endpoints are diff.
	- FIX: server-initiated ping was a solution to keep alive idle connections

- possible wss close reason
	- if "utf-8 encoded bytestring to unicode" conversion fails; close the conn
- how long a wss or tcp conn can last?
	- https://stackoverflow.com/questions/50197453/how-long-can-a-websocket-connection-last
	- https://stackoverflow.com/questions/45693430/how-long-can-a-tcp-connection-stay-open
	

- papi-ws questions and
- why config with single worker?
```
exec gunicorn demoapi.wsgi:ws \
--worker-class geventwebsocket.gunicorn.workers.GeventWebSocketWorker \
--worker-connections 4000 \
--bind 0.0.0.0:8000 \
--threads 8 \
--pythonpath . --logger-class demoapi.glogger.gunicorn_logger
```

- why not `--workers=(2*CPU)+1` and why `--threads=8`?
- [x] why `event loop` in-combination with `gevent` is not detecting `epoll` system call (for a scalable I/O event notification mechanism)
	- my linux does have it
	```
	>>> import select
	>>> select.epoll()
	<select.epoll object at 0x7f30c5ac4228>
	>>> hasattr(select, 'epoll')
	```
	- FIX: checked again and found `gevent.selectors.GeventSelector`

## Probable Solutions
- increase `--keep-alive` (default:2 sec)
	- When Gunicorn is deployed behind a load balancer, it often makes sense to set this to a higher value.
- increase `--timeout` (default:30 sec)
	- Workers silent for more than this many seconds are killed and restarted.
	- Generally set to thirty seconds. Only set this noticeably higher if you’re sure of the repercussions for sync workers. For the non sync workers it just means that the worker process is still communicating and is not tied to the length of time required to handle a single request.
- Long-lived TCP connections: Network Load Balancer supports long-running TCP connections that can be open for months or years, making it ideal for WebSocket-type applications, IoT, gaming, and messaging applications.

## Ref
- https://tools.ietf.org/html/rfc6455
- https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_servers
- https://www.slideshare.net/jaquayle/best-practices-in-building-websockets-apis-elad-wertzberger-liveperson
- https://hpbn.co/websocket/
- https://www.quora.com/What-are-the-best-practices-for-managing-connections-to-Websockets-on-the-server-side


## TODO
- https://stackoverflow.com/questions/14925413/gevent-websocket-detecting-closed-connection
- https://stackoverflow.com/questions/31188874/why-is-gevent-websocket-synchronous
- https://stackoverflow.com/questions/23314964/is-there-a-server-cost-to-using-websockets