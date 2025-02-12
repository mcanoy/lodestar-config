# Development on OpenShift

## Getting Started With Helm

This directory contains a Helm chart which can be used to deploy a development version of this app for rapid testing.

Before you use it, you will need to download & install Helm 3.

If you are not familiar with Helm - how to configure it and run - you can start with this quickstart:

[https://helm.sh/docs/intro/quickstart](https://helm.sh/docs/intro/quickstart)

## Using This Chart

1. Clone the target repo:

```
git clone https://github.com/rht-labs/lodestar-config
```

2. Change into to the `deployment` directory:

```
cd lodestar-config/deployment
```

3. Deploy using the following Helm command:

```shell script
helm template . \
  --values values-dev.yaml \
  --set git.uri=https://github.com/dwasinge/lodestar-config.git \
  --set git.ref=main \
  --set namespaces=<your-namespaces> \
| oc apply -f -
```

It accepts the following variables

| Variable  | Use  |
|---|---|
| `git.uri`  | The HTTPS reference to the repo (your fork!) to build  |
| `git.ref`  | The branch name to build  |

This will spin up all of the usual resources that this service needs in production, plus a `BuildConfig` configured to build it from source from the Git repository specified. To trigger this build, use `oc start-build lodestar-config`.

