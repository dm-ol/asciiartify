### Installing ArgoCD
![](622997.gif)

# Add an alias to speed up command entry
alias k=kubectl

# Create the cluster
k3d cluster create -a 3 aaclust

# Check for the presence of the configuration file
code ~/.kube/config

# Installing ArgoCD 
k create namespace argocd
k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Check for ArgoCD pods
k get pod -n argocd

# Installing ArgoCD CLI
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

# Check for ArgoCD pods
k get pod -n argocd

# The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. You can simply retrieve this password using the argocd CLI:
argocd admin initial-password -n argocd

# Kubectl port-forwarding can also be used to connect to the API server without exposing the service.
k port-forward svc/argocd-server -n argocd 8080:443

# The API server can then be accessed using https://localhost:8080