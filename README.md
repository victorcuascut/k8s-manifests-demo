# k8s-manifests-demo

This is a sample k8s-manifest repo which can be used with ArgoCD and built and tested locally

# Kind Environment Setup
```
$ kind create cluster --config=kind.yaml
$ kubectl create namespace argocd
$ kubectl config set-context --current --namespace=argocd
```

# ArgoCD Install
```
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

# Access
 ```
 $ kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
 $ kubectl -n argocd port-forward svc/argocd-server -n argocd 8080:443
 ```
Log into https://127.0.0.1:8080 with username: admin and the password you got from the above command.
# Configure ArgoCD Repo
Once logged in go to settings > repositories and create a connection to your repo

Sample project can be used for this demo (Set Project as Default and set Repository URL to demo repo. No username and password needed)
https://github.com/victorcuascut/k8s-manifests-demo

# Create first ArgoCD Application
As the demo uses an app of apps design your initial application will point to a configuration under argocd within the repo.
Sample configuration
```
project: default
source:
  repoURL: 'https://github.com/victorcuascut/k8s-manifests-demo'
  path: ./argocd/overlays/all-in-one-cluster/
  targetRevision: HEAD
destination:
  server: 'https://kubernetes.default.svc'
  namespace: argocd
syncPolicy:
  automated:
    prune: true
    selfHeal: true
```