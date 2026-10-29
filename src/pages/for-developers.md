---
layout: ../layouts/ContentPage.astro
title: Get started with ANS
eyebrow: Get started
heading: Try the protocol. Inspect the evidence.
description: Run a local registration lifecycle, choose an SDK, and add identity verification to an application or gateway.
---

## Local quickstart

The Go reference implementation includes a Registration Authority, Transparency
Log, offline verifier, and development DNS server. The demo registers an agent and
verifies a SCITT receipt locally.

**Prerequisites:** Git, Make, Go 1.26+, OpenSSL, curl, and jq. Check the
[reference quickstart](https://github.com/agentnameservice/ans#quickstart-60-seconds)
for current requirements.

```sh
git clone https://github.com/agentnameservice/ans
cd ans
make build
scripts/demo/start.sh
scripts/demo/run-lifecycle.sh
```

Look for `VERIFIED` in the offline-verification stage. Stop the demo afterward:

```sh
scripts/demo/stop.sh
```

**Local development only:** the default demo uses development keys and a `noop`
DNS verifier. A passing receipt check does not test public DNS, production
certificate issuance, or a live deployment. Use the repository's local DNS guide
to exercise DNS validation.

## Choose your tools

- [Go SDK and CLI](https://github.com/agentnameservice/ans-sdk-go): registry and
  transparency clients, verification, and command-line tools.
- [Rust libraries](https://github.com/agentnameservice/ans-sdk-rust): API clients,
  shared types, and verification libraries with rustls support.
- [Java SDK](https://github.com/agentnameservice/ans-sdk-java): registration,
  discovery, cryptography, and agent client modules.

Use each project's installation guide and release notes for its supported features
and versions. The SDKs have different APIs and coverage.

## Integrate verification

1. **Choose your authority and trust roots.** Configure Registration Authority
   and Transparency Log endpoints explicitly. Decide which log keys and identities
   your application trusts.
2. **Register and publish.** Prove control of your domain, complete the certificate
   workflow, publish the DNS records returned by your RA, and wait for activation.
3. **Verify peers and authenticate callers.** Follow the ANS-6 procedures for
   certificates, identity, status, and possession. Select mTLS or DPoP for your
   topology and your implementation's capabilities.
4. **Apply authorization.** Map the authenticated identity to permitted actions.
   Test expiration, revocation, replay rejection, certificate rotation, and
   unavailable verification evidence.

## Follow a working example

- [Java protocol examples](https://github.com/agentnameservice/ans-sdk-java/tree/main/ans-sdk-agent-client/examples)
  cover A2A, MCP, and HTTP clients and services.
- [Go DPoP example](https://github.com/agentnameservice/ans-sdk-go/tree/main/examples/a2a-no-mtls)
  demonstrates application-layer proof of possession.
- [Rust MCP client](https://github.com/agentnameservice/ans-sdk-rust/blob/main/crates/ans-verify/examples/mcp_mtls_client.rs)
  demonstrates MCP over mTLS.
- [Gateway authentication](https://github.com/agentnameservice/ans-gateway-auth)
  includes recipes for agentgateway and Agent Router.

Review each example's configuration and coverage before deployment. For wire-level
contracts, use the [OpenAPI definitions and schemas](https://github.com/agentnameservice/ans-registry/tree/main/api).
