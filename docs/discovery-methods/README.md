# Addressing and discovery methods

Neo-Alexandria has two discovery questions. Given a topic, which experts might help? Given an expert’s address, where should a client deliver the query?

Email illustrates the second question. In `ada@example.org`, the domain identifies where to route the message, and the receiving operator decides what `ada` maps to. The sending mail server looks up `example.org` in DNS for its MX records, which list the mail servers and their preference order. With no MX records, SMTP falls back to the domain’s address records. When it connects, it presents the full recipient address with `RCPT TO`. The sender can get that address from a contact, a directory, or an earlier exchange. [SMTP addressing](https://datatracker.ietf.org/doc/html/rfc5321#section-2.3.11) · [SMTP routing](https://datatracker.ietf.org/doc/html/rfc5321#section-5.1) · [Recipient command](https://datatracker.ietf.org/doc/html/rfc5321#section-4.1.1.3)

## Discovery across protocols

Of these seven examples, four use ordinary DNS in domain-based deployments. Three of those four specify DNS service records for locating a server. One example uses multicast DNS, and two discover peers independently of DNS.

| Protocol | Discovery method | DNS role |
| --- | --- | --- |
| XMPP | Resolves the domain in an address such as `ada@example.org` to the XMPP service. | `SRV` records. [RFC 6120](https://datatracker.ietf.org/doc/html/rfc6120#section-3.2) |
| SIP | Resolves a URI such as `sip:ada@example.org` to a server, port, and transport. | `NAPTR` and `SRV` records. [RFC 3263](https://datatracker.ietf.org/doc/html/rfc3263#section-4) |
| Matrix | Resolves the server name in an address such as `@ada:example.org`, with support for HTTPS delegation. | Hostname lookup and `SRV` records. [Matrix specification](https://spec.matrix.org/latest/server-server-api/#resolving-server-names) |
| ActivityPub | Fetches the recipient’s actor document to find their inbox URL. | Ordinary hostname lookup for the web hosts. [W3C specification](https://www.w3.org/TR/activitypub/#delivery) |
| DNS-SD over mDNS | Discovers local services, such as printers, by querying other devices on the local network. | Multicast DNS. [RFC 6763](https://datatracker.ietf.org/doc/html/rfc6763) |
| BitTorrent DHT | Finds peers for a torrent by querying a distributed hash table with its info hash. | DNS can resolve bootstrap hostnames. Peer lookup runs through the DHT. [BEP 5](https://www.bittorrent.org/beps/bep_0005.html) · [libtorrent bootstrap settings](https://www.libtorrent.org/reference-Settings.html#dht-bootstrap-nodes) |
| Bluetooth LE | Finds nearby devices by scanning for advertisements. | Device discovery runs over Bluetooth radio. [Bluetooth SIG](https://www.bluetooth.com/bluetooth-le-primer/) |

## How BitTorrent clients join a DHT

A standard magnet link identifies the torrent by its info hash. For magnets without a tracker, BEP 9 points clients to the BEP 5 DHT for peer discovery. A client can bootstrap that DHT from saved routing contacts, configured bootstrap nodes, or the `nodes` field in a trackerless `.torrent` file. Clients can start with different contacts and reach the same DHT if their contacts lead into the same connected network. [Magnet links](https://www.bittorrent.org/beps/bep_0009.html) · [DHT specification](https://www.bittorrent.org/beps/bep_0005.html) · [libtorrent bootstrap settings](https://www.libtorrent.org/reference-Settings.html#dht-bootstrap-nodes)

Mainline follows BEP 5. Vuze has a separate DHT, and BiglyBT supports both. BEP 32 also describes separate IPv4 and IPv6 DHTs for Mainline. A client that participates in both keeps two routing tables. [BEP 5](https://www.bittorrent.org/beps/bep_0005.html) · [BiglyBT](https://github.com/BiglySoftware/BiglyBT-Android/blob/master/metadata/en-US/full_description.txt) · [BEP 32](https://www.bittorrent.org/beps/bep_0032.html#operation)

## A DNS-based option for Neo-Alexandria

A client could take an address such as `ada@example.org`, use DNS to reach `example.org`, and use WebFinger over HTTPS to look up where to deliver queries for `ada`. The domain could serve that lookup itself or delegate it to a provider. A domain owner could change providers while keeping the same participant addresses. [WebFinger queries](https://datatracker.ietf.org/doc/html/rfc7033#section-4.2) · [Hosted WebFinger services](https://datatracker.ietf.org/doc/html/rfc7033#section-7)

For topic discovery, experts could publish profiles that describe their areas of expertise. Independently operated directories could index those profiles, rank matches using their own criteria, and return participant addresses. Clients would resolve those addresses through the same delivery lookup regardless of which directory they used.
