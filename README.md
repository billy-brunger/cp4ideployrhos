# Cloud Pak for Integration automated deployment
Automating deployment of CP4I using tekton pipelines

1) Create a namespace to install CP4I
    
    oc new-project cp4i

2) Import the catalog source into the cluster
    
    oc apply -f catalog.yaml

3) Install the operators
  
    oc apply -f operator-group.yaml

    oc apply -f subscription.yaml

    To test if the installation was successful run the following command
        oc get csv -n openshift-operators

4) Add entitlement for specific namespace (add your entitlement key to the command)
    oc create secret docker-registry ibm-entitlement-key \
     --docker-username=cp \
     --docker-password='entitlement key' \
     --docker-server=cp.icr.io \
     --namespace=cp4i \

5) Installing the platform navigator UI
        oc apply -f platform-ui-instance.yaml

        

