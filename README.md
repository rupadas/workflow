# workflow
```
minikube start
```

For creating argo namespace
```
kubectl create namespace argo
```
Installing argo into agro name space
```
kubectl apply -n argo -f https://github.com/argoproj/argo-workflows/releases/download/v3.4.4/install.yaml
```
Patching this to run it in local server without cer file
```
kubectl patch deployment \
  argo-server \
  --namespace argo \
  --type='json' \
  -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/args", "value": [
  "server",
  "--insecure",
  "--auth-mode=server"
]}]'
```
For Argo port fowrward to check dashboard at localhost:2746
```
kubectl -n argo port-forward deployment/argo-server 2746:2746
```

To resolve access error while deploying
```
kubectl create rolebinding default-admin --clusterrole=admin --serviceaccount=argo:default --namespace=argo
```
Submitting the argo task and watch is for tracking the flow
```
argo submit -n argo --watch cyber-workflow.yaml
```

[![H1p3RYx.md.png](https://iili.io/H1p3RYx.md.png)](https://freeimage.host/i/H1p3RYx)
[![H1p3A2j.md.png](https://iili.io/H1p3A2j.md.png)](https://freeimage.host/i/H1p3A2j)

