# tkgi-demo - matomo
bitnami matomo offers the following format

- cloud instance
⋅⋅* GCP
⋅⋅* AWS
⋅⋅* Azure
- mac installer
- open virtual appliance (ova)

###  please note that the following  configurations are not meant to be used in production, please review and adjust for your environment

#### environment
- ops manager 2.10.11
- tkgi 1.11
- harbor 2.1.2

#### demo
- matomo

Since matomo is not packaged as an helm chart, we need to get some prerequisite ready first

<<<<<<< HEAD
1. define a default storageclass (if not already defined)
⋅⋅* required for our database engine and matomo persistent data
2. install a supported database engine
=======
- define a default storageclass (if not already defined)
⋅⋅* required for our database engine and matomo persistent data
- install a supported database engine
>>>>>>> 0181276415180bd1144c0c6b41d19f6caa4f3e13
⋅⋅* in this example we will use mariadb

then we need define some manifest in order to make it run on k8s

<<<<<<< HEAD
1. deployment
2. service
⋅⋅* ingress controller
3. persistent volume claim (pvc)
=======
- deployment
- service
⋅⋅* ingress controller
- persistent volume claim (pvc)
>>>>>>> 0181276415180bd1144c0c6b41d19f6caa4f3e13

### steps

configure storage class (if not present)

```yaml
kubectl apply -f sc.yaml
```

install mariadb

```shell
helm repo add bitnami
helm repo update
helm install mariadb \
  --set auth.rootPassword=[password],auth.database=bitnami_matomo \
    bitnami/mariadb
```  

apply the manifest

```yaml
kubectl apply -f matomo-deployment.yaml,matomo-pvc.yaml,matomo-service.yaml
```
