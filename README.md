docker-events
=============

Create an event emitter from dockerode's events response

Overview
--------

Docker exposes an event API, allowing one to monitor the happenings of a Docker
host. dockerode allows for consumption of this API, albeit in a very raw form.
docker-events does a bit of work for you, turning the raw API of dockerode into
something a little more high-level by parsing the response stream and pushing
things out of an EventEmitter.

API
---

### DockerEvents (constructor)

```js
var emitter = new DockerEvents({
  docker: new Dockerode(options),
});
```

### start

```js
emitter.start();
```

### stop

```js
emitter.stop();
```

### #connect

```js
emitter.on("connect", function() {
  console.log("connected to docker api");
});
```

### #disconnect

```js
emitter.on("disconnect", function() {
  console.log("disconnected to docker api; reconnecting");
});
```

### #_message

Any raw event from Docker.

```js
emitter.on("_message", function(message) {
  console.log("got a message from docker: %j", message);
});
```

### Docker events

Events are emitted in a form of `<event.Type>:<event.Action>`.

Full list of events: https://docs.docker.com/reference/api/engine/version/v1.52/#tag/System/operation/SystemEvents

For example:

```js
emitter.on("container:create", function(message) {
  console.log("container created: %j", message);
});

emitter.on("container:start", function(message) {
  console.log("container started: %j", message);
});
```

License
-------

3-clause BSD. A copy is included with the source.

Contact
-------

* GitHub ([deoxxa](http://github.com/deoxxa))
* Twitter ([@deoxxa](http://twitter.com/deoxxa))
* Email ([deoxxa@fknsrs.biz](mailto:deoxxa@fknsrs.biz))

