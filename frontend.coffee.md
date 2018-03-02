A socket.io server used as front-end for abrasive-ducks
-------------------------------------------------------

    socketio_frontend = (io,build_client_policy,frontend_join) ->

      io.on 'connection', (socket,params) ->

request contains headers such as Cookie, handshake contains headers, query, … see https://socket.io/docs/server-api/#socket-handshake

        client_policy = build_client_policy socket.request, socket.handshake
          .multicast()

        client_disconnect = most.fromEvent 'disconnect', socket

        client_source = most
          .fromEvent 'msg', socket
          .until client_disconnect

        client_sink = frontend_join client_source, client_policy

        client_sink
        .until client_disconnect
        .filter operation NOTIFY
        .forEach (msg) ->
          socket.emit 'msg', msg.toJS()

        client_policy
        .take 1
        .forEach -> socket.emit 'ready'

        return

      return

    module.exports = socketio_frontend
    most = require 'most'
    {operation} = require 'abrasive-ducks-transducers'
    {NOTIFY} = require 'red-rings/operations'
