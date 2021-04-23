# kubernetes networks


### Установка MetalLB
```
k apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/namespace.yaml

k apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/metallb.yaml

k create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
```

