A [red-rings](https://github.com/shimaore/red-rings/) component supporting [Socket.io](https://www.npmjs.com/package/socket.io-client).

The following modules are provided:
- `client` — a frontend client (usable e.g. in a UI)
- `frontend` — a frontend plugin for abrasive-ducks

No backend is provided.

Client
------

```
const socket = io('http://localhost')
const client = new RedRingSocketioClient(socket)

socket.on( 'ready', () =>
  client
  .receive("legacy-number:${number}")
  .map( (msg) => {
    switch msg.get 'state'
      when 'ingress-call'
        msg.getIn(['value','source'])
      when 'call-attempt'
        msg.getIn(['value','destination'])
      when 'end'
        null
  })
  .forEach( (number) => … )
})
```

`client.receive(message,limit = most.never())` returns a Most.js stream of Immutable.js messages. The stream stops when `limit` emits an event.

`client.create(doc)`

`client.update(id,rev,doc,operations)`

`client.delete(id,rev)`

(`client.notify(key,id,value,doc)`)
