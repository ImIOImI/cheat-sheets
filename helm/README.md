###Updating helm
It's my opinion that `upgrade --install` should be the default way helm interacts with k8s. It
basically means "upgrade the package and if it doesn't exist install it."

```powershell
#In Powershell:
helm upgrade --install `
    <install name> . `
    --set <key>=<value> `
```

```bash
#In bash
helm upgrade --install \
    <install name> . \
    --set <key>=<value> `
```

###Debugging
```shell script
helm lint

#render templates, then return the manifest files
helm install --dry-run --debug

#shows what is installed on the server, already
helm get manifest

#Debug the entire deployment and output all the yaml to test.yaml
helm template --debug . > test.yaml
```