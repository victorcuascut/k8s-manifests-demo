# k8s-manifests-demo

This is a sample k8s-manifest repo which can be used with ArgoCD

# Kind Environment Setup
```
$ kind create cluster --config=kind.yaml
$ kubectl create namespace argocd
$ kubens argocd
```

# ArgoCD Install
```
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

# Access
 ```
 $ kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
 ```

# Argo CD config
https://github.com/victorcuascut/k8s-manifests-demo