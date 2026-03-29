# clust

Self-healing container runtime with mTLS mesh. Deploy containers with mutual TLS on every connection — no sidecars, no SDKs, no service mesh config in your app.

Three binaries, zero external dependencies:
- **supervisord** — Raft consensus, embedded CA, NATS
- **workerd** — container lifecycle, embedded mesh proxy, embedded DNS
- **gatewayd** — dual-homed ingress proxy, WebSocket gateway

Your app just makes HTTP calls. Each container gets a private point-to-point link to its host — no shared bridge, no network to sniff. Between nodes, every connection is mTLS. No TLS config in your app.

## Install

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh
```

Or a specific version:

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh -s -- 0.1.0
```
