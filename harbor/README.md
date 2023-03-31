# harbor

## deployment

Deploy in stages.

* sync namespace
* sync `harbor-ingress-cert` - this will create the ingress secret
* sync the rest
