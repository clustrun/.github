# clust

Self-healing container runtime with mTLS mesh. Deploy containers with mutual TLS on every connection — no sidecars, no SDKs, no service mesh config in your app.

Three binaries, zero external dependencies:
- **supervisord** — Raft consensus, embedded CA, NATS
- **workerd** — container lifecycle, embedded mesh proxy, embedded DNS
- **gatewayd** — dual-homed ingress proxy, WebSocket gateway

Containers talk plain HTTP. The mesh is transparent — your app just does `GET http://other-service/` and clust handles identity, encryption, and routing.

## Install

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh
```

Or a specific version:

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh -s -- 0.1.0
```
