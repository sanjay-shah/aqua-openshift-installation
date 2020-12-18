# Aqua Security OpenShift Installation Steps


## Storage Class(sc) and Persitent Volume(pv)

Aqua requires sc and pv for aqua-db and aqua-web
Follow this [link](https://github.com/code-ready/crc/wiki/Dynamic-volume-provisioning) to create local storage on your local OpenShift development environment or crc vm.

## Aqua serviceaccount privilaged access
Before aqua is installed, aqua-sa service account need to be added to the privlaged user group on your cluster. This is needed becasue aqua needs privilaged access to cluster resource. Run the oc command below to add aqua-sa serviceaccoiunt in aqua namespace to privilaged access user group.

`oc adm policy add-scc-to-user privileged -z aqua-sa -n aqua`

## Install aqua with aquactl

Download the Aquactl binary from the appropriate link:

Linux: https://get.aquasec.com/aquactl/stable/aquactl
MacOS: https://get.aquasec.com/aquactl/mac/stable/aquactl
    
Run the following command to install aqua. 

`./aquactl deploy csp`

Select Red Hat OpenShift as Platform.
