---
layout: layout.pug
navigationTitle: Create the Cluster
title: Create the Cluster
menuWeight: 70
excerpt: Create a Kubernetes cluster using the infrastructure definition
beta: false
enterprise: false
---

With the inventory, and the control plane endpoint defined, use the `dkp` binary to create a Konvoy cluster. The following command relies on the pre-provisioned cluster API infrastructure provider to initialize the Kubernetes control plane and worker nodes on the hosts defined in the inventory.

<p class="message--note"><strong>NOTE: </strong>When specifying the <code>cluster-name</code>, you must use the same <code>cluster-name</code> as used when defining your inventory objects.</p>

```bash
dkp create cluster preprovisioned --cluster-name ${CLUSTER_NAME} --control-plane-endpoint-host <control plane endpoint host> --control-plane-endpoint-port <control plane endpoint port, if different than 6443>
```

```bash
Generating cluster resources
cluster.cluster.x-k8s.io/preprovisioned-example-rhel-84 created
kubeadmcontrolplane.controlplane.cluster.x-k8s.io/preprovisioned-example-rhel-84-control-plane created
preprovisionedcluster.infrastructure.cluster.konvoy.d2iq.io/preprovisioned-example-rhel-84 created
preprovisionedmachinetemplate.infrastructure.cluster.konvoy.d2iq.io/preprovisioned-example-rhel-84-control-plane created
secret/preprovisioned-example-rhel-84-etcd-encryption-config created
machinedeployment.cluster.x-k8s.io/preprovisioned-example-rhel-84-md-0 created
preprovisionedmachinetemplate.infrastructure.cluster.konvoy.d2iq.io/preprovisioned-example-rhel-84-md-0 created
kubeadmconfigtemplate.bootstrap.cluster.x-k8s.io/preprovisioned-example-rhel-84-md-0 created
clusterresourceset.addons.cluster.x-k8s.io/calico-cni-installation-preprovisioned-example-rhel-84 created
configmap/calico-cni-installation-preprovisioned-example-rhel-84 created
configmap/tigera-operator-preprovisioned-example-rhel-84 created
clusterresourceset.addons.cluster.x-k8s.io/local-volume-provisioner-preprovisioned-example-rhel-84 created
configmap/local-volume-provisioner-preprovisioned-example-rhel-84 created
clusterresourceset.addons.cluster.x-k8s.io/node-feature-discovery-preprovisioned-example-rhel-84 created
configmap/node-feature-discovery-preprovisioned-example-rhel-84 created
clusterresourceset.addons.cluster.x-k8s.io/nvidia-feature-discovery-preprovisioned-example-rhel-84 created
configmap/nvidia-feature-discovery-preprovisioned-example-rhel-84 created
```

<p class="message--note"><strong>NOTE: </strong>If you have <a href="../create-secrets-and-overrides">overrides for your clusters</a>, you must specify the secret as part of the create cluster command. If these are not specified, the overrides for your nodes will not be applied. </p>

```bash
dkp create cluster preprovisioned --cluster-name ${CLUSTER_NAME} --control-plane-endpoint-host <control plane endpoint host> --control-plane-endpoint-port <control plane endpoint port, if different than 6443> --override-secret-name=$CLUSTER_NAME-user-overrides
```

Depending on the cluster size, it will take a few minutes to be created. After the creation, use this command to get the Kubernetes kubeconfig for the new cluster and begin deploying workloads:

```bash
dkp get kubeconfig -c ${CLUSTER_NAME} > ${CLUSTER_NAME}.conf
```

### Verify your Calico installation

Before exploring the new cluster, confirm your `calico` installation is correct.
By default, Calico automatically detects the IP to use for each node using the `first-found` [method][calico-method]. This is not always appropriate for your particular nodes. In that case, you must modify Calico's configuration to use a different method.
An alternative is to use the `interface` method by providing the interface ID to use. Follow the steps outlined in this section to modify Calico's configuration. In this example, all cluster nodes use `ens192` as the interface name.

