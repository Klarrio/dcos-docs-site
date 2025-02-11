---
layout: layout.pug
navigationTitle: API documentation (v1beta2)
title: API documentation (v1beta2)
menuWeight: 10
notes: Automatically generated, DO NOT EDIT
enterprise: false
excerpt: API documentation (v1beta2)
---

# API Documentation (v1beta2)

> This document is automatically generated from the API definition in the code.

## Table of Contents
* [VSphereDatacenters](#vspheredatacenters)
* [VSphereMachineOpts](#vspheremachineopts)
* [VSphereMachineOptsNetwork](#vspheremachineoptsnetwork)
* [VSphereMachineOptsNetworkGlobal](#vspheremachineoptsnetworkglobal)
* [VSphereMachineOptsNetworkMachine](#vspheremachineoptsnetworkmachine)
* [VSphereProviderOptions](#vsphereprovideroptions)
* [AutoscalingOptions](#autoscalingoptions)
* [ClusterProvisioner](#clusterprovisioner)
* [ClusterProvisionerSpec](#clusterprovisionerspec)
* [DockerProviderOptions](#dockerprovideroptions)
* [Machine](#machine)
* [MachinePool](#machinepool)
* [SSHCredentials](#sshcredentials)
* [ForwardingRule](#forwardingrule)
* [GCPMachineOpts](#gcpmachineopts)
* [GCPProviderOptions](#gcpprovideroptions)
* [IAMSA](#iamsa)
* [Network](#network)
* [ServiceAccount](#serviceaccount)
* [AvailabilitySet](#availabilityset)
* [AzureMachineOpts](#azuremachineopts)
* [AzureProviderOptions](#azureprovideroptions)
* [LoadBalancer](#loadbalancer)
* [VNET](#vnet)
* [AWSMachineOpts](#awsmachineopts)
* [AWSProviderOptions](#awsprovideroptions)
* [ELB](#elb)
* [IAM](#iam)
* [InstanceProfile](#instanceprofile)
* [SpotBlockOptions](#spotblockoptions)
* [VPC](#vpc)
* [Inventory](#inventory)
* [InventoryHost](#inventoryhost)
* [InventoryNodePool](#inventorynodepool)
* [APIServer](#apiserver)
* [AddonConfig](#addonconfig)
* [AddonRepository](#addonrepository)
* [Addons](#addons)
* [AdmissionPlugins](#admissionplugins)
* [AutoProvisioning](#autoprovisioning)
* [CalicoContainerNetworking](#calicocontainernetworking)
* [Certificate](#certificate)
* [CloudProvider](#cloudprovider)
* [ClusterConfiguration](#clusterconfiguration)
* [ClusterConfigurationSpec](#clusterconfigurationspec)
* [ConfigData](#configdata)
* [ContainerNetworking](#containernetworking)
* [ContainerRuntime](#containerruntime)
* [ContainerdContainerRuntime](#containerdcontainerruntime)
* [ControlPlane](#controlplane)
* [Etcd](#etcd)
* [GPU](#gpu)
* [IPTables](#iptables)
* [ImageRegistry](#imageregistry)
* [Keepalived](#keepalived)
* [Kubelet](#kubelet)
* [Kubernetes](#kubernetes)
* [LoggingOptions](#loggingoptions)
* [Networking](#networking)
* [NodeLabel](#nodelabel)
* [NodePool](#nodepool)
* [NodeTaint](#nodetaint)
* [OSPackages](#ospackages)
* [OperatingSystem](#operatingsystem)
* [PreflightChecks](#preflightchecks)

## VSphereDatacenters

VSphereDatacenters is vSphere datacenters definition values.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | Define the Name of the datacenter to be used. | string | true |
| datastore | Define the Datastore to be used. | string | true |
| cluster | Define the Cluster to be used. | string | true |
| network | Define the Network to be used. | string | true |
| vmFolder | Define the VM Folder to be used. | string | false |

[Back to TOC](#table-of-contents)

## VSphereMachineOpts

VSphereMachineOpts is vSphere specific options for machine.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| network | Networking describes static network configuration if needed | [VSphereMachineOptsNetwork](#vspheremachineoptsnetwork) | false |

[Back to TOC](#table-of-contents)

## VSphereMachineOptsNetwork

VSphereMachineOptsNetwork is vSphere specific network options for machine.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| global | Global describes static network configuration of global settings like nameserver and gateway | [VSphereMachineOptsNetworkGlobal](#vspheremachineoptsnetworkglobal) | false |
| machines | Machines describes static network configuration for the machines like ip address with subnet and MAC address | [][VSphereMachineOptsNetworkMachine](#vspheremachineoptsnetworkmachine) | false |

[Back to TOC](#table-of-contents)

## VSphereMachineOptsNetworkGlobal

VSphereMachineOptsNetworkGlobal is vSphere specific options for machines global network settings

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| searchDomains | Define the search domains as list | []string | false |
| nameservers | Define the machines nameservers as list | []string | false |
| vlan | Define the machines VLAN to be used | int16 | false |
| ipv4Gateway | Define the machines IPv4 gateway to be used for internet access | string | false |

[Back to TOC](#table-of-contents)

## VSphereMachineOptsNetworkMachine

VSphereMachineOptsNetworkMachine is vSphere specific options for machines global network settings

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| ipv4Address | Define the machines IPv4 address to be used in CIDR notation like 192.168.0.1/24 (24 -> 255.255.255.0) | string | false |
| macAddress | Define the machines MAC address to be set, instead of getting an automatically assinged one | string | false |

[Back to TOC](#table-of-contents)

## VSphereProviderOptions

VSphereProviderOptions describes vSphere provider specific options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| server | Define the vSphere Server endpoint | string | true |
| port | Define the Datacenter where you cluster is hosted. (default: `443`) | int64 | false |
| datacenters | Define the Datacenters where you cluster is hosted. | [][VSphereDatacenters](#vspheredatacenters) | true |
| username | Define the vSphere Username for the cloud-provider to be used. | string | true |
| password | Define the vSphere Password for the cloud-provider to be used. | string | true |

[Back to TOC](#table-of-contents)

## AutoscalingOptions

AutoscalingOptions configures autoscaling features for a node pool.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| minSize | Specifies the minimum number of machines to keep in a pool by the autoscaler. (default: `1`) | int32 | false |
| maxSize | Specifies the maximum number of machines to be provisioned by the autoscaler. (default: `10`) | int32 | false |

[Back to TOC](#table-of-contents)

## ClusterProvisioner

ClusterProvisioner describes provisioner options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| metadata |  | [metav1.ObjectMeta](https://v1-17.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#objectmeta-v1-meta) | true |
| spec |  | [ClusterProvisionerSpec](#clusterprovisionerspec) | false |

[Back to TOC](#table-of-contents)

## ClusterProvisionerSpec

ClusterProvisionerSpec is the spec that contains the provisioner options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| provider | The provider used to provision the cluster. One can choose one of the following: `aws`, `azure`, `gcp`, `vsphere`, `docker`. (default: `aws`) | string | true |
| aws | AWS provisioner specific options. | [AWSProviderOptions](#awsprovideroptions) | false |
| azure | Azure provisioner specific options. | [AzureProviderOptions](#azureprovideroptions) | false |
| gcp | GCP provisioner specific options. | [GCPProviderOptions](#gcpprovideroptions) | false |
| vsphere | vSphere provisioner specific options. | [VSphereProviderOptions](#vsphereprovideroptions) | false |
| docker | Docker provisioner specific options. | [DockerProviderOptions](#dockerprovideroptions) | false |
| nodePools | A list of node pools to create. There must exist at least one control plane node pool. | [][MachinePool](#machinepool) | false |
| sshCredentials | Contains SSH credentials information for accessing machines in a cluster. | [SSHCredentials](#sshcredentials) | false |
| version | Version of a Konvoy cluster. | string | false |

[Back to TOC](#table-of-contents)

## DockerProviderOptions

DockerProviderOptions describes Docker provider related options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| disablePortMapping | Disable mapping container ports to host ports. Port mapping is only needed on OSX where direct container access is not possible. (default: `false`) | bool | false |
| controlPlaneMappedPortBase | If port mapping is enabled, this specifies the host port number base for the API endpoints on control plane nodes. (default: `46000`) | int32 | false |
| sshControlPlaneMappedPortBase | If port mapping is enabled, this specifies the host port number base for the SSH service on control plane nodes. (default: `22000`) | int32 | false |
| sshWorkerMappedPortBase | If port mapping is enabled, this specifies the host port number base for the SSH service on worker nodes. (default: `22010`) | int32 | false |
| dedicatedNetwork | Specifies if a dedicated docker network would be created for the cluster. (default: `false`) | bool | false |

[Back to TOC](#table-of-contents)

## Machine

Machine specifies details about a machine in a node pool.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| imageID | The image ID that will be used for the instances instead of the default image. Depending on the provisioner, the meaning is different. `aws`: [AMI ID](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html). `azure`: [VM Image URN](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/cli-ps-findimage). `gcp`: [VM Image URI](https://cloud.google.com/sdk/gcloud/reference/compute/images/list). `docker`: N/A. | string | false |
| imageName | The image name (e.g., Docker image name) that is used instead of the default image. Depending on the provisioner, the meaning is different. `aws`: N/A. `azure`: N/A. `gcp`: N/A. `docker`: Docker image name. | string | false |
| rootVolumeSize | The root volume size in GiBs. (default: 80) | int64 | false |
| rootVolumeType | The root volume type. Depending on the provisioner, the meaning is different. `aws`: [EBS volume type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html) (default: `gp2`). `azure`: [Disk storage account type](https://docs.microsoft.com/en-us/rest/api/compute/disks/createorupdate#diskstorageaccounttypes) (default: `StandardSSD_LRS`). `gcp`: [Disk type](https://cloud.google.com/sdk/gcloud/reference/compute/disk-types) (default: `pd-ssd`). `docker`: N/A. | string | false |
| rootVolumeIOPS | The root volume IOPS. Depending on the provisioner, the meaning is different. `aws`: [EBS volume IOPS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html) (default: `1000` for control plane nodes). `azure`: N/A. `gcp`: N/A. `docker`: N/A. | int32 | false |
| imagefsVolumeEnabled | Whether to enable dedicated disk for image filesystem (for example, `/var/lib/containerd`). (default: `true`) | bool | false |
| imagefsVolumeSize | The size of imagefs volume in GiBs. (default: `160`) | int64 | false |
| imagefsVolumeType | The volume type for the imagefs volume. Depending on the provisioner, the meaning is different. `aws`: [EBS volume type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html) (default: `gp2`). `azure`: [Disk storage account type](https://docs.microsoft.com/en-us/rest/api/compute/disks/createorupdate#diskstorageaccounttypes) (default: `Standard_LRS`). `gcp`: [Disk type](https://cloud.google.com/sdk/gcloud/reference/compute/disk-types) (default: `pd-ssd`). `docker`: N/A. | string | false |
| imagefsVolumeDevice | The device name of the imagefs volume. Depending on the provisioner, the meaning is different. `aws`: [Device name](https://docs.aws.amazon.com/cli/latest/reference/ec2/attach-volume.html) (default: `xvdb`). `azure`: N/A. `gcp`: N/A. `docker`: N/A. | string | false |
| type | The machine type. Depending on the provisioner, the meaning is different. `aws`: [EC2 instance type](https://aws.amazon.com/ec2/instance-types/) (default: `m5.xlarge` for control plane, `m5.2xlarge` for workers). `azure`: [VM type](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sizes) (default: `Standard_D4s_v3` for control plane, `Standard_D8s_v3` for workers). `gcp`: [Machine type](https://cloud.google.com/compute/docs/machine-types) (default: `n1-standard-4` for control plane, `n1-standard-8` for workers). `docker`: N/A. | string | false |
| aws | AWS provisioner specific configurations. | [AWSMachineOpts](#awsmachineopts) | false |
| azure | Azure provisioner specific configurations. | [AzureMachineOpts](#azuremachineopts) | false |
| gcp | GCP provisioner specific configurations. | [GCPMachineOpts](#gcpmachineopts) | false |
| vsphere | vSphere provisioner specific configurations. | [VSphereMachineOpts](#vspheremachineopts) | false |

[Back to TOC](#table-of-contents)

## MachinePool

MachinePool describes a node pool that will be provisioned by the provisioner.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | The unique name that defines a node pool. | string | true |
| indexType | Determines how to index a node pool. It can be one of the following. `named`:\n   The node pool is referenced using its name.\n   This means one can update or delete the node pool without affecting other node pools.\n`positional` (DEPRECATED):\n   The node pool is referenced using its position in the node pool list.\n   This means deleting the node pool would affect subsequent positional node pools in the node pool list.\n   This type has been DEPRECATED in favor of `named` node pools.\n(default: `named`) | string | false |
| controlPlane | Determines if a node pool contains Kubernetes Master nodes (control plane). Only one such node pool can exist. (default: `false`) | bool | false |
| bastion | Determines if a node pool contains bastion hosts. Only one such node pool can exist. (default: `false`) | bool | false |
| count | The number of nodes in a node pool. You should set the `count` to an odd number `controlPlane` is set to `true` to help keep `etcd` store consistent. A node pool count of 3 is considered \"highly available\" (HA) to protect against failures. (default: `4` for worker pool, `3` for control plane pool) | int32 | true |
| machine | Details about the machines in the node pool. | [Machine](#machine) | false |
| autoscaling | Autoscaling configurations for the node pool. | [AutoscalingOptions](#autoscalingoptions) | false |

[Back to TOC](#table-of-contents)

## SSHCredentials

SSHCredentials describes the options passed to the provisioner regarding the ssh keys.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| user | The user name to use when accessing a machine through ssh. (default: `centos`) | string | true |
| publicKeyFile | The path and name of the public key file to use when accessing a machine through ssh. (default: `<clustername>-ssh.pub`) | string | true |
| privateKeyFile | The path and name of the private key file to use when accessing a machine through ssh. If not set, Konvoy will assume the key presents in ssh-agent. (default: `<clustername>-ssh.pem`) | string | false |

[Back to TOC](#table-of-contents)

## ForwardingRule

ForwardingRule contains details for the kube-apiserver ForwardingRule / LoadBalancer.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| internal | Set to `true` to make the ForwardingRule / LoadBalancer internal. (default: `false`) | bool | false |

[Back to TOC](#table-of-contents)

## GCPMachineOpts

GCPMachineOpts is gcp specific options for machine.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| iam | IAM represents access control details. | [IAMSA](#iamsa) | false |
| subnetIDs | [GCP Subnets](https://cloud.google.com/vpc/docs/vpc) to launch the instances into. | []string | false |
| associatePublicIPAddress | Whether to associate an [external IP](https://cloud.google.com/compute/docs/ip-addresses#externaladdresses) with each instance in the node pool. GCP will effectively create a `ONE_TO_ONE_NAT` NAT IP for each instance. (default: `true`) | bool | false |

[Back to TOC](#table-of-contents)

## GCPProviderOptions

GCPProviderOptions describes GCP provider specific options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| region | [GCP region](https://cloud.google.com/compute/docs/regions-zones) where you cluster is hosted. (default: `us-west1`) | string | false |
| network | [GCP VPC Network](https://cloud.google.com/vpc/docs/vpc) specific options for the cluster. | [Network](#network) | false |
| zones | [GCP zones](https://cloud.google.com/compute/docs/regions-zones) to deploy a cluster in a region. (default: `[\"us-west1-a\", \"us-west1-b\", \"us-west1-c\"]`) | []string | false |
| forwardingRule | [GCP forwarding rule](https://cloud.google.com/load-balancing/docs/forwarding-rule-concepts) for the kube-apiservers. | [ForwardingRule](#forwardingrule) | false |
| tags | Additional [tags](https://cloud.google.com/blog/products/gcp/labelling-and-grouping-your-google-cloud-platform-resources) for the resources provisioned through the Konvoy CLI. | []string | false |
| labels | Additional [labels](https://cloud.google.com/blog/products/gcp/labelling-and-grouping-your-google-cloud-platform-resources) for the resources provisioned through the Konvoy CLI. (default: `{owner: <username>}`) | map[string]string | false |

[Back to TOC](#table-of-contents)

## IAMSA

IAMSA contains ServiceAccount and policy information to use instead of creating one.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| serviceAccount | [GCP service account](https://cloud.google.com/iam/docs/service-accounts) and policies to use. If not set, Konvoy will automatically create the service account and policies. | [ServiceAccount](#serviceaccount) | false |

[Back to TOC](#table-of-contents)

## Network

Network contains the network information required if using an existing network.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| selfLink | The self link reference to the VPC network where the cluster should be launched. If not set, Konvoy will provision a new VPC network. | string | false |
| routerSelfLink | The self link reference to the router to be used by Konvoy. If not set, Konvoy will provision a new router in the VPC network. | string | false |
| natSelfLink | The self link reference to the NAT router to be used by Konvoy. If not set, Konvoy will provision a new NAT router in the VPC network. | string | false |
| createInternetGatewayRoute | Whether to create a default route to the Internet Gateway in the VPC network. This option is ignored if using a pre-existing VPC network. (default: `true`) | bool | false |

[Back to TOC](#table-of-contents)

## ServiceAccount

ServiceAccount describes GCP service account and policy information.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | The name of the service account. | string | false |
| role | The role name to use to bind to the service account. | string | false |

[Back to TOC](#table-of-contents)

## AvailabilitySet

AvailabilitySet contains the availability_set information.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| faultDomainCount | The amount of VMs with common storage as well as a common power source and network switch. (default: `3`) | int32 | false |
| updateDomainCount | The amount of VMs and underlying physical hardware that can be rebooted at the same time. (default: `3`) | int32 | false |

[Back to TOC](#table-of-contents)

## AzureMachineOpts

AzureMachineOpts is azure specific options for machine.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| subnetIDs | [Azure Subnets](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview) to launch the VMs into. | []string | false |

[Back to TOC](#table-of-contents)

## AzureProviderOptions

AzureProviderOptions describes azure provider specific options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| location | [Azure location](https://azure.microsoft.com/en-us/global-infrastructure/locations/) where your cluster will be hosted. (default: `eastus2`) | string | false |
| vnet | [Azure VNET](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview) specific options for the cluster. | [VNET](#vnet) | false |
| availabilitySet | [Azure availability sets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability) defines grouping capability for isolating VMs from each other. | [AvailabilitySet](#availabilityset) | false |
| loadbalancer | [Azure LoadBalancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview) configurations for the kube-apiservers. | [LoadBalancer](#loadbalancer) | false |
| tags | Additional [Azure tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources) for the resources provisioned through the Konvoy CLI. (default: `{owner: <username>}`) | map[string]string | false |

[Back to TOC](#table-of-contents)

## LoadBalancer

LoadBalancer contains details for the kube-apiserver LoadBalancer.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| internal | Set to `true` to make the LoadBalancer internal. (default: `false`) | bool | false |
| apiServerPort | Port on which Kubernetes apiserver is accessible. (default: `6443`) | int32 | false |

[Back to TOC](#table-of-contents)

## VNET

VNET contains the virtual network information required if using an existing virtual network

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | Name of the virtual network where the cluster should be launched. If not set, Konvoy will provision a new virtual network. | string | false |
| cidr | The CIDR block to use for the virtual network address space. If using an existing virtual network, set it to its CIDR block. (default: `10.0.0.0/16`) | string | false |
| resourceGroup | The name of the Resource group to be used by Konvoy. | string | false |
| routeTable | The name of the route table to be used by Konvoy. Konvoy will add routes to this route table. | string | false |

[Back to TOC](#table-of-contents)

## AWSMachineOpts

AWSMachineOpts is aws specific options for a machine in a node pool.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| kmsKeyID | The ID of the KMS key used for encryption at rest. [EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) (default: no volume encryption). | string | false |
| iam | [AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) represents access control details. | [IAM](#iam) | false |
| subnetIDs | [AWS Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) to launch the instances into. | []string | false |
| associatePublicIPAddress | Whether to associate a [public IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html) with each instance in the node pool. (default: `true`) | bool | false |
| spotBlockOpts | Options to make the machine pool backed by spot instances | [SpotBlockOptions](#spotblockoptions) | false |

[Back to TOC](#table-of-contents)

## AWSProviderOptions

AWSProviderOptions describes AWS provider specific options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| region | [AWS region](https://docs.aws.amazon.com/general/latest/gr/rande.html) where your cluster is hosted. (default: `us-west-2`) | string | false |
| vpc | [AWS VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) specific options for the cluster. | [VPC](#vpc) | false |
| availabilityZones | Availability zones to deploy a cluster in a region. (default: `[\"us-west-2c\"]`) | []string | false |
| elb | [AWS ELB](https://aws.amazon.com/elasticloadbalancing/) configurations for the kube-apiservers. | [ELB](#elb) | false |
| tags | Additional [tags](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html) for the resources provisioned through the Konvoy CLI. (default: `{owner: <username>}`) | map[string]string | false |
| skipMetadataAPICheck | Terraform -> Skip the AWS Metadata API check. Useful for AWS API implementations that do not have a metadata API endpoint. Setting to true prevents Terraform from authenticating via the Metadata API. (default: `false`) | bool | false |

[Back to TOC](#table-of-contents)

## ELB

ELB contains details for the kube-apiserver ELB.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| internal | Set to `true` to make the ELB internal. (default: `false`) | bool | false |
| subnetIDs | [AWS Subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) IDs where ELBs will be launched on. | []string | false |
| apiServerPort | Port on which Kubernetes apiserver is accessible. (default: `6443`) | int32 | false |

[Back to TOC](#table-of-contents)

## IAM

IAM contains role information to use instead of creating one.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| instanceProfile | The instance profile for the nodes in a node pool. If not set, Konvoy will automatically create roles and policies. | [InstanceProfile](#instanceprofile) | false |

[Back to TOC](#table-of-contents)

## InstanceProfile

InstanceProfile describes the role to use for instances.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| arn | ARN of the role with policies required to run a Kubernetes cluster. | string | false |
| name | Name of the role with policies required to run a Kubernetes cluster. | string | false |

[Back to TOC](#table-of-contents)

## SpotBlockOptions

SpotBlockOptions to configure spot options

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| spotDuration | Minutes the spot block will last for (default: `0`) | int32 | false |
| allowUnfulfilled | Allows spot workers to be unfulfilled if all requests aren't filled by a node (default: `false`) | bool | false |
| spotPrice | The maximum price to request on the spot market | string | false |
| creationTimeout | Creation Timeout | string | false |

[Back to TOC](#table-of-contents)

## VPC

VPC contains the VPC specific options for the cluster.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| ID | The ID of the [AWS VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) where the cluster should be launched. If not set, Konvoy will provision a new VPC. | string | false |
| cidr | The CIDR block to use for the [AWS VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html). If using an existing VPC, set it to the CIDR block for that VPC. (default: `10.0.0.0/16`) | string | false |
| routeTableID | The ID of the [AWS RouteTable](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) to be used by Konvoy. Konvoy will add routes to this route table if `EnableInternetGateway` is set. If a custom VPC is used and `OverrideDefaultRouteTable` is set, this field needs to be set to the ID of the default route table of the VPC. This field should not be set when a new VPC will be created. | string | false |
| overrideDefaultRouteTable | Whether to override default route table in the VPC. If set, Konvoy will take over the default route table, and delete all existing routes in the default route table. (default: `true`) | bool | false |
| internetGatewayID | The ID of the [AWS Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) to use for the cluster. This field must not be set if `EnableInternetGateway` is set. Konvoy will add a route to the IGW specified if specified. | string | false |
| enableInternetGateway | Whether to create an [AWS Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) in a VPC. (default: `true`) | bool | false |
| enableVPCEndpoints | Whether to create [AWS VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in a VPC. Creating this allows Kubernetes cloud provider and AWS CSI drivers to talk to the AWS services without IGW. (default: `false`) | bool | false |

[Back to TOC](#table-of-contents)

## Inventory

Inventory holds the inventory properties.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| control-plane | Describes configurations for the control plane node pool. | [InventoryNodePool](#inventorynodepool) | true |
| node | Describes configurations for the worker node pool. | [InventoryNodePool](#inventorynodepool) | true |
| bastion | Describes configurations for the bastion host node pool. | [InventoryNodePool](#inventorynodepool) | true |
| all | Describes configurations for all nodes. | [InventoryNodePool](#inventorynodepool) | true |

[Back to TOC](#table-of-contents)

## InventoryHost

InventoryHost holds the inventory host properties.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| ansible_host | The Ansible host. | string | true |
| ansible_port | The Ansible port. | string | true |
| node_pool | The name of the node pool. | string | true |

[Back to TOC](#table-of-contents)

## InventoryNodePool

InventoryNodePool holds the inventory nodePool properties.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| hosts | Map of hosts using IP as the key. | map[string][InventoryHost](#inventoryhost) | false |
| vars | Ansible variables. | InventoryVars | false |

[Back to TOC](#table-of-contents)

## APIServer

APIServer describes the settings for the api-server.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| targetRamMB | Specifies the `--target-ram-mb` flag for the apiserver. | string | false |

[Back to TOC](#table-of-contents)

## AddonConfig

AddonConfig is a quick reference to an Addon.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | The name of the addon. | string | true |
| enabled | Enables the addon to be deployed. | bool | true |
| values | Overrides the values found in default addon configuration file. Maps are merged while values and arrays are replaced. | string | false |

[Back to TOC](#table-of-contents)

## AddonRepository

AddonRepository describes in-cluster helm and kudo configuration used during air-gapped installation.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| image | The image of the addon chart and package repository to deploy in the cluster used during air-gapped installations. | string | false |

[Back to TOC](#table-of-contents)

## Addons

Addons describes an addon repository to use for the cluster.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| configRepository | The git repository of the addon repository to use. (default: `https://github.com/mesosphere/kubernetes-base-addons`) | string | false |
| configVersion | The version of the addon configuration files to use. (default: `master`) | string | false |
| addonRepository | In-cluster package configuration used during air-gapped installations. | [AddonRepository](#addonrepository) | false |
| addonsList | List of addon objects that can be deployed, if enabled. | AddonConfigs | false |

[Back to TOC](#table-of-contents)

## AdmissionPlugins

AdmissionPlugins configures Kubernetes admission plugins.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| enabled | List of admission plugins to enable. (default: `[\"AlwaysPullImages\", \"NodeRestriction\"]`) | []string | false |
| disabled | List of admission plugins to disable. | []string | false |

[Back to TOC](#table-of-contents)

## AutoProvisioning

AutoProvisioning contains configurations for the auto provisioner.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| config | [Helm value overrides](https://helm.sh/docs/chart_template_guide/values_files/) for the auto-provisioning helm chart. You can specify arbitrary YAML/JSON object for this field. The specified value overrides will need to conform to the schema defined for the chart. | apiext.JSON | false |
| disabled | Disabled skips the installation of the auto-provisioning components, the default is false. | bool | false |

[Back to TOC](#table-of-contents)

## CalicoContainerNetworking

CalicoContainerNetworking describes Calico CNI

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| version | The version of the [Calico](https://www.projectcalico.org/) CNI plugin. | string | false |
| encapsulation | The encapsulation mode. The supported modes are: [ipip](https://docs.projectcalico.org/getting-started/kubernetes/installation/config-options#configuring-ip-in-ip). [vxlan](https://docs.projectcalico.org/getting-started/kubernetes/installation/config-options#switching-from-ip-in-ip-to-vxlan). (default: `ipip`) [none](no encapsulation) | string | false |
| mtu | The MTU to use for the veth interfaces. (default: depends on `encapsulation` and provisioner) | int32 | false |

[Back to TOC](#table-of-contents)

## Certificate

Certificate contains information about an X.509 certificate.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| subjectAlternativeNames | List of Subject Alternative Names (SAN) for the control plane endpoint. | []string | false |

[Back to TOC](#table-of-contents)

## CloudProvider

CloudProvider describes the options passed to Kubernets cloud-provider options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| provider | Kubernetes cloud provider to use. (default: `aws`) | string | false |

[Back to TOC](#table-of-contents)

## ClusterConfiguration

ClusterConfiguration describes Kubernetes cluster options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| metadata |  | [metav1.ObjectMeta](https://v1-17.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#objectmeta-v1-meta) | true |
| spec |  | [ClusterConfigurationSpec](#clusterconfigurationspec) | false |

[Back to TOC](#table-of-contents)

## ClusterConfigurationSpec

ClusterConfigurationSpec is the spec that contains the Kubernetes cluster options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| kubernetes | Kubernetes specific properties. | [Kubernetes](#kubernetes) | false |
| autoProvisioning | Auto provisioning specific properties. | [AutoProvisioning](#autoprovisioning) | false |
| containerNetworking | Container networking specific properties. | [ContainerNetworking](#containernetworking) | false |
| containerRuntime | Container runtime specific properties. | [ContainerRuntime](#containerruntime) | false |
| imageRegistries | Container image registries related settings. | [][ImageRegistry](#imageregistry) | false |
| osPackages | Configure OS packages repositories. | [OSPackages](#ospackages) | false |
| nodePools | Node pool configurations. | [][NodePool](#nodepool) | false |
| addons | List of addons that can be deployed. | [][Addons](#addons) | false |
| version | Version of the cluster. | string | false |
| loggingOptions | LoggingOptions information with settings for the logging system environment | [LoggingOptions](#loggingoptions) | false |

[Back to TOC](#table-of-contents)

## ConfigData

ConfigData represents a file configuration for a Konvoy cluster component. It also specifies whether or not the configuration should be imported into the corresponding data. With a containerd version lower than v1.3.0 the `ConfigData` content can be merge or completely replace the existing configuration.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| data | [TOML configuration](https://github.com/containerd/cri/blob/master/docs/config.md) of containerd to be merged/replaced, or imported with versions (>=v1.3.0). | string | true |
| replace | Enable to use `configData.data`. Otherwise, merge `configData.data` with the internal default. (default: `false`) | bool | true |

[Back to TOC](#table-of-contents)

## ContainerNetworking

ContainerNetworking describes the CNI used by Kubernetes.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| calico | [Calico](https://www.projectcalico.org/) specific configurations. | [CalicoContainerNetworking](#calicocontainernetworking) | false |

[Back to TOC](#table-of-contents)

## ContainerRuntime

ContainerRuntime describes the runtime used by the Kubelet.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| containerd | [Containerd](https://containerd.io) specific configurations. | [ContainerdContainerRuntime](#containerdcontainerruntime) | false |

[Back to TOC](#table-of-contents)

## ContainerdContainerRuntime

ContainerdContainerRuntime describes containerd runtime options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| version | The version of the [containerd](https://containerd.io) runtime. | string | false |
| configData | Contains data for configuring the [containerd](https://containerd.io) runtime. | [ConfigData](#configdata) | false |

[Back to TOC](#table-of-contents)

## ControlPlane

ControlPlane contains all control plane related configurations.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| controlPlaneEndpointOverride | Overrides the `control_plane_endpoint` from `inventory.yaml`. | string | false |
| certificate | Certificate related configurations for the control plane. | [Certificate](#certificate) | false |
| keepalived | Keepalived configurations. | [Keepalived](#keepalived) | false |

[Back to TOC](#table-of-contents)

## Etcd

Etcd describes the settings for Etcd.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| imageRepository | The imageRepository to pull the etcd image from. \"/etcd\" will be appended at the end before pulling. (default: `k8s.gcr.io`) | string | false |
| imageTag | The imageTag of etcd image to use, defaulted internally to the kubernetes version default. | string | false |

[Back to TOC](#table-of-contents)

## GPU

GPU represents an object that contains details of user defined GPU info.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| nvidia | [NVIDIA](https://docs.nvidia.com/datacenter/kubernetes/kubernetes-upstream/index.htm) specific configuration. | [Nvidia](#nvidia) | false |

[Back to TOC](#table-of-contents)

## IPTables

IPTables describes different iptable modifications options that will be performed by Konvoy.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| addDefaultRules | If true add default rules to allow cluster communication. (default: `false`) | bool | false |

[Back to TOC](#table-of-contents)

## ImageRegistry

ImageRegistry describes the docker image registries that are automatically configured to be used by the ContainerRuntime.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| server | The full address including `https://` or `http://` and an optional port. | string | false |
| username | The registry user name. | string | false |
| password | The registry password. This setting requires you to provide a value for the `username` setting. | string | false |
| auth | Contains the base64 encoded `username:password`. | string | false |
| identityToken | Used to authenticate the user and get an access token. | string | false |
| default | When set `true`, containerd will be configured to try to pull images from this registry first, before pulling from any external registries. Konvoy will also use this registry to push images to when doing an air-gapped installation. | bool | false |

[Back to TOC](#table-of-contents)

## Keepalived

Keepalived describes different keepalived related options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| interface | The interface to run keepalived on. If not set, Konvoy will automatically guess the interface. | string | false |
| vrid | The Virtual Router ID (VRID) for keepalived. If not specified, Konvoy will randomly assign a VRID. | int32 | false |

[Back to TOC](#table-of-contents)

## Kubelet

Kubelet describes the settings for the Kubelet.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| cgroupRoot | Specifies the`--cgroup-root` flag for the Kubelet. | string | false |
| kubeReserved | Specifies the `--kube-reserved` flag for the Kubelet, on all of the nodes in the cluster. | string | false |

[Back to TOC](#table-of-contents)

## Kubernetes

Kubernetes controls the options used by `kubeadm` and at other points during installation.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| version | The version of Kubernetes to deploy. (default: `1.19.15`) | string | false |
| imageRepository | The imageRepository to pull the control-plane images from. (default: `k8s.gcr.io`) | string | false |
| controlPlane | Control plane specific configurations. | [ControlPlane](#controlplane) | false |
| networking | Cluster networking specific configurations. | [Networking](#networking) | false |
| cloudProvider | Cloud provider specific configurations. | [CloudProvider](#cloudprovider) | false |
| admissionPlugins | Configurations for admission plugins. | [AdmissionPlugins](#admissionplugins) | false |
| preflightChecks | Configurations for preflight checks. | [PreflightChecks](#preflightchecks) | false |
| apiserver | Configurations for APIServer. | [APIServer](#apiserver) | false |
| kubelet | Configurations for Kubelet. | [Kubelet](#kubelet) | false |
| etcd | Configurations for Etcd. | [Etcd](#etcd) | false |

[Back to TOC](#table-of-contents)

## LoggingOptions

LoggingOptions describes logging system options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| persistentStorage | PersistentStorage specifies how logs are stored. The detault is persistent. | bool | false |
| logRotationSize | LogRotationSize specifies the maximum size for individual journal files stored persistently in journald. The default is 1G. | string | false |
| logRetentionTime | LogRetentionTime specifies the maximum time to store journal entries. The default is 1 month. | string | false |
| logKeepFreePercentage | LogKeepFreePercentage specifies how much disk space systemd must leave free. The default is 20%. | string | false |
| logMaxUsageSize | LogMaxUsageSize specifies the maximum size the journal can use. The default is 8G. | string | false |

[Back to TOC](#table-of-contents)

## Networking

Networking describes different networking related options.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| podSubnet | The CIDR range where each pod IP will be assigned from. (default: `192.168.0.0/16`) | string | false |
| serviceSubnet | The CIDR range where each service VIP will be assigned from. (default: `10.0.0.0/18`) | string | false |
| httpProxy | The address to the HTTP proxy to set `HTTP_PROXY` env variable during installation. | string | false |
| httpsProxy | The address to the HTTPs proxy to set `HTTPS_PROXY` env variable during installation. | string | false |
| noProxy | List of addresses to pass to `NO_PROXY`. All node addresses, podSubnet, serviceSubnet, controlPlane endpoint and `127.0.0.1` and `localhost` are automatically set. | []string | false |
| iptables | OS iptables configuration. | [IPTables](#iptables) | false |

[Back to TOC](#table-of-contents)

## NodeLabel

NodeLabel represents a Kubernetes node label.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| key | The label key to be applied to a node. | string | true |
| value | The label value corresponding to the label key. | string | true |

[Back to TOC](#table-of-contents)

## NodePool

NodePool is an object that contains details of a node pool such as its name, taints and labels.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | The name of the node pool corresponding to that in `ClusterProvisioner.spec.nodePool`. (default: `control-plane` for control plane, `worker` for workers) | string | true |
| labels | User defined labels to set on all nodes in the node pool. | [][NodeLabel](#nodelabel) | false |
| taints | User defined taints to set on all nodes in the node pool. | [][NodeTaint](#nodetaint) | false |
| gpu | Configuration for any GPU enabled nodes in the node pool. | [GPU](#gpu) | false |
| operatingSystem | Operating System specific configuration | [OperatingSystem](#operatingsystem) | false |

[Back to TOC](#table-of-contents)

## NodeTaint

NodeTaint represents a Kubernetes taint to be applied to a node.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| key | The taint key to be applied to a node. | string | true |
| value | The taint value corresponding to the taint key. | string | true |
| effect | The effect of the taint on pods that do not tolerate the taint. Valid effects are `NoSchedule`, `PreferNoSchedule` and `NoExecute`. | string | true |

[Back to TOC](#table-of-contents)

## Nvidia

Nvidia defines the user configuration of Nvidia specific info.


## OSPackages

OSPackages configures the installation of linux package and related properties.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| enableAdditionalRepositories | Enable the installation of D2iQ, Kubernetes and Docker OS repositories. (default: `true`) | bool | false |

[Back to TOC](#table-of-contents)

## OperatingSystem

OperatingSystem defines user overrides for OS specific configuration

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| assumeDistribution | Override the automatically determined OS distribution Valid values are `CentOS`, `RedHat`, `Ubuntu`, `Debian` | string | false |

[Back to TOC](#table-of-contents)

## PreflightChecks

PreflightChecks describes the set of preflight checks to be performed.

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| errorsToIgnore | A list of errors to ignore for Ansible preflight checks. (default: depends on provisioner used) | []string | false |

[Back to TOC](#table-of-contents)
