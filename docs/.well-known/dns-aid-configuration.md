# DNS for AI Discovery (DNS-AID) Configuration

## Overview

DNS-AID records enable agents to discover endpoints through DNS using ServiceMode
SVCB/HTTPS records. These records must be published at the DNS level for your
domain.

## Required Records

Add the following DNS records for `brownyx.com`:

```dns
; Agent discovery entrypoint
_index._agents.brownyx.com.   3600 IN SVCB 1 cel.brownyx.com. alpn="https" port=443 mandatory=alpn,port

; A2A protocol endpoint (if applicable)
_a2a._agents.brownyx.com.     3600 IN SVCB 1 cel.brownyx.com. alpn="a2a" port=443 mandatory=alpn,port
```

## Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `alpn`    | `https` or `a2a` | Application-Layer Protocol Negotiation identifier |
| `port`    | `443` | Target port for the endpoint |
| `mandatory` | `alpn,port` | Required SvcParam keys |

## DNSSEC

Sign the `_agents.brownyx.com` zone with DNSSEC so validating resolvers return
authenticated data. Most DNS providers support DNSSEC signing through their
control panel.

## Validation

Verify DNS-AID records via DNS-over-HTTPS:

```bash
# Query via Cloudflare
curl "https://cloudflare-dns.com/dns-query?name=_index._agents.brownyx.com&type=SVCB" \
  -H "accept: application/dns-json"

# Query via Google
curl "https://dns.google/resolve?name=_index._agents.brownyx.com&type=SVCB"
```

Expected response contains SVCB records with `alpn` and `port` parameters.

## References

- [DNS-AID Draft](https://datatracker.ietf.org/doc/draft-mozleywilliams-dnsop-dnsaid/)
- [RFC 9460 - Service Binding](https://www.rfc-editor.org/rfc/rfc9460)
