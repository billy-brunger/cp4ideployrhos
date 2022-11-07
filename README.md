## Cloud Pak for Integration CLI Deployment on RedHat Openshift 

[Redhat Openshift Cluster for CP4I (Techzone)](https://techzone.ibm.com/collection/cloud-pak-for-integration-activation-kit-v-2#tab-3)

**1) Create a namespace to install CP4I**
    
    oc new-project cp4i

**2) Import the catalog source into the cluster**
    
    oc apply -f catalog.yaml

**3) Install the operators**
  
    oc apply -f operator-group.yaml

    oc apply -f subscription.yaml
    
    repeat the command but replace <subscription.yaml> with the operators you want to install (refer to index.md)
    

    To test if the installation was successful run the following command
        oc get csv -n openshift-operators

**4) Add entitlement for specific namespace ([add your entitlement key](https://myibm.ibm.com/products-services/containerlibrary))**
    
    oc create secret docker-registry ibm-entitlement-key \
     --docker-username=cp \
     --docker-password='entitlement key' \
     --docker-server=cp.icr.io \
     --namespace=cp4i \

**5) Installing the platform navigator UI**
       
     oc apply -f platform-ui-instance.yaml
     
## Deploying the Cloud Pak via Openshift UI 

**1) Creating a Namespace**

    Goto Home -> Projects 
    Then Select 'Create Project'
    Call the project "cp4i"
    
**2) Importing the Catalog**
     
     Click the '+' Icon in the top right of the Header
     Copy & Paste the YAML from catalog.yaml
     Hit Create 
     
**3) Installing the operators**
     
     Goto Operators -> Operator Hub
     Now search for Cloud Pak for Integration
     Install it
     Repeat for all the capabilities you want
     
**Alternatively you can install the operators by doing step 2 again - this time copy & pasting the yaml files called subscriptionX.yaml (refer to index.md for product names)** 

**4) Adding your entitlement key**

    In the left navigation, click Workloads > Secrets
    Create -> Image pull secret 
        Secret Name: ibm-entitlement-key
        Authentication Type: Image registry credentials
        Registry server address: cp.icr.io
        Username: cp
        Password: [your entitlement key](https://myibm.ibm.com/products-services/containerlibrary)
        Email: optional
        
**5) Deploying the Platform Navigator UI**

     Click the '+' Icon in the top right of the Header
     Copy & Paste the YAML from platform-ui-instance.yaml
     Hit Create 

