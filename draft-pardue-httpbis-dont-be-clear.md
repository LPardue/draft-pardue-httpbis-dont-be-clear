---
title: Reserving the clear ALPN Protocol ID
abbrev: Reserving clear
docname: draft-pardue-httpbis-dont-be-clear-latest
category: std

ipr: trust200902
keyword: Internet-Draft

stand_alone: yes
pi: [toc, sortrefs, symrefs]

author:
 -
    ins: L. Pardue
    name: Lucas Pardue
    org: Cloudflare
    email: lucaspardue.24.7@gmail.com

 -
    ins: A. Ramine
    name: Anthony Ramine
    org: Cloudflare
    email: tbd@tbd.com



--- abstract

HTTP Alternative Services (Alt-Svc) are identified by a tuple of
Application-Protocol Layer Negotiation (ALPN) protocol identifier, a host and a
port. The wire format for Alt-Svc is defined in ABNF and encodes this tuple or
the keyword "clear", which has a special meaning. This memo reserves the ALPN
protocol identifier "clear" to reduce the chances of accidental aliasing with
the "clear" keyword.

--- note_Note_to_Readers

*RFC EDITOR: please remove this section before publication*

Source code and issues list for this draft can be found at
<https://github.com/LPardue/draft-pardue-httpbis-dont-be-clear>.


--- middle

# Introduction

HTTP Alternative Services (Alt-Svc) {{!ALTSVC=RFC7838}} are identified by a
tuple of Application-Protocol Layer Negotiation (ALPN) {{!ALPN=RFC7301}}
protocol identifier, a host and a port. The wire format for Alt-Svc is defined
in ABNF and encodes this tuple or the keyword "clear", which has a special
meaning. This memo reserves the ALPN protocol identifier "clear" to reduce the
chances of accidental aliasing with the "clear" keyword.


## Conventions and Definitions {#defs}

{::boilerplate bcp14}


# Aliasing and Avoidance

{{ALTSVC}} Section 3 defines the Alt-Svc header field defined in ABNF. The value
can either be the keyword "clear", or an `alt-value` which includes an encoded
ALPN protocol identifier.

The Alt-Svc header field requires a custom parser, which introduces a
possibility for implementation failure. There is a chance that someone defines the ALPN
protocol identifier "clear", which could lead to a naive parser confusing the too. The "clear" keyword is a special value which invalidates cached alternative services. Confusion between keyword and protocol identifier might lead to detrimental effects.

To prevent unintented aliasing, this document registers the "clear" ALPN
protocol identifier and which relates to no application-layer protocol,
effectively reserving it and preventing any unintended aliasing.

# Security Considerations {#security}

Broken Alt-Svc header field parsers might confuse a "clear" keyword with a
"clear" ALPN protocol identifier. This could invalidate Alternative Service
cache state but a conformant client should fall back safely as described in
Section 2.4 of {{ALTSVC}}.


# IANA Considerations

## Registration of "clear" Identification String

This document creates a new registration, "clear", in the "Application-Layer
Protocol Negotiation (ALPN) Protocol IDs" registry established in {{ALPN}}.

The "clear" string is a reserved value that does not identify any protocol:

  Protocol:
  : Reserved

  Identification Sequence:
  : 0x63 0x6C 0x65 0x61 0x72 ("clear")

  Specification:
  : This document

--- back

# Acknowledgments {#acks}
{:numbered="false"}

Your name here.
