---
layout: layout.pug
navigationTitle: Bootstrap
title: Bootstrap
menuWeight: 15
excerpt: Prepare to deploy Kubernetes clusters
enterprise: false
---

To create Kubernetes clusters, Konvoy uses [Cluster API][capi_book] (CAPI) controllers. These controllers run on a Kubernetes cluster. To get started, you need a _bootstrap_ cluster. By default, Konvoy creates a bootstrap cluster for you in a Docker container using the Kubernetes-in-Docker ([KIND][kind]) tool.

## Prerequisites

Before you begin, you must:

- Complete the steps in [Prerequisites][prerequisites].
- Ensure the `dkp` binary can be found in your `$PATH`.

## Bootstrap Cluster Lifecycle Services

1.  If an HTTP proxy is required for the bootstrap cluster, set the local `http_proxy`, `https_proxy`, and `no_proxy` environment variables. They are copied into the bootstrap cluster.

1.  Create a bootstrap cluster:

    ```bash
    dkp create bootstrap --kubeconfig $HOME/.kube/config
    ```

    ```sh
    ✓ Creating a bootstrap cluster
    ✓ Initializing bootstrap controllers
    ```

    Konvoy creates a bootstrap cluster using [KIND][kind] as a library. Konvoy then deploys the following [Cluster API][capi_book] providers on the cluster:

    - [Core Provider][capi]
    - [AWS Infrastructure Provider][capa]
    - [Kubeadm Bootstrap Provider][cabpk]
    - [Kubeadm ControlPlane Provider][kcp]

    Konvoy waits until the controller-manager and webhook deployments of these providers are ready. List these deployments using this command:

    ```bash
    kubectl get --all-namespaces deployments -l=clusterctl.cluster.x-k8s.io
    ```

    ```sh
    NAMESPACE                           NAME                                            READY   UP-TO-DATE   AVAILABLE   AGE
    capa-system                         capa-controller-manager                         1/1     1            1           5m23s
    capi-kubeadm-bootstrap-system       capi-kubeadm-bootstrap-controller-manager       1/1     1            1           5m33s
    capi-kubeadm-control-plane-system   capi-kubeadm-control-plane-controller-manager   1/1     1            1           5m29s
    capi-system                         capi-controller-manager                         1/1     1            1           5m36s
    cappp-system                        cappp-controller-manager                        1/1     1            1           5m12s
    capz-system                         capz-controller-manager                         1/1     1            1           5m17s
    cert-manager                        cert-manager                                    1/1     1            1           5m56s
    cert-manager                        cert-manager-cainjector                         1/1     1            1           5m56s
    cert-manager                        cert-manager-webhook                            1/1     1            1           5m56s
    ```

    Konvoy then creates additional resources for Cluster API to apply to every new cluster. The resources, called `ClusterResourceSets`, contain complete YAML manifests to deploy essential cluster applications, such as the [Calico][calico] Container Networking Interface (CNI) implementation, and Container Storage Interface (CSI) implementations for various infrastructure APIs. List ClusterResourceSets using this command:

    ```bash
    kubectl get clusterresourceset
    ```

    ```sh
    NAME                                            AGE
    aws-ebs-csi                                     5m41s
    calico-installation-aws                         5m41s
    calico-installation-azure                       5m41s
    calico-installation-preprovisioned              5m41s
    calico-installation-preprovisioned-flatcar      5m41s
    cluster-autoscaler                              5m41s
    local-volume-provisioner                        5m41s
    node-feature-discovery                          5m41s
    nvidia-feature-discovery                        5m41s
    tigera-operator                                 5m41s
    ```

    A ClusterResourceSet object defines selectors that match against cluster labels, and a reference to a ConfigMap. The ConfigMap contains a YAML manifest. When a cluster with matching labels is created, the YAML manifest is applied to the cluster. The manifest is applied only once, when the cluster is created.

    For example, this is the `node-feature-discovery` ClusterResourceSet, which is now deployed by Konvoy from the above actions:

    ```yaml
    apiVersion: addons.cluster.x-k8s.io/v1alpha4
    kind: ClusterResourceSet
    metadata:
       name: node-feature-discovery
    spec:
      clusterSelector:
          matchExpressions:
          - key: konvoy.d2iq.io/provider
             operator: Exists
      resources:
      - kind: ConfigMap
         name: node-feature-discovery
      strategy: ApplyOnce

    ```

    Konvoy defines the selectors and sets the correct labels on the Cluster objects. For a more detailed explanation of how ClusterResourceSets work, see the [Extension Proposal][clusterresourceset_caep].

[install_docker]: https://docs.docker.com/get-docker/
[install_clusterawsadm]: https://github.com/kubernetes-sigs/cluster-api-provider-aws/releases
[install_kubectl]: https://kubernetes.io/docs/tasks/tools/install-kubectl/
[aws_credentials]: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html
[capa]: https://github.com/kubernetes-sigs/cluster-api-provider-aws
[kind]: https://github.com/kubernetes-sigs/kind
[capi_book]: https://cluster-api.sigs.k8s.io/
[calico]: https://docs.projectcalico.org/
[capi]: https://github.com/kubernetes-sigs/cluster-api/tree/v0.3.20/
[kcp]: https://github.com/kubernetes-sigs/cluster-api/tree/v0.3.20/controlplane/kubeadm
[cabpk]: https://github.com/kubernetes-sigs/cluster-api/tree/v0.3.20/bootstrap/kubeadm
[clusterresourceset_caep]: https://github.com/kubernetes-sigs/cluster-api/blob/master/docs/proposals/20200220-cluster-resource-set.md
[prerequisites]: ../prerequisites
