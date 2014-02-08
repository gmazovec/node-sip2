sipcore.js
==========

General purpose SIP library for JavaScript.

## Installation

    npm install sipcore

## API

    SIP.format (msg, compact)
    SIP.parse (text)
    SIP.parseUri (text)
    SIP.formatUri (uri)
    SIP.isMessage (obj)

    SIP.createMessage (obj)
    Message.getHeader (name, parse, pos)
    Message.setHeader (name, value, pos)
    Message.toResponse (status, reason)
    Message.toRequest (method, uri)
    Message.copy ()
    Message.format (compact)

    SIP.createTransport ()
    Transport.register (protocol, [port], [address])
    Transport.listen ([cb])
    Transport.isListening ([protocol])
    Transport.send (msg, [address], [port], [protocol], [cb])
    Transport.close ()
    Event: Transport.on('message', function (msg))
    Event: Transport.on('listening', function (listenState))

    SIP.createTransaction (transport, [msg])
    Transaction.state
    Transaction.timeout
    Transaction.error
    Transaction.send (msg, [addr], [port], [protocol], [cb])
    Transaction.send (msg, [cb])
    Transaction.on('message', function (message))
    Transaction.on('state', function (state)
    Transaction.on('timeout', function ())


## Example

    var sip = require('sipcore');
    var transport = sip.createTransport();

    process.env.JS_ENV = 'node';

    transport.register('udp');
    transport.listen(function (listenState) {
      console.log('* UDP listening...', listenState.udp ? 'ok' : 'failed');
    });

    transport.on('message', function (msg) {
      console.log('-- new SIP message');
      console.log(msg.format());
    });