Get the pods running on your cluster with this command:

   ```bash
   kubectl get pods -A --kubeconfig ${CLUSTER_NAME}.conf
   ```

   ```bash
   NAMESPACE                NAME                                                                READY   STATUS            RESTARTS        AGE
   calico-system            calico-kube-controllers-57fbd7bd59-vpn8b                            1/1     Running           0               16m
   calico-system            calico-node-5tbvl                                                   1/1     Running           0               16m
   calico-system            calico-node-nbdwd                                                   1/1     Running           0               4m40s
   calico-system            calico-node-twl6b                                                   0/1     PodInitializing   0               9s
   calico-system            calico-node-wktkh                                                   1/1     Running           0               5m35s
   calico-system            calico-typha-54f46b998d-52pt2                                       1/1     Running           0               16m
   calico-system            calico-typha-54f46b998d-9tzb8                                       1/1     Running           0               4m31s
   default                  cuda-vectoradd                                                      0/1     Pending           0               0s
   kube-system              coredns-78fcd69978-frwx4                                            1/1     Running           0               16m
   kube-system              coredns-78fcd69978-kkf44                                            1/1     Running           0               16m
   kube-system              etcd-ip-10-0-121-16.us-west-2.compute.internal                      0/1     Running           0               8s
   kube-system              etcd-ip-10-0-46-17.us-west-2.compute.internal                       1/1     Running           1               16m
   kube-system              etcd-ip-10-0-88-238.us-west-2.compute.internal                      1/1     Running           1               5m35s
   kube-system              kube-apiserver-ip-10-0-121-16.us-west-2.compute.internal            0/1     Running           6               7s
   kube-system              kube-apiserver-ip-10-0-46-17.us-west-2.compute.internal             1/1     Running           1               16m
   kube-system              kube-apiserver-ip-10-0-88-238.us-west-2.compute.internal            1/1     Running           1               5m34s
   kube-system              kube-controller-manager-ip-10-0-121-16.us-west-2.compute.internal   0/1     Running           0               7s
   kube-system              kube-controller-manager-ip-10-0-46-17.us-west-2.compute.internal    1/1     Running           1 (5m25s ago)   15m
   kube-system              kube-controller-manager-ip-10-0-88-238.us-west-2.compute.internal   1/1     Running           0               5m34s
   kube-system              kube-proxy-gclmt                                                    1/1     Running           0               16m
   kube-system              kube-proxy-gptd4                                                    1/1     Running           0               9s
   kube-system              kube-proxy-mwkgl                                                    1/1     Running           0               4m40s
   kube-system              kube-proxy-zcqxd                                                    1/1     Running           0               5m35s
   kube-system              kube-scheduler-ip-10-0-121-16.us-west-2.compute.internal            0/1     Running           1               7s
   kube-system              kube-scheduler-ip-10-0-46-17.us-west-2.compute.internal             1/1     Running           3 (5m25s ago)   16m
   kube-system              kube-scheduler-ip-10-0-88-238.us-west-2.compute.internal            1/1     Running           1               5m34s
   kube-system              local-volume-provisioner-2mv7z                                      1/1     Running           0               4m10s
   kube-system              local-volume-provisioner-vdcrg                                      1/1     Running           0               4m53s
   kube-system              local-volume-provisioner-wsjrt                                      1/1     Running           0               16m
   node-feature-discovery   node-feature-discovery-master-84c67dcbb6-m78vr                      1/1     Running           0               16m
   node-feature-discovery   node-feature-discovery-worker-vpvpl                                 1/1     Running           0               4m10s
   tigera-operator          tigera-operator-d499f5c8f-79dc4                                     1/1     Running           1 (5m24s ago)   16m
   ```

<p class="message--note"><strong>NOTE: </strong>If a <code>calico-node</code> pod is not ready on your cluster, you must edit the <code>installation</code> file.
</p>

To edit the installation file, run the command:

   ```bash
   kubectl edit installation default --kubeconfig ${CLUSTER_NAME}.conf
   ```

Change the value for `spec.calicoNetwork.nodeAddressAutodetectionV4` to `interface: ens192`, and save the file:

   ```yaml
   spec:
     calicoNetwork:
     ...
       nodeAddressAutodetectionV4:
         interface: ens192
   ```

Save this file. You may need to delete the node feature discovery worker pod in the `node-feature-discovery` namespace if that pod has failed. After you delete it, Kubernetes replaces the pod as part of its normal reconciliation.

## Use the built-in Virtual IP

As explained in [Define the Control Plane Endpoint][define-control-plane-endpoint], we recommend using an external load balancer for the control plane endpoint, but provide a built-in virtual IP when an external load balancer is not available. The built-in virtual IP uses the [kube-vip][kube-vip] project.
To use the virtual IP, add these flags to the `create cluster` command:


| Virtual IP Configuration                 | Flag                                 |
| ---------------------------------------- | ------------------------------------ |
| Network interface to use for Virtual IP. _Must exist on all control plane machines._ | `--virtual-ip-interface string`             |
| IPv4 address. _Reserved for use by the cluster._ | `--control-plane-endpoint string` |

### Virtual IP Example

```bash
dkp create cluster preprovisioned \
    --cluster-name ${CLUSTER_NAME} \
    --control-plane-endpoint-host 196.168.1.10 \
    --virtual-ip-interface eth1
```

Confirm that your [Calico installation is correct][calico-install].

## Provision on the Flatcar Linux OS

When provisioning onto the Flatcar Container Linux distribution, you must instruct the bootstrap cluster to make some changes related to the installation paths. To accomplish this, add the `--os-hint flatcar` flag to the above `create cluster` command.

### Flatcar Linux Example

```bash
dkp create cluster preprovisioned \
    --cluster-name ${CLUSTER_NAME} \
    --os-hint flatcar
```

Confirm that your [Calico installation is correct][calico-install].

## Use an HTTP Proxy

