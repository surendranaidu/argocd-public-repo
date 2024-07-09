**setup k3d:**
curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash


**create a cluster:**
k3d cluster create argocd-cluster-2 --config cluster-config.yaml


**To set argocd:**
k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

**To install argocd:**
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd6
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

**To check commands argocd service and deployemnt**
k -n  argocd get deployment

k -n  argocd get services

**To set NodePort:**
k  patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

**To port-forward :**
k port-forward svc/argocd-server -n argocd 8081:443

**To get password :**
k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" |base64 -d && echo


**To port-forward :**
k port-forward svc/nginx-service -n default 8081:80

k scale deploy nginx-deployment --replicas 3
