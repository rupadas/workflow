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
For Argo deploying
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

![local](https://i.ibb.co/23Xrtvv/Screenshot-2023-02-06-at-10-38-31-PM.png)

![argo dashborad](https://i.ibb.co/h70SZc4/Screenshot-2023-02-06-at-10-45-09-PM.png)

