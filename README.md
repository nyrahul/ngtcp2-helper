# ngtcp2-helper
Provides interface, design details of ngtcp2. Future, will provide easy to use ngtcp2 APIs pre-integrated with various events/ssl libs.

# ngtcp2 design rationale
ngtcp2 implementation does not tightly couple with the socket layer nor the SSL
implementation. It depends on upper layer to manage the sockets, read/write the
sockets on behalf of the ngtcp2. Similarly timers are not directly managed
inside ngtcp2. The upper layer (I am calling it APP in the call flows) checks
the expiry time from ngtcp2 and starts the timer.

The SSL implementation is also not tightly coupled i.e., the ngtcp2 requires
the APP layer to fulfill certain callbacks which in turn could be implemented
using any TLS1.3 implementation. The existing example client/server apps in the
ngtcp2 use libev for socket management and OpenSSL for TLS1.3 handling.

The advantage with this design is that the app layer is free to choose any
event library for sockets, timers etc. The example uses libevent, but libuv can
as well be easily plugged in. Similarly the APP controls the TLS1.3
implementation to use and thus could switch the TLS libary in the future.

The ngtcp2 implementation provides QUIC implementation decoupled from any
platform libs and thus should be easy to port.

# ngtcp2 API flow

Please note that this is not a rigorous representation i.e., the flow is
supposed to give an idea about how ngtcp2 APIs manages handshake, connections
and streams.

![QUIC/ngtcp2 handshake flow](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/nyrahul/ngtcp2-helper/master/res/ngtcp2-handshake.puml?cache=no)

![ngtcp2 API flow](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/nyrahul/ngtcp2-helper/master/res/ngtcp2-api-flow.puml?cache=no)

# QUIC pcap

ngtcp2 client/server examples used.
Server UDP port: 12345

[QUIC 1-RTT session flow](pcap/quic-1rtt-sess.pcap)

Above session was resumed using 0RTT flow.
[QUIC 0-RTT session flow](pcap/quic-0rtt-sess.pcap)

Certificate and Private key files used from [TalkWithTLS](https://github.com/nyrahul/TalkWithTLS/tree/master/certs/RSA_Certs).
Thanks to [Ashok](https://github.com/raja-ashok)
