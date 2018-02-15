    {RedRing} = require 'red-rings'

    class RedRingSocketioClient extends RedRing

      constructor: (io) ->
        super io
        @io = io
        return

      send: (msg) ->
        @io.emit 'msg', msg

      source_of: (key) ->
        most.fromEvents 'msg', @io

    module.exports = RedRingSocketioClient