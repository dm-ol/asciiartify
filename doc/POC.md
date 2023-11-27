### Installing ArgoCD

![Instruction](622997.gif)

# Add an alias to speed up command entry

alias k=kubectl

# Create the cluster

k3d cluster create argo

# Check for the presence of the configuration file

code ~/.kube/config

# Check cluster info

k cluster-info
k get all -A

# Installing ArgoCD

k create namespace argocd
k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Check created namespace

k get ns

# Check for ArgoCD pods

k get pod -n argocd

# Installing ArgoCD CLI

curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

# The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. You can simply retrieve this password using the argocd CLI

argocd admin initial-password -n argocd

# or

k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d;echo

# Kubectl port-forwarding can also be used to connect to the API server without exposing the service

k port-forward svc/argocd-server -n argocd 8080:443

# The API server can then be accessed using <https://localhost:8080>
