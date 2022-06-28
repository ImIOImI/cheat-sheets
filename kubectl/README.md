## Node Operations
```powershell
#Gets a list of nodes
kubectl get nodes
#gets a list of all the pods running on a node
kubectl get pods --all-namespaces -o wide --field-selector spec.nodeName=<node name>
```

## Namespace Operations
```powershell
#delete a namespace and everything in it
kubectl delete namespace <namespace>
#create a namespace
kubectl create namespace <namespace>
```

## Describe Operations
```powershell
#describe all the pods in a names space
kubectl get pods -o wide --namespace sandbox
```

## Logs
```powershell
#tail a pod
kubectl --namespace sandbox logs --follow <Pod name>
```

## Iterate over a resource and do a thing
```powershell 
#kubectl get <resource> -n <namespace> -o name | xargs -I % kubectl <operation> -n <namespace>

#For example delete All HPAs and scale to 1
kubectl get hpa -n <namespace> -o name | xargs -I % kubectl delete % -n <namespace> ; kubectl get deploy -n <namespace> -o name | xargs -I % kubectl autoscale % --min=1 --max=1 -n <namespace>

#select all the pods where version label is v1 and add label foo=bar
kubectl get pods -n <namespace> -o name --selector=version=v1 | xargs -I % kubectl label % -n <namespace> foo=bar

#get all the deployments and restart them
kubectl get deploy -n <namespace> -o name | xargs -I % kubectl rollout restart % -n <namespace>

#add a label to all pod specs in deployments in a namespace 
kubectl get deploy -n <namespace> -o name | xargs -I  kubectl patch % -n <namespace> -p '{"spec": {"template": {"metadata": {"labels": {"<key>": "<value>"}}}}}'
```

## CRDs
```powershell 
#Get CRDs that are installed on the cluster
kubectl get --raw /openapi/v2 > openapi.json

kubectl get crds -o json
kubectl get crds -o yaml
```

## Launch Interactive Pod in a cluster
This is great to test DNS and such inside the cluster
```bash
kubectl run -n api -i --tty --rm debug --image=ubuntu --restart=Never -- 
```