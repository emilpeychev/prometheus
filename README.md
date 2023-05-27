# Prometheus

Setup Prometheus in your Kubernetes Cluster

## Instructions

### NFS Volume

* Let's begin by provisioning an NFS default StoregeClass called `monitoring-tools` for the `monitoring-tools` Namespace.
* Run the `nfs-monitoring-tools-storage-class` helm installation.

### Create the Persistent Volume

* Create the persistent volume and add the flag `--wait=true` to ensure that the claim is made after the deployment is complete.

```
kubectl apply -f pvc-prometheus.yaml --wait=true
```

### Grant access to your Prometheus

* Run the access-prometheus.yaml to provide ClusterRoleBinding, ClusterRole and  ServiceAccount.

```
kubectl apply -f access-prometheus.yaml
```

### Run the Deployment

* Run the  `deployment-prometheus.yaml` to deploy Prometheus, the Service and ConfigMap.

```
kubectl apply -f deployment-prometheus.yaml

```
### Add the exporter `kube-state-metrics`

* Finally add the exporter and query the `NODE_IP:32002`

```
kubectl apply -f exporter-prometheus.yaml
```

* If all snapped in place your Prometheus is running on your worker-node_IP:32002