If you require HTTP proxy configurations, you can apply them during the `create` operation by adding the appropriate flags to the `create cluster` command:

| Proxy configuration                      | Flag                                 |
| ---------------------------------------- | ------------------------------------ |
| HTTP proxy for control plane machines    | `--control-plane-http-proxy string`  |
| HTTPS proxy for control plane machines   | `--control-plane-https-proxy string` |
| No Proxy list for control plane machines | `--control-plane-no-proxy strings`   |
| HTTP proxy for worker machines           | `--worker-http-proxy string`         |
| HTTPS proxy for worker machines          | `--worker-https-proxy string`        |
| No Proxy list for worker machines        | `--worker-no-proxy strings`          |

### HTTP Proxy Example

```bash
dkp create cluster preprovisioned \
    --cluster-name ${CLUSTER_NAME} \
    --control-plane-http-proxy http://proxy.example.com:8080 \
    --control-plane-https-proxy https://proxy.example.com:8080 \
    --control-plane-no-proxy "127.0.0.1,10.96.0.0/12,192.168.0.0/16,kubernetes,kubernetes.default.svc,kubernetes.default.svc.cluster,kubernetes.default.svc.cluster.local,.svc,.svc.cluster,.svc.cluster.local" \
    --worker-http-proxy http://proxy.example.com:8080 \
    --worker-https-proxy https://proxy.example.com:8080 \
    --worker-no-proxy "127.0.0.1,10.96.0.0/12,192.168.0.0/16,kubernetes,kubernetes.default.svc,kubernetes.default.svc.cluster,kubernetes.default.svc.cluster.local,.svc,.svc.cluster,.svc.cluster.local"
```

Confirm that your [Calico installation is correct][calico-install].

## Use an alternative mirror

To apply Docker registry configurations during the create operation, add the appropriate flags to the `create cluster` command:

| Docker registry configuration                                | Flag                            |
| ------------------------------------------------------------ | ------------------------------- |
| CA certificate chain to use while communicating with the registry mirror using TLS | `--registry-mirror-cacert file` |
| URL of a container registry to use as a mirror in the cluster | `--registry-mirror-url string`  |

This is useful when using an internal registry and when Internet access is not available (air-gapped installations).

When the cluster is up and running, you can deploy and test workloads.

### Alternative Mirror Example

```bash
dkp create cluster preprovisioned \
    --cluster-name ${CLUSTER_NAME} \
    --registry-mirror-cacert /tmp/registry.pem \
    --registry-mirror-url https://registry.example.com
```

Confirm that your [Calico installation is correct][calico-install].

## Use alternate pod or service subnets

In Konvoy, the default pod subnet is 192.168.0.0/16, and the default service subnet is 10.96.0.0/12. If you wish to change the subnets you can do so with the following steps:

1.  Generate the yaml manifests for the cluster using the `--dry-run` and `-o yaml` flags, along with the desired `dkp cluster create` command:

    ```bash
    dkp create cluster preprovisioned --cluster-name ${CLUSTER_NAME} --control-plane-endpoint-host <control plane endpoint host> --control-plane-endpoint-port <control plane endpoint port, if different than 6443> --dry-run -o yaml > cluster.yaml
    ```

1.  To modify the service subnet, add or edit the `spec.clusterNetwork.services.cidrBlocks` field of the `Cluster` object:

    ```yaml
    kind: Cluster
    spec:
      clusterNetwork:
        services:
          cidrBlocks:
          - 10.0.0.0/18
    ```

1.  To modify the pod subnet, edit the `Cluster` and calico-cni `ConfigMap` resources:

    Cluster: Add or edit the`spec.clusterNetwork.pods.cidrBlocks` field:

    ```yaml
    kind: Cluster
    spec:
      clusterNetwork:
        pods:
          cidrBlocks:
          - 172.16.0.0/16
    ```

    ConfigMap: Edit the `data."custom-resources.yaml".spec.calicoNetwork.ipPools.cidr` field with your desired pod subnet:

    ```yaml
    apiVersion: v1
    data:
      custom-resources.yaml: |
        apiVersion: operator.tigera.io/v1
        kind: Installation
        metadata:
          name: default
        spec:
          # Configures Calico networking.
          calicoNetwork:
            # Note: The ipPools section cannot be modified post-install.
            ipPools:
            - blockSize: 26
              cidr: 172.16.0.0/16
    kind: ConfigMap
    metadata:
      name: calico-cni-<cluter-name>
    ```

When you provision the cluster, the configured pod and service subnets will be applied.

Confirm that your [Calico installation is correct][calico-install].

[calico-install]: #verify-your-calico-installation
[calico-method]: https://projectcalico.docs.tigera.io/reference/node/configuration#ip-autodetection-methods
[create-secrets-and-overrides]: ../create-secrets-and-overrides
[define-control-plane-endpoint]: ../define-control-plane-endpoint
[kube-vip]: https://kube-vip.chipzoller.dev