
# Steps to deploy an app and connect it with nginx-ingress controller in Digital Ocean

- Create kubernetes cluster in Digital Ocean and Prepare for `kubectl`

- Install ingress-nginx in cluster (ref: https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes)

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.1/deploy/static/provider/do/deploy.yaml
```

- Check installation
```
kubectl get pods -n ingress-nginx \
  -l app.kubernetes.io/name=ingress-nginx --watch

# and

kubectl get svc --namespace=ingress-nginx
```

- Prepare deployment, service and ingress templetes for app

- Add this annotation in ingress template

```
metadata:
  name: nginx-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
```

- Apply templates into cluster

# HTTPS (optional)

- Fill-in certificate and key in tls-secret.yaml and Apply into cluster

- Add tls in ingress 
```
spec:
  tls:
  - hosts:
    - example.com
    secretName: ingress-nginx-tls
```
