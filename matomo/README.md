# tkgi-demo * matomo
in this section we will demo the installation of the bitnami matomo application, which is offered in the following format

* cloud instance
  - GCP
  - AWS
  - Azure
* mac installer
* open virtual appliance (ova)

normally for k8s an helm chart would be the best option, since it's not available, here's the steps to make this application run on tkgi
###  please note that the following configurations are not meant to be used in production, please review and adjust for your environment

#### environment
* ops manager 2.10.11
* tkgi 1.11
* harbor 2.1.2

#### demo
matomo high level

Since matomo is not packaged as an helm chart, we need to get some prerequisite ready first

* define a default storageclass (if not already defined)
  * required for our database engine and matomo persistent data
* install a supported database engine
  * in this example we will use mariadb

then we need define some manifest in order to make it run on k8s

* deployment
* service
  * ingress controller
* persistent volume claim (pvc)

### steps

#### important please review the manifest and customize any parameters between []

define a storageclass (if not present)

```
kubectl apply -f sc.yaml
```

install mariadb

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install mariadb \
  --set auth.rootPassword=[password],auth.database=bitnami_matomo \
    bitnami/mariadb
```  

apply the manifest

```
kubectl apply -f matomo-deployment.yaml,matomo-pvc.yaml,matomo-service.yaml
```
