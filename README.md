# Grafana Sample

## Local Environment Setup

### Requirements

- Rancher Desktop (https://rancherdesktop.io/)
- Tilt (https://tilt.dev/)

### Quick Start on Local Machine

Configure `_scm_config/values.local.yaml`

```bash
# register helm repo
helm repo list
helm repo add grafana https://grafana.github.io/helm-charts
# install dependencies
helm dep update ./charts
# start local k8s cluster
tilt up
# clean local k8s cluster
tilt down
```

### Notes

The default admin credentials are configurable on `charts/values.yaml`, however in case you cannot login you can change admin password with the following method: 

```bash
# get a pod name
kubectl get pod
# ssh to the pod
kubectl exec -it <pod_name> -- /bin/bash
# change grafana password
grafana-cli admin reset-admin-password admin
```