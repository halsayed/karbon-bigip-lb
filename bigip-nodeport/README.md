## Intergrate F5 Big-IP with Karbon

This deployment mode will be based on nodeport and will use classical way to configure F5 using ConfigMaps

**Deploy F5 CIS:**

    kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=XXXXXX
    
    kubectl create serviceaccount k8s-bigip-ctlr -n kube-system
    kubectl create clusterrolebinding k8s-bigip-ctlr-clusteradmin --clusterrole=cluster-admin --serviceaccount=kube-system:k8s-bigip-ctlr

**Note:** In production you want to define a custom cluster role for CIS, please refer to BigIP docs


    kubectl create -f f5-cis-nodeport-deployment.yaml

**Deploy sample application:**

    kubectl create -f sample-app.yaml
    kubectl create -f sample-service.yaml
    kubectl create -f sample-ingress.yaml
    


