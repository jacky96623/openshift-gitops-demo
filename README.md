# openshift-gitops-demo

## Prerequisites

### Ingress-Nginx Controller (KIC)

#### Install

```sh
#!/usr/bin/env sh
# Ref: https://kubernetes.github.io/ingress-nginx/deploy/#quick-start
set -e

oc create ns ingress-nginx
oc -n ingress-nginx adm policy add-scc-to-user privileged \
  -z ingress-nginx-admission \
  -z ingress-nginx
helm -n ingress-nginx install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --set controller.service.type=ClusterIP

```

#### Remark

We may need to expose the `ingress-nginx` service via:

```sh
oc -n ingress-nginx expose svc/ingress-nginx-controller --name <route name> --hostname <FQDN>
```
