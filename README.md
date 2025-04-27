# k3s-dev


# Local Kubernetes Install

## k3s install

```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.32.3+k3s1" sh -s - server --cluster-init
```

## Helm Install

```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```



## kubectl Install

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
```

## kubectl setup

/etc/rancher/k3s/k3s.yaml from the Linux machine and save it to your local workstation in the directory ~/.kube/config

```sh
kubectl get all
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

```sh
helm install cert-manager jetstack/cert-manager   --namespace cert-manager   --create-namespace   --version v1.13.1   --set installCRDs=true
```