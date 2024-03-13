# provisioning
This repo is aimed to provide cluster as a service

## Procedure
- Create a new branch (dt/NAME_OF_DIGTAL_TWINS)
- Follow the digital-twins-example folder. Use the folders edge, region or wavelength to configure the cluster.
- Automatically the Actions will create the PR with the new changes to be merged into main. Go to the argocd and sync
  the cluster. Wait up to the cluster be deployed. If the cluster is deployed in region zones, you need to create the
  vpc peering in aws. In edge you don't need configure the peering
- You must configure the folders following the digital-twins-examples stored in auto-ztp repository.
- When the PR is merge. Action will install the cluster-addons and will include the folders in sites/NAME_DIGIAL_TIWNS/ZONE/NAME_CLUSTER.
  The NAME_CLUSTER is getting of the values.yaml file