# clust

Self-healing container runtime with built-in mTLS mesh. Zero external dependencies.

Your app just makes HTTP calls. Each container gets a private point-to-point link to its host — no shared bridge, no network to sniff. Between nodes, every connection is mTLS. No sidecars, no SDKs, no TLS config in your app.

## Install

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh
```

## Quick Start

```sh
clust init                                              # one-time user setup
clust create mycluster --quick                          # Docker defaults, no wizard
clust up                                                # pull images, start cluster
clust service init hello.demo.internal --image=traefik/whoami:v1.11.0
clust service deploy hello.demo.internal                # seal draft + deploy
clust curl https://hello.demo.internal/
```

## Ship a New Version

```sh
clust service set hello.demo.internal --image=traefik/whoami:v1.12.0
clust diff                                              # review pending changes
clust service deploy hello.demo.internal                # seal + deploy
```
