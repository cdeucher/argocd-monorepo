
# ArgoCD monorepo

```
https://argo-cd.readthedocs.io/en/stable/
```

+ Install ArgoCD on Minikube
```bash
minikube start

kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

minikube tunnel
```
+ Login
```
kubectl port-forward svc/argocd-server -n argocd 8080:443

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

argocd login $(minikube ip)
```

+ Examples
```
1)
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default

argocd app get guestbook
argocd app sync guestbook

2)
argocd app create app --repo https://github.com/cdeucher/argocd-monorepo.git --path app --dest-server https://kubernetes.default.svc --dest-namespace app
```
