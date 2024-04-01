# provisioning
This repo is aimed to provide cluster as a service

## Procedure
**Creating cluster DT:**

1. Go to provisioning repo and creates the workspace to the DT: 
  Folders and zones (edge, region, wavelength) and each one 
  with the ```NAME_CLUSTER.yaml``` file

    1.1. Modify the ```NAME_CLUSTER.yaml``` file to creates clusters

    1.2. ```clusters["name"]  = NAME_CLUSTER and NAME_CLUSTER.yaml ``` file must be the same

2. Go to the auto-ztp repo and creates the
   workspace to the DT: Folders and zones (edge,
    region, wavelength) and each other with the 
    content as digital-twins-example folder and
    push the changes

3. Go to the ```iac-terragrunt``` repo
    and creates the workspace to the DT. Call the 
    subnets module tf and configure the terragrunt.hcl.
    to each cluster and push the changes

4. Return to the provisioning repo and push the changes the 
    ```dt/NAME_DT``` branch

5. When push branch. Wait a few seconds. Wait until the 
    GitHub Actions has been finished. 

    5.1 Go to the argocd GUI, filter for project clusters and you will see 
        the cluster ir synced automatically and it's deploying. Wait ultil the
        cluster is deployed

6. If the intention is to create a cluster in edge. 
    
    6.1 Go to the ```iac-terragrunt``` in the workspace
    of the DT. 
    
    6.2 Call a ```eni-lni``` tf module with the terragrunt.hcl file.
    Go to the console AWS and check the id of each EC2 of the cluster

    6.3 Pull the changes in the main branch

7. Go to the provisioning repo. Approve and merge the changes to main
    The cluster(s) is ready to work

**Deleting Cluster DT:**

1. Go to provisioning repo and delete the file regarding to the name cluster 
   (```ex: telefonica/edge/telefonica.yaml```) and push the changes in ```dt/NAME_DT.```
    1.1 Wait until all actions jobs in the pull requests has been successfully finished

2. If cluster in edge. Go to the ```iac-terragrunt``` and repo delete the related 
    parameters of the cluster in ```eni-lni/terragrunt.hcl``` and push the changes in main

3. Go to the provisioning repo and in the Pull Request merge the changes to main
    the cluster will be deleted automatically

2. Go to the ```iac-terragrunt``` repo and delete the related 
    parameters of the cluster in ```subnets/terragrunt.hcl``` and push the changes in main
    