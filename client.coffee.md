    {RedRing} = require 'red-rings'

    class RedRingSocketioClient extends RedRing

      constructor: (io) ->
        super io
        @io = io
        @source = most
          .fromEvent 'msg', @io
          .map fromJS
          .multicast()
        return

      send: (msg) ->
        @io.emit 'msg', msg

      source_of: (key) ->
        key = Immutable.fromJS key
        @source.filter (msg) -> Immutable.is key, msg.get 'key'

    module.exports = RedRingSocketioClient
    most = require 'most'
    Immutable = require 'immutable'
    reviver = require 'ccnq4-kitty/reviver'
    fromJS = (x) -> Immutable.fromJS x, reviver
