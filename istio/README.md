## Debugging routing

`istoctl analyze -n <namespace>`

Print a list of all the routes registered in the ingress gateway
```
istioctl proxy-config routes -n istio-system $(kubectl get pods -n istio-system -o name | grep istio-ingress -m1)
```

## Debugging certs

Print a list of all the certs, whether or not they're valid, and when they expire
```
istioctl proxy-config secret -n istio-system $(kubectl get pods -n istio-system -o name | grep istio-ingress -m1)
```
