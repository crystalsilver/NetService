# Pure Swift NetService (Bonjour / Zeroconf / mDNS) implementation

This module allows you to publish your own Bonjour service on the local
network. On macOS NetService is included with Cocoa, however on Linux there's
no such thing in the standard library. There might be rough edges, however
things are shaping up nicely.

[![Build Status](https://travis-ci.org/Bouke/NetService.svg?branch=master)](https://travis-ci.org/Bouke/NetService)

## Usage

See also [NetService-Example](https://github.com/Bouke/NetService-Example).

### Publish a NetService

This code will publish a new NetService. It will also setup both IPv4 and IPv6 listening sockets at an available port.

```swift
let service = NetService(domain: "local.", type: "_hap._tcp.", name: "Zithoek", port: 0)
service.publish(options: [.listenForConnections])
service.schedule(in: .main, forMode: .defaultRunLoopMode)
service.delegate = ...
withExtendedLifetime((service, delegate)) {
    RunLoop.main.run()
}
```

### Browsing for NetServices

This code will start a search for the given service type.

```swift
let browser = NetServiceBrowser()
browser.searchForServices(ofType: "_airplay._tcp.", inDomain: "local.")
browser.delegate = ...
withExtendedLifetime((browser, delegate)) {
    RunLoop.main.run()
}
```

## Credits

This library was written by [Bouke Haarsma](https://twitter.com/BoukeHaarsma).
