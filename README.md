# Aqua Security OpenShift Installation Steps

## Install OpenShift-CLI(oc)

`brew install openshift-cli`

## Storage Class(sc) and Persitent Volume(pv) - Optional

If you're using [crc](https://developers.redhat.com/products/codeready-containers/download/) for local development, you need to provsion local storage or PersistentVolume for aqua-db and aqua-web.
Follow this [link](https://github.com/code-ready/crc/wiki/Dynamic-volume-provisioning) to create local storage on crc

## Login to OpenShift Cluster

`oc login -u kubeadmin -p <password> https://api.crc.testing:6443`

## Create Aqua project

`oc new-project aqua`

## Aqua serviceaccount privilaged access
Before aqua is installed, aqua-sa service account need to be added to the privlaged user group on your cluster. This is needed becasue aqua needs privilaged access to cluster resource. Run the `oc` command below to add aqua-sa serviceaccoiunt in aqua namespace to privilaged access user group.

`oc adm policy add-scc-to-user privileged -z aqua-sa -n aqua` This step may not be needed for aquactl2

## Install Aqua with aquactl

Download `aquactl v2` binary from the appropriate link:

Note: OpenShift issues have been fixed in `aquactl` v2

Linux: https://get.aquasec.com/aquactl/v2/aquactl \
MacOS: https://get.aquasec.com/aquactl/mac/v2/aquactl
    
Run the following command to install aqua. 

`./aquactl deploy csp`

Select Red Hat OpenShift as Platform and complete installation.

## Create Route for aqua-web UI and API

After Aqua installation completes sucessfully, create route using [server-route.yaml](server-route.yaml) file by running either `oc` or `kubectl` command.

`oc apply -f https://raw.githubusercontent.com/sanjay-shah/aqua-openshift-installation/main/server-route.yaml` \

## Access Aqua Web UI

On local crc https://aqua-web.apps-crc.testing \
On server [hostname](https://github.com/sanjay-shah/aqua-openshift-installation/blob/475417ab053bf55af7e7cdad85e39692fc803890/server-route.yaml#L8) provided in your route.


