# k3s-dev


# Local Kubernetes Install

## k3s install

```sh
curl -sfL https://get.k3s.io | sh -
```

## k3s uninstall


```sh
/usr/local/bin/k3s-uninstall.sh
```

## Helm Install

```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```



<!-- ## kubectl Install

```sh
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
# If the folder `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
sudo apt-get update
sudo apt-get install -y kubectl
``` -->

## kubectl setup

<!-- ```sh
sudo chmod 777 /etc/rancher/k3s/k3s.yaml
``` -->

```sh
cat /etc/rancher/k3s/k3s.yaml
```
from the Linux machine and save it to your local workstation in the directory 
```sh
nano ~/.kube/config
```


```sh
kubectl get all
```

```sh
kubectl get services -n kube-system
```


## Setup https

```sh
kubectl edit deployment traefik -n kube-system
```

### Add Args
spec -> template -> spec -> container

```sh
      args:
        - --certificatesresolvers.le.acme.email=huzaifairfan2001@gmail.com
        - --certificatesresolvers.le.acme.storage=/data/acme.json
        - --certificatesresolvers.le.acme.tlschallenge=true
```



### install cert manager

<!-- ```sh
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.17.2 \
  --set crds.enabled=true
``` -->


## Nginx Deployment

```sh
kubectl create configmap nginx-index --from-file=index.html
```


```sh
kubectl apply -f nginx-deployment.yaml
```

```sh
kubectl apply -f nginx-ingressroute.yaml
```

## Delete Deployment

```sh
kubectl delete -f nginx-deployment.yaml 
```

```sh
kubectl delete -f nginx-ingressroute.yaml
```


## Kubernetes Management Tool

### Lens

```sh
https://docs.k8slens.dev/getting-started/install-lens/#install-lens-desktop-from-the-apt-repository
```
