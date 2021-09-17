# tkgi-demo * smb csi drive
in this section we will demo the installation of the smb csi driver, apply some specifics for tkgi and then use it to mount a windows share

###  please note that the following configurations are not meant to be used in production, please review and adjust for your environment

#### environment
* ops manager 2.10.11
* tkgi 1.11
* harbor 2.1.2

#### demo

high level csi smb driver
* csi smb driver installation
* apply csi smb driver modification
* create demo pod|pv
  - validation steps
* define a default storageclass (optional)
  - allowing pod can create persistent volume 

### steps

install the csi smb driver

follow the steps from official [https://github.com/kubernetes-csi/csi-driver-smb]: csi-driver-smb

#### important please review the manifest and customize any parameters between []

csi smb driver modification

```
kubectl apply -f csi-smb-controller.yaml,csi-smb-driver.yaml,csi-smb-node.yaml,rbac-csi-smb-controller.yaml
```  

demo - create a basic/custom index.html on the targeted windows share

```
<html>
    <h1>welcome</h1>
    </br>
    <h1>hello from Kubernetes storage - using windows share!!!!!</h1>
</html>
```

demo - create persistentvolume and deploy test pod

```
kubectl apply -f pod-smb.yaml,pv-smb.yaml,pvc-smb.yaml
```

test

```
kubectl exec -it pod-smb -- /bin/bash
curl localhost
  *the output shoudl match the content of the index.html*
```

configure storageclass

```
kubectl apply -f sc.yaml
```