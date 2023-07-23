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

Linearized Matrix {{!I-D.ralston-mimi-linearized-matrix}} describes the access control semantics for
a messaging protocol using MLS. This document describes how servers and clients interact with each other
to ensure messages are delivered.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document makes use of {{!I-D.ralston-mimi-terminology}}.


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
