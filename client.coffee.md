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
        key = fromJS key
        @source.filter (msg) -> key.equals msg.get 'key'

    module.exports = RedRingSocketioClient
    most = require 'most'
    {fromJS} = require 'immutable'
