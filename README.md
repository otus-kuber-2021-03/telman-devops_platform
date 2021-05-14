
# Kubernetes-templating
## Add repo
```
helm3 repo add stable https://charts.helm.sh/stable
```

## Ingress-nginx
```
helm3 upgrade --install ingress-nginx stable/ingress-nginx --wait --namespace=ingress-nginx --version=3.17.0

k -n ingress-nginx get svc 
```

## Cert-manager
```
k create ns cert-manager

helm3 install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.1.0 --set installCRDs=true

k apply -f kubernetes-templating/cert-manager/test-resources.yaml

k apply -f kubernetes-templating/cert-manager/letsencrypt-production.yaml
```

## Chartmuseum
```
k create ns chartmuseum

helm3 upgrade --install chartmuseum stable/chartmuseum --wait --namespace=chartmuseum --version=2.13.2 -f kubernetes-templating/chartmuseum/values.yaml

k -n chartmuseum get certificate
```

## Chartmuseum wt star
```
helm3 plugin install https://github.com/chartmuseum/helm-push

helm3 repo add --username {USERNAME}--password {PASSWORD} chartmuseum_repo http://chartmuseum.{IP_ADDRESS}.nip.io

helm3 push {CHART_NAME} chartmuseum_repo

helm3 search {CHART_NAME}

helm3 repo update chartmuseum_repo
```

# Kubernetes Monitoring
Установка kube-prometheus-stack через helm3
```
helm3 upgrade --install prometheus prometheus-community/kube-prometheus-stack -f kubernetes-monitoring/kube-prometheus-stack/values.yaml

k appy -f config-map.yaml deployment.yaml service.yaml ingress.yaml service-monitor.yaml
```
