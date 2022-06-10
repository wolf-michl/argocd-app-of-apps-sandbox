# argocd-app-of-apps-sandbox

Just a simple sandbox project to try out Argo CD's app of apps pattern.

## Setup

```bash
argocd app create app-of-apps \
    --dest-namespace argocd \
    --dest-server https://kubernetes.default.svc \
    --repo https://github.com/wolf-michl/argocd-app-of-apps-sandbox.git \
    --path .
```

```bash
argocd app sync app-of-apps
```

```bash
argocd app sync -l app.kubernetes.io/instance=app-of-apps
```

## How does it work?

Argo CD's [cluster bootstrapping](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/)
documentation recommends
the [app of apps pattern](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/#app-of-apps-pattern)
approach to install many apps at once.

Our app of apps is defined in a helm chart (which is this repository).
The [Chart.yaml](Chart.yaml) is boilerplate which defines our app of apps as app-of-apps.
The [values.yaml](values.yaml) defines some default values which can then be used by the applications. This value.yaml
may also be completely empty, if we don't need any default values.
The [templates folder](templates) contains our real applications. They are defined as custom resources in form of YAML
files.
