# clust

Self-healing container runtime with built-in mTLS mesh. Zero external dependencies.

Your app just makes HTTP calls. Each container gets a private point-to-point link to its host — no shared bridge, no network to sniff. Between nodes, every connection is mTLS. No sidecars, no SDKs, no TLS config in your app.

## Install

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh
```

Or a specific version:

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh -s -- 0.1.0
```

## Quick Start

```sh
clust init                              # one-time user setup
clust create mycluster --quick          # Docker defaults, no wizard
clust up                                # pulls images, starts cluster
clust deploy hello.demo.internal traefik/whoami:v1.11.0 --port 8080 --health-path /health
clust curl https://hello.demo.internal/
```
