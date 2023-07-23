---
title: "Linearized Matrix - Transport"
abbrev: "LM Transport"
category: info

docname: draft-ralston-mimi-linearized-matrix-transport-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "More Instant Messaging Interoperability"
keyword:
 - mimi
 - matrix
 - linearized
 - interoperability
 - messaging
 - decentralized
 - transport
venue:
  group: "More Instant Messaging Interoperability"
  type: "Working Group"
  mail: "mimi@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/mimi/"
  github: "turt2live/ietf-mimi-linearized-matrix-transport"
  latest: "https://turt2live.github.io/ietf-mimi-linearized-matrix-transport/draft-ralston-mimi-linearized-matrix-transport.html"

author:
 -
    fullname: Travis Ralston
    organization: The Matrix.org Foundation C.I.C.
    email: travisr@matrix.org

normative:

informative:


--- abstract

This document describes the transport protocol for Linearized Matrix.


--- middle

# Introduction

Linearized Matrix {{!I-D.ralston-mimi-linearized-matrix}} (LM) focuses on the access control policies for
a messaging protocol, but does not define a transport for client-to-server or server-to-server
communications. This document defines that transport, using gRPC ([grpc.io](https://grpc.io/)) for
server-to-server and describing the requirements of a client-to-server API without strict format.

**TODO**: Is {{?I-D.kumar-rtgwg-grpc-protocol}} up to date enough for a reference?

Layering the transport in this way allows for messaging providers to use proprietary or otherwise
custom transports when interacting with their servers. The requirements of that API are described
by this document, however.

The types throughout this document form a single `.proto` file, included in the appendix for easy
reference.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document makes use of {{!I-D.ralston-mimi-terminology}}.

# Architecture

LM {{!I-D.ralston-mimi-linearized-matrix}} defines a hub server and participant server which reside
in the context of a room. Each room has an MLS {{!RFC9420}} group associated with it. Each LM server
is responsible for its own namespace of users (including clients of those users).

The LM Transport protocol describes the requirements for a client to talk to its server, be it a hub
or participant, and the baseline gRPC structures needed for a server to talk to another server.

The server-server API has three logical operation modes:

1. Participant-to-hub for submitting events and information to the room.
2. Hub-to-participant for delivering messages from the room.
3. Direct-to-server when routing through a hub is inefficient or unnecessary.

Additionally, the implied requirements of a client-server API are described, and where applicable
guarantee that the sending client generated the request ultimately sent to another server.

~~~ aasvg
   .------------.                                  .------------.
  |   Client A   |                                |   Client B   |
   '---------+--'                                  '---------+--'
      ^      |                                        ^      |
      |      |  Client-Server API                     |      |
      |      V                                        |      V
+-----+------------+                            +-----+------------+
|                  +--------------------------->|                  |
| Provider/Server  |                            | Provider/Server  |
|        A         |<---------------------------+        B         |
+-----+------------+   Server-Server Protocol   +------------------+
      |     ^
      |     |                      +------------------+
      |     +----------------------+                  |
      |                            | Provider/Server  |
      +--------------------------->|        C         |
                                   +------------+-----+
                                         ^      |
                                         |      |
                                         |      V
                                      .--+---------.
                                     |   Client C   |
                                      '------------'
~~~

This diagram is simplified to show a single client per provider - a provider MAY
have multiple clients and/or users.

Servers (providers) are identified by their DNS name, as described in LM.

**TODO**: Improve server name reference/bring section here?

# Client-Server API

This document uses gRPC to describe client-server API operations, but does not require
a server to use gRPC for such operations. The client-server gRPC operations are purely
for semantics.

The operations here are inspired by Matrix's existing Client-Server API semantics as
well as {{?I-D.robert-mimi-delivery-service}} for MLS specifics.

## Operation: Create Room

Clients MAY either request a room ID from their server prior to this operation, or
if the server supports client-generated localparts the client can submit that instead.

The room ID is used as the group ID for the MLS group.

~~~
rpc CreateRoom(CreateRoomRequest) returns (CreateRoomResponse) {}

message CreateRoomRequest {
  string room_id = 0;

  // TODO: MLS?
}
~~~

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
