# Sysdig-Kustomize
Deploy Sysdig on GKE, works for clusters with Ubuntu and COS nodepools. Taking from steps [here](https://sysdigdocs.atlassian.net/wiki/spaces/Platform/pages/256475257/GKE+Agent+Installation+Steps)

The steps from the sysdig page are below as well, do the below from the `sysdig-kustomize` root
```
# create variables to use later
export SYSDIG_ACCESS_KEY={your_access_key}
export GCP_EMAIL={your_gcp_email}

# create the sysdig namespace
kubectl create ns sysdig-agent

# create the sysdig access secret
kubectl create secret generic sysdig-agent --from-literal=access-key=<your sysdig access key> -n sysdig-agent

# GKE 1.6 and later only
kubectl create clusterrolebinding your-user-cluster-admin-binding --clusterrole=cluster-admin --user=$GCP_EMAIL

# add serviceaccount
kubectl apply -f sysdig-agent-clusterrole.yaml -n sysdig-agent
kubectl create serviceaccount sysdig-agent -n sysdig-agent
kubectl create clusterrolebinding sysdig-agent --clusterrole=sysdig-agent --serviceaccount=sysdig-agent:sysdig-agent  
```

To run:
```
# Only running Ubuntu
kubectl apply -k base

# To deploy on COS nodes
kubectl apply -k overlays/gke-cos

# To deploy on Ubuntu nodes
kubectl apply -k overlays/gke-ubuntu
```

How `sysdig-kustomize` works:
`sysdig-kustomize` uses default Node Labels to deploy on COS or Ubuntu nodes, for Ubuntu:

```
      nodeSelector:
        cloud.google.com/gke-os-distribution: ubuntu
```
And COS
```
      nodeSelector:
        cloud.google.com/gke-os-distribution: cos
```


More to come :)
email me at elugo25111@gmail.com and soon to be lugo@sysdig.com :)