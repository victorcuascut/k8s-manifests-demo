# k8s-manifests-demo

This is a sample k8s-manifest repo which can be used with ArgoCD

# Kind Environment Setup
Create Kind.yaml
```
# kind.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  - containerPort: 80
    hostPort: 80
    protocol: TCP
  - containerPort: 443
    hostPort: 443
    protocol: TCP
```

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
