# harbor

## deployment

Deploy in stages.

* sync namespace
* sync `harbor-ingress-cert` - this will create the ingress secret
* create auth secrets
* sync the rest

## auth secrets

The following secrets need to be set up:

```bash
create secret generic harbor-admin-auth -n harbor \                                                                                                                  ─╯
--from-literal admin-password='********'
```

```bash
kubectl create secret generic harbor-secret-key -n harbor \                                                                                                                  ─╯
--from-literal secretKey='********'
```

```bash
kubectl create secret generic harbor-registry-auth -n harbor \                                                                                                               ─╯
--from-literal REGISTRY_PASSWD='********' \
--from-literal REGISTRY_HTPASSWD='$apr1$XLefHzeG$Xl4.s00sMSCCcMyJljSZb0' # example string
```
