##Debugging routing

`istoctl analyze -n <namespace>`

`istioctl proxy-config routes -n istio-system $(kubectl get pods -n istio-system | grep istio-ingress -m1 | awk '{print $1;}')`
