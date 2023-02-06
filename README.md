# workflow
```
minikube start
```

```
kubectl create namespace argo
```

```
kubectl apply -n argo -f https://github.com/argoproj/argo-workflows/releases/download/v3.4.4/install.yaml
```

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
```
kubectl -n argo port-forward deployment/argo-server 2746:2746
```

```
kubectl create rolebinding default-admin --clusterrole=admin --serviceaccount=argo:default --namespace=argo
```

```
argo submit -n argo --watch cyber-workflow.yaml
```
![local](https://i.ibb.co/BtbPPBP/Screenshot-2023-02-06-at-10-38-31-PM.png)
![argo dashborad](https://i.ibb.co/fDgFTzS/Screenshot-2023-02-06-at-10-45-09-PM.png)

