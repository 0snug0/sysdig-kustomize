# Sysdig-Kustomize
Deploy Sysdig on GKE, works for clusters with Ubuntu and COS node-pools

Uses default Node Labels to deploy on COS or Ubuntu nodes, for Ubuntu:

```
      nodeSelector:
        cloud.google.com/gke-os-distribution: ubuntu
```
And COS
```
      nodeSelector:
        cloud.google.com/gke-os-distribution: cos
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

More to come :)