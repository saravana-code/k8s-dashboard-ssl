# k8s-dashboard-ssl
Add trusted SSL certificates to k8s dashboard with ingress

This way we are adding SSL certificate to k8s dashboard

Namespace used to install dashboard is "kube-system" this comes by default, if its not there create it using below command or you can change the namespace on files

```
kubectl create namespace kube-system
```
Make sure you have added SSL certs already , if not please use the below command to add the SSL certs

Replace ssl.crt,ssl.key with your actual files

```
kubectl create secret tls kubernetes-dashboard-tls --key ssl.key --cert ssl.crt -n=kube-system
```
Create a htpasswd, it will be used on basic-auth to login to the dashboard

```
htpasswd -c auth admin
```
Create a secret with the htpasswd created on the above step

```
kubectl -n kube-system create secret generic kubernetes-dashboard-auth --from-file=auth
```

Create deployments, service,ingress of k8s dashboard

```
kubectl create -f *.yml
```
You should be able to access your dns name (our example: "prod.example.com") using the link : https://prod.example.com/ with the username and password given on htpasswd
