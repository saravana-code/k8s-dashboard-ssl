# k8s-dashboard-ssl
Add trusted SSL certificates to k8s dashboard with ingress

This way we are adding SSL certificate to k8s dashboard

Namespace used to install dashboard is "kube-system" this comes by default, if its not there create it using below command or you can change the namespace on files

```
kubectl create namespace kube-system
```

Create a htpasswd, it will be used on basic-auth to login to the dashboard

```
htpasswd -c auth admin
```
Create a secret with the htpasswd created on the above step

```
kubectl -n kube-system create secret generic kubernetes-dashboard-auth --from-file=auth
```
