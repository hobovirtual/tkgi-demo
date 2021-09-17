# tkgi-demo - matomo
bitnami matomo offers the following format

- cloud instance
-- GCP
-- AWS
-- Azure
- mac installer
- open virtual appliance (ova)

###  please note that the following  configuration are not meant to be used in production

#### environment
- ops manager 2.10.11
- tkgi 1.11
- harbor 2.1.2

#### demo
- matomo

Since matomo is not packaged as an helm chart, we need to get some prerequisite ready first

- define a default storageclass (if not already defined)
-- required for our database engine and matomo persistent data
- install a supported database engine
-- in this example we will use mariadb

then we need define some manifest in order to make it run on k8s

- deployment
- service
-- ingress controller
- persistent volume claim (pvc)

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