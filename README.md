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