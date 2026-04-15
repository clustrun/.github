# clust

Self-healing container runtime with built-in mTLS mesh. Zero external dependencies.

Your app just makes HTTP calls. Each container gets a private point-to-point link to its host — no shared bridge, no network to sniff. Between nodes, every connection is mTLS. No sidecars, no SDKs, no TLS config in your app.

## Install

```sh
curl -sfL https://raw.githubusercontent.com/clustrun/install/main/install.sh | sh
```

## Get Started

```sh
clust create mycluster --quick                          # create cluster + start it
clust service canary.demo.internal deploy --image=traefik/whoami:v1.8
clust curl https://canary.demo.internal/
```

## Deploy a New Version

```sh
clust service canary.demo.internal deploy --image=traefik/whoami:v1.9
```

## Deploy Safely

Review before pushing:

```sh
clust service canary.demo.internal set --image=traefik/whoami:v1.10
clust service canary.demo.internal diff                 # review changes
clust service canary.demo.internal deploy
```

Test alongside production with a canary branch:

```sh
clust service canary.demo.internal branch next --image=traefik/whoami:v1.10 --weight=10
clust service canary.demo.internal deploy               # 90% primary, 10% next
clust curl https://next.canary.demo.internal/health     # test the branch directly
clust service canary.demo.internal promote next         # next becomes primary
clust service canary.demo.internal deploy               # deploy promoted config
```

## Experiment

Blue/green with a dark branch:

```sh
clust service canary.demo.internal branch green --image=traefik/whoami:v1.11
clust service canary.demo.internal deploy               # green running, 0% traffic

clust curl https://green.canary.demo.internal/health    # test the dark branch

clust service canary.demo.internal set green --weight=100
clust service canary.demo.internal deploy               # 0% primary, 100% green

clust service canary.demo.internal promote green        # green becomes primary
clust service canary.demo.internal deploy
```

## Control What a Service Can Reach

```sh
clust service canary.demo.internal egress https://checkip.amazonaws.com/
clust service canary.demo.internal deploy
clust curl https://canary.demo.internal/myip            # works
clust service canary.demo.internal egress --rm https://checkip.amazonaws.com/
clust service canary.demo.internal deploy
clust curl https://canary.demo.internal/myip            # blocked
```