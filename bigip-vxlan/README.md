## Install F5 CIS

**BIG-IP credentials and CIS service account and role:**


    kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=XXXXX
    kubectl create -f cis/f5-cis-rbac.yaml

**Create CIS CRD:**

    kubectl create -f https://raw.githubusercontent.com/F5Networks/k8s-bigip-ctlr/master/docs/config_examples/customResourceDefinitions/customresourcedefinitions.yml


**Deploy CIS controller:**

Customize the deployment and node file with environment settings and then deploy.

    kubectl create -f cis/f5-cis-deployment.yaml
    kubectl create -f cis/f5-bigip-node.yaml


## Install F5 IPAM

**F5 IPAM rbac:**

    kubectl create -f ipam/f5-ipam-rbac.yaml

**Create IPAM CRD:**

    kubectl create -f https://raw.githubusercontent.com/F5Networks/f5-ipam-controller/main/docs/_static/schemas/ipam_schema.yaml

**Create IPAM PVC:**

    kubectl create -f ipam/f5-ipam-pvc.yaml



**Deploy IPAM:**

    kubectl create -f ipam/f5-ipam-deployment.yaml


**NGINX CRD:**
    kubectl apply -f nginx/crd/k8s.nginx.org_virtualservers.yaml
    kubectl apply -f nginx/crd/k8s.nginx.org_virtualserverroutes.yaml
    kubectl apply -f nginx/crd/k8s.nginx.org_transportservers.yaml
    kubectl apply -f nginx/crd/k8s.nginx.org_policies.yaml


**Deploy nginx:**
    kubectl create -f nginx/ns-and-sa.yaml
    kubectl create -f nginx/rbac.yaml
    kubectl create -f nginx/default-server-secret.yaml
    kubectl create -f nginx/nginx-config.yaml
    kubectl create -f nginx/ingress-class.yaml
    kubectl create -f nginx/nginx-ingress.yaml
    kubectl create -f nginx/nginx-service.yaml
    