# Kiali Cheat Sheet

## Get Kiali Token
powershell:
```powershell
$base64token=$(kubectl get secret -n istio-system $(kubectl get sa kiali-service-account -n istio-system -o jsonpath=`{.secrets[0].name`}) -o jsonpath=`{.data.token`})
$token=[Text.Encoding]::Utf8.GetString([Convert]::FromBase64String($base64token))
```
bash:
```shell
token=$(kubectl get secret -n istio-system $(kubectl get sa kiali-service-account -n istio-system -o jsonpath={.secrets[0].name}) -o jsonpath={.data.token} | base64 -d)
```