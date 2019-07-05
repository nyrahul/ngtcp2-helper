# ngtcp2-helper
Provides interface, design details of ngtcp2. Future, will provide easy to use ngtcp2 APIs pre-integrated with various events/ssl libs.

# ngtcp2 API flow

Please note that this is not a rigorous representation i.e., the flow is
supposed to give an idea about how ngtcp2 APIs manages handshake, connections
and streams.

![ngtcp2 API flow](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/nyrahul/ngtcp2-helper/master/res/ngtcp2-api-flow.puml?cache=no)

# QUIC pcap

ngtcp2 client/server examples used.
Server UDP port: 12345

[QUIC 1-RTT session flow](pcap/quic-1rtt-sess.pcap)

Above session was resumed using 0RTT flow.
[QUIC 0-RTT session flow](pcap/quic-0rtt-sess.pcap)

Certificate and Private key files used from [TalkWithTLS](https://github.com/nyrahul/TalkWithTLS/tree/master/certs/RSA_Certs).
Thanks to [Ashok](https://github.com/raja-ashok)
