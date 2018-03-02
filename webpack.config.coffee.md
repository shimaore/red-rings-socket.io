    path = require 'path'
    module.exports =
      entry:
        browser: './client.js'
      output:
        path: path.join __dirname, '.'
        filename: '[name].js'
        library: 'RedRingSocketioClient'
        libraryTarget: 'umd'
