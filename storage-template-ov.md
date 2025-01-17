---

copyright:
  years: 2020, 2023
lastupdated: "2023-05-17"

keywords: satellite storage, storage template, satellite config, block, file, ocs

subcollection: satellite

---

{{site.data.keyword.attribute-definition-list}}

# Understanding {{site.data.keyword.satelliteshort}} storage
{: #storage-template-ov}

Before you can decide what type of storage is the right solution for your {{site.data.keyword.satelliteshort}} clusters, you must understand the infrastructure provider, your app requirements, the type of data that you want to store, and how often you want to access this data. For more information, see [choosing a storage solution](/docs/openshift?topic=openshift-storage-plan).

Before you can use storage templates and configurations to manage your storage resources across locations and clusters, make sure you [Set up {{site.data.keyword.satelliteshort}} Config](/docs/satellite?topic=satellite-setup-clusters-satconfig) in your location.
{: note}


## What are my options for deploying storage to {{site.data.keyword.satelliteshort}}?
{: #storage-sat-configure}

You have two options when configuring storage in {{site.data.keyword.satelliteshort}}. The first is by using one of the provided storage templates. The second is by bringing your own storage drivers (BYOD), Helm charts, or Operators from the IBM Cloud Catalog, OperatorHub, or GitHub repo. 
{: shortdesc}

{{site.data.keyword.satelliteshort}} storage templates
:   You can create storage configurations by [using the {{site.data.keyword.satelliteshort}} storage template for the storage provider or driver](#storage-template-ov-providers) that you want to use. After you create a storage configuration by using a template, you can assign your storage configuration to your clusters or services. By using storage templates, you can create storage configurations that can be consistently assigned, updated, and managed across the clusters, service clusters, and cluster groups in your location.

Bring your own Operators, drivers, and plug-ins
:   You can also bring your own storage drivers to {{site.data.keyword.satelliteshort}} by installing them from the Catalog, OperatorHub, Helm charts, or by using your preferred method of deploying images to your clusters including images and drivers from various {{site.data.keyword.cloud_notm}} storage and partner solutions, for example Portworx. Bringing your own storage driver is functionally supported, but you are responsible for the entire lifecycle operations, installation, troubleshooting, and support.

While bringing your own drivers or operators to your {{site.data.keyword.satelliteshort}} clusters is possible, if you want to deploy {{site.data.keyword.cloud_notm}} services that use storage make sure you use one of the provided storage templates.
{: note}

## Which deployment option should I use?
{: #storage-template-services}

Since {{site.data.keyword.satelliteshort}} storage templates are supported by {{site.data.keyword.cloud_notm}} and the configurations that you create by deploying templates can be used across your {{site.data.keyword.satelliteshort}} clusters, service clusters, and cluster groups, templates are the preferred option when setting up storage for services in {{site.data.keyword.satelliteshort}}.

If the storage solution that you want to use does not have a {{site.data.keyword.satelliteshort}} template available, check the IBM Cloud Catalog for supported Helm charts and Operators.


## What are the benefits of using templates?
{: #storage-template-benefits}

With {{site.data.keyword.satelliteshort}} storage templates, you can create a storage configuration that can be deployed across your clusters without the need to re-create the configuration for each cluster.
{: shortdesc}

The {{site.data.keyword.satelliteshort}} storage templates are provided and tested by {{site.data.keyword.IBM_notm}} or third-party vendors. {{site.data.keyword.IBM_notm}} provides the configuration tooling to install the storage drivers on clusters in your {{site.data.keyword.satelliteshort}} location as described in the templates. For issues with the installation process, you can contact {{site.data.keyword.IBM_notm}}. However, for issues with lifecycle operations of the storage devices, contact the storage provider.

When you use a {{site.data.keyword.satelliteshort}} storage template to create a configuration, you include the details for the storage provider that you want to use. Each template contains a set of parameters that is specific to the storage provider. These parameters include things like credentials, device information, worker nodes, and more. After you use a template to create a storage configuration, you can reuse that configuration to assign storage across your {{site.data.keyword.satelliteshort}} clusters.

You can also quickly update the configuration parameters and apply them automatically across clusters, service clusters, and cluster groups in your locations.

| Feature or benefit | {{site.data.keyword.satelliteshort}} storage templates | Bring your own drivers |
| --- | --- | --- |
| Integrated with the {{site.data.keyword.satelliteshort}} interface. | Yes | No |
| Quickly and consistently install storage drivers across multiple clusters. | Yes| No |
| Repeatable, site-specific or storage-specific configurations. | Yes | No |
| Certified and tested with {{site.data.keyword.satelliteshort}}. | Yes| No |
{: caption="Comparison of supported features between using {{site.data.keyword.satelliteshort}} storage templates and bringing your own storage drivers" caption-side="bottom"}


## How do templates work?
{: #storage-template-flow}

When you create a configuration by using a template, you specify a set of parameters for the storage provider that you want to use. These parameters preset values that are used when you deploy storage drivers, create persistent volumes, provision instances, or use other functions depending on the provider and the type of storage that you want to use. For more information, see the [list of available storage templates](#storage-template-ov-providers).
{: shortdesc}

The following image depicts the workflow for creating a {{site.data.keyword.satelliteshort}} storage configuration by using a storage template.

1. Select the storage template that you want to use for your configuration.
2. Create a {{site.data.keyword.satelliteshort}} cluster. Make sure that you select the **Enable cluster admin access for {{site.data.keyword.satelliteshort}} Config** option when you create the cluster. If you don't enable Administrator (admin) access for {{site.data.keyword.satelliteshort}} Config when creating your cluster, you must re-create your cluster and enable admin access before you can deploy storage.
3. Assign your {{site.data.keyword.satelliteshort}} storage configuration to your clusters.
4. {{site.data.keyword.satelliteshort}} deploys the storage drivers and any solution-specific resources for the provider that you selected to the clusters that you assigned the storage configuration to.

![Concept overview of Satellite storage templates](/images/storage-template.svg){: caption="Figure 1. A conceptual overview of creating a storage configuration by using a template." caption-side="bottom"}


## Which storage templates are available?
{: #storage-template-ov-providers}

You can create a {{site.data.keyword.satelliteshort}} storage configuration by using a template for the storage provider that you want to use. If your preferred storage provider does not have a template, you can [create your own configuration template](https://github.com/{{site.data.keyword.IBM_notm}}/ibm-satellite-storage){: external} or you can manually deploy storage drivers. The following list includes the storage templates are currently available to deploy to your {{site.data.keyword.satelliteshort}} clusters.
{: shortdesc}

| Template name | Template CLI name | Version | Revision | Supported status |
| --- | --- | --- | --- | --- |
| [AWS EBS CSI Driver](/docs/satellite?topic=satellite-storage-aws-ebs-csi-driver) | `aws-ebs-csi-driver` | 1.1.0 | 5 | Supported |
| [AWS EBS CSI Driver](/docs/satellite?topic=satellite-storage-aws-ebs-csi-driver) | `aws-ebs-csi-driver` | 1.5.1 | 5 | Supported |
| [AWS EBS CSI Driver](/docs/satellite?topic=satellite-storage-aws-ebs-csi-driver) | `aws-ebs-csi-driver` | 1.12.0 (Default) | 2 | Supported |
| [AWS EFS CSI Driver](/docs/satellite?topic=satellite-storage-aws-efs-csi-driver) | `aws-efs-csi-driver` | 1.3.1 | 4 | Supported |
| [AWS EFS CSI Driver](/docs/satellite?topic=satellite-storage-aws-efs-csi-driver) | `aws-efs-csi-driver` | 1.3.7 | 4 | Supported |
| [AWS EFS CSI Driver](/docs/satellite?topic=satellite-storage-aws-efs-csi-driver) | `aws-efs-csi-driver` | 1.4.2 (Default) | 1 | Supported |
| [Azure Disk CSI Driver](/docs/satellite?topic=satellite-storage-azuredisk-csi-driver) | `azuredisk-csi-driver` | 1.4.0 | 5 | Supported |
| [Azure Disk CSI Driver](/docs/satellite?topic=satellite-storage-azuredisk-csi-driver) | `azuredisk-csi-driver` | 1.18.0 | 5 | Supported |
| [Azure Disk CSI Driver](/docs/satellite?topic=satellite-storage-azuredisk-csi-driver) | `azuredisk-csi-driver` | 1.23.0 (Default) | 1 | Supported |
| [Azure File CSI Driver](/docs/satellite?topic=satellite-storage-azurefile-csi-driver) | `azurefile-csi-driver` | 1.9.0 | 4 | Supported |
| [Azure File CSI Driver](/docs/satellite?topic=satellite-storage-azurefile-csi-driver) | `azurefile-csi-driver` | 1.18.0 | 4 | Supported |
| [Azure File CSI Driver](/docs/satellite?topic=satellite-storage-azurefile-csi-driver) | `azurefile-csi-driver` | 1.22.0 (Default) | 1 | Supported |
| [GCP Compute Persistent Disk CSI Driver](/docs/satellite?topic=satellite-storage-gcp-compute-persistent-disk-csi-driver) | `gcp-compute-persistent-disk-csi-driver` | 1.0.4 | 4 | Deprecated |
| [GCP Compute Persistent Disk CSI Driver](/docs/satellite?topic=satellite-storage-gcp-compute-persistent-disk-csi-driver) | `gcp-compute-persistent-disk-csi-driver` | 1.7.1 | 5 | Supported |
| [GCP Compute Persistent Disk CSI Driver](/docs/satellite?topic=satellite-storage-gcp-compute-persistent-disk-csi-driver) | `gcp-compute-persistent-disk-csi-driver` | 1.8.0 (Default) | 2 | Supported |
| [IBM Object Storage Plugin](/docs/satellite?topic=satellite-storage-ibm-object-storage-plugin) | `ibm-object-storage-plugin` | 2.2 (Default) | 11 | Supported |
| [IBM System Storage Block CSI driver](/docs/satellite?topic=satellite-storage-ibm-system-storage-block-csi-driver) | `ibm-system-storage-block-csi-driver` | 1.4.0 | 2 | Deprecated |
| [IBM System Storage Block CSI driver](/docs/satellite?topic=satellite-storage-ibm-system-storage-block-csi-driver) | `ibm-system-storage-block-csi-driver` | 1.5.0 | 2 | Deprecated |
| [IBM System Storage Block CSI driver](/docs/satellite?topic=satellite-storage-ibm-system-storage-block-csi-driver) | `ibm-system-storage-block-csi-driver` | 1.10.0 (Default) | 1 | Supported |
| [IBM System Storage Block CSI driver](/docs/satellite?topic=satellite-storage-ibm-system-storage-block-csi-driver) | `ibm-system-storage-block-csi-driver` | 1.11.1 | 1 | Supported |
| [[Beta] IBM VPC Block CSI driver](/docs/satellite?topic=satellite-storage-ibm-vpc-block-csi-driver) | `ibm-vpc-block-csi-driver` | 5.0 (Default) | 10 | Supported |
| [Local Storage Operator - Block](/docs/satellite?topic=satellite-storage-local-volume-block) | `local-volume-block` | 4.8 | 4 | Supported |
| [Local Storage Operator - Block](/docs/satellite?topic=satellite-storage-local-volume-block) | `local-volume-block` | 4.9 | 4 | Supported |
| [Local Storage Operator - Block](/docs/satellite?topic=satellite-storage-local-volume-block) | `local-volume-block` | 4.10 (Default) | 4 | Supported |
| [Local Storage Operator - Block](/docs/satellite?topic=satellite-storage-local-volume-block) | `local-volume-block` | 4.11 | 1 | Supported |
| [Local Storage Operator - Block](/docs/satellite?topic=satellite-storage-local-volume-block) | `local-volume-block` | 4.12 | 1 | Supported |
| [Local Storage Operator - File](/docs/satellite?topic=satellite-storage-local-volume-file) | `local-volume-file` | 4.8 | 4 | Supported |
| [Local Storage Operator - File](/docs/satellite?topic=satellite-storage-local-volume-file) | `local-volume-file` | 4.9 | 4 | Supported |
| [Local Storage Operator - File](/docs/satellite?topic=satellite-storage-local-volume-file) | `local-volume-file` | 4.10 (Default) | 4 | Supported |
| [Local Storage Operator - File](/docs/satellite?topic=satellite-storage-local-volume-file) | `local-volume-file` | 4.11 | 1 | Supported |
| [Local Storage Operator - File](/docs/satellite?topic=satellite-storage-local-volume-file) | `local-volume-file` | 4.12 | 1 | Supported |
| [NetApp Ontap-NAS Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-nas) | `netapp-ontap-nas` | 21.04 | 20 | Supported |
| [NetApp Ontap-NAS Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-nas) | `netapp-ontap-nas` | 22.04 | 18 | Supported |
| [NetApp Ontap-NAS Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-nas) | `netapp-ontap-nas` | 22.10 (Default) | 5 | Supported |
| [NetApp Ontap-SAN Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-san) | `netapp-ontap-san` | 21.04 | 21 | Supported |
| [NetApp Ontap-SAN Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-san) | `netapp-ontap-san` | 22.04 | 18 | Supported |
| [NetApp Ontap-SAN Driver](/docs/satellite?topic=satellite-storage-netapp-ontap-san) | `netapp-ontap-san` | 22.10 (Default) | 5 | Supported |
| [NetApp Trident Operator](/docs/satellite?topic=satellite-storage-netapp-trident) | `netapp-trident` | 21.04 | 4 | Supported |
| [NetApp Trident Operator](/docs/satellite?topic=satellite-storage-netapp-trident) | `netapp-trident` | 22.04 | 3 | Supported |
| [NetApp Trident Operator](/docs/satellite?topic=satellite-storage-netapp-trident) | `netapp-trident` | 22.10 (Default) | 1 | Supported |
| [OpenShift Data Foundation for local devices](/docs/satellite?topic=satellite-storage-odf-local) | `odf-local` | 4.9 | 23 | Supported |
| [OpenShift Data Foundation for local devices](/docs/satellite?topic=satellite-storage-odf-local) | `odf-local` | 4.10 (Default) | 17 | Supported |
| [OpenShift Data Foundation for local devices](/docs/satellite?topic=satellite-storage-odf-local) | `odf-local` | 4.11 | 6 | Supported |
| [OpenShift Data Foundation for local devices](/docs/satellite?topic=satellite-storage-odf-local) | `odf-local` | 4.12 | 2 | Supported |
| [OpenShift Data Foundation for remote storage](/docs/satellite?topic=satellite-storage-odf-remote) | `odf-remote` | 4.9 | 23 | Supported |
| [OpenShift Data Foundation for remote storage](/docs/satellite?topic=satellite-storage-odf-remote) | `odf-remote` | 4.10 (Default) | 17 | Supported |
| [OpenShift Data Foundation for remote storage](/docs/satellite?topic=satellite-storage-odf-remote) | `odf-remote` | 4.11 | 6 | Supported |
| [OpenShift Data Foundation for remote storage](/docs/satellite?topic=satellite-storage-odf-remote) | `odf-remote` | 4.12 | 2 | Supported |
| [VMware CSI Driver](/docs/satellite?topic=satellite-storage-vsphere-csi-driver) | `vsphere-csi-driver` | 2.5.1 (Default) | 6 | Supported |
{: caption="Storage template versions" caption-side="bottom"}


