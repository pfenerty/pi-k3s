1. image sd cards with Ubuntu server 21.04

2. setup password-less ssh

```
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@192.168.xxx.xxx
```

3. update nodes

```
ansible-playbook update.yml -i inventory/pi-cluster/hosts.ini
```

4. install k3s

```
ansible-playbook site.yml -i inventory/pi-cluster/hosts.ini
```

5. copy kubeconfig

```
<k3s-master>:/etc/rancher/k3s/k3s.yaml
```

6. create secrets

```
kubectl apply -f flux/apps/dev/secrets/docker-hub-creds.secret.yaml
```

```
kubectl apply -f flux/apps/dev/secrets/drone-gitea.secret.yaml
```

5. run flux

```
flux bootstrap git --url=ssh://git@github.com/pfenerty/pi-k3s.git --path=flux/clusters/pi-cluster --private-key-file=<relative_path>
```