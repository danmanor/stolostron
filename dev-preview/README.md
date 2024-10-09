## Getting Started with Development Preview Content
<!-- This URL uses a tag so we can predict the value -->
Links: [Release-ACM-2.11/MCE-2.6](https://github.com/stolostron/stolostron/tree/2.11/dev-preview)

Welcome to the hub for Red Hat Advanced Cluster Management Development preview content!  Many of our unique and upcoming features start as Development Preview content, available through the stolostron community for feedback and tight iteration as we discover and adapt to new use cases and usage patterns.

Below, you'll find a list of current dev-preview content complete with installation and usage instructions!  **Don't forget to give us feedback on our dev-preview content at acm-contact@redhat.com**. 

Features on Development Preview

- [Getting Started with Development Preview Content](#getting-started-with-development-preview-content)
- [Ansible Collection \& Inventory Plugin](#ansible-collection--inventory-plugin)
  - [Installation](#installation)
  - [Usage](#usage)
- [Dynamic Metric Collection (Custom Metrics Collection)](#dynamic-metric-collection-custom-metrics-collection)
  - [Installation](#installation-3)
  - [Usage](#usage-3)
- [Observability Instance Sizes](#observability-instance-sizes)
  - [Installation](#installation-8)
  - [Usage](#usage-8)


## Ansible Collection & Inventory Plugin

This Ansible Collection allows your operations teams to stay in their comfort zone and leverage Ansible to orchestrate multicluster operations in kubernetes with Red Hat Advanced Cluster Management for Kubernetes and Multicluster Engine. This Ansible collection also includes an inventory plugin, which registers all ACM-managed cluters within the Ansible Inventory, allowing you to use your entire toolbelt of Ansible collections conventiently against your fleet of clusters.

**Repository**: [stolostron/ansible-collection.core](https://github.com/stolostron/ansible-collection.core)

### Installation

Installation instructions can be found in the [repo](https://github.com/stolostron/ansible-collection.core) and the collection can be found on [Ansible Galaxy](https://galaxy.ansible.com/stolostron/core).

### Usage

Usage instructions can be found in the [repo](https://github.com/stolostron/ansible-collection.core) and the collection can be found on [Ansible Galaxy](https://galaxy.ansible.com/stolostron/core).

## Dynamic Metric Collection (Custom Metrics Collection) <!-- [ACM 2.8+] -->

Dynamic metrics collection refers to the ability to initiate metrics collection on managed clusters based on specific conditions. Collecting metrics consumes resources on your hub cluster. This is especially important when you considering metric collection across a large fleet of clusters. It makes sense to start collecting certain metrics only when they are likely going to be needed optimally using resources. When problems occur on a managed cluster, it may be necessary to collect metrics at a higher rate to help analyze the problems. Dynamic metrics collection enables both these use cases. Metrics collection stops automatically 15 minutes after the underlying condition no longer exists.

**Repository**: [stolostron/multicluster-observability-operator](https://github.com/stolostron/multicluster-observability-operator)

### Installation

No special installation is necessary to use this feature.

### Usage

Usage instructions and examples can be found in the [here](https://github.com/stolostron/multicluster-observability-operator/tree/main/dev-previews/dynamic-metrics-collection)

## Observability Instance Sizes

This feature provides the ability to control the scale of your ACM Observability instance. The existing mechanism to scale up Observability resources in the hub is to use `AdvancedConfig` in MultiClusterObservability CR. But this requires the user to be familiar with the intricacies of the components within Observability (Thanos. AlertManager, Observatorium API, etc.).

With Instance Sizes, users can now configure a set of resource requests across all their Observability components, sized proportionally, using a single field in their MCO CR, `InstanceSize`.

The sizes currently supported are: minimal, default, small, medium, large, xLarge, 2xLarge and 4xLarge, which represents a linear scale of usage for ACM MCO.
By default `InstanceSize` is set to `default`. This feature is entirely opt-in, and your existing `AdvancedConfig` will always override it.

The sizes themselves proportionally size MCO components according to a practical scale of usage. Our estimates indicate a measure like below (here total CPU/Memory are approximate request values for Hub Observability components),

| InstanceSize  | Active Timeseries Supported | Total CPU Request | Total Memory Request (GiB) |
|---------------|-----------------------------|-------------------|----------------------------|
| Default       | < 200k                      |                  3|                          12|
| Minimal       | < 1 million                 |                 16|                          25|
| Small         | 1 million                   |                 32|                          72|
| Medium        | 5 million                   |                 55|                         137|
| Large         | 10 million                  |                103|                         293|
| Xlarge        | 20 million                  |                163|                         590|
| 2xlarge       | 50 million                  |                222|                        1019|
| 4xlarge       | 100 million                 |                337|                        2158|


For details on how to size your cluster before enabling an InstanceSize, refer to this [spreadsheet](https://docs.google.com/spreadsheets/d/1ye8wDROJW2_VpR4imPtwXANJuBSWHCWKegoUzz-bWdU/edit?gid=0#gid=0).

### Installation

Follow the installation instructions in the above to install MCO operator, and ensure you have enough resources to support the particular size size.

### Usage

Simply set `InstanceSize` field on MCO CR to a value that would suit your monitoring needs.

## Multicluster Global Hub Security Dashboard

This feature enhances the multicluster global hub by adding a new dashboard within its Grafana instance, which aggregates security data from various [Red Hat Advanced Cluster Security for Kubernetes](https://www.redhat.com/en/technologies/cloud-computing/openshift/advanced-cluster-security-kubernetes) (RHACS) instances across managed clusters. This allows users to utilize the multicluster global hub to gain a comprehensive overview of the security status of their managed clusters.

For more information, see - [enable-rhacs-integration](https://github.com/stolostron/multicluster-global-hub/blob/main/doc/dev-preview.md#enable-rhacs-integration).

**Repository**: [stolostron/multicluster-global-hub](https://github.com/stolostron/multicluster-global-hub).

### Installation

RHACS installation required.

### Usage

Usage instructions can be found in - [enable-rhacs-integration](https://github.com/stolostron/multicluster-global-hub/blob/main/doc/dev-preview.md#enable-rhacs-integration).

### Dashboard Preview:

![RHACS Security Violations Dashboard](https://github.com/stolostron/multicluster-global-hub/blob/main/doc/images/rhacs-global-hub-dashboard.png)

# Graduated features

### Hosted Control Planes with MCE (MCE 2.5)
  
  * Usage and use-case documentation can be found in the [Hosted Control Plane Clusters section of the doc](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/multicluster_global_hub/index).  

### Multicluster Global Hub (ACM 2.9)
  
  * Usage instructions and examples can be found in the [Getting Started Section](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html/clusters/cluster_mce_overview#hosted-control-planes-intro).

### Finer-Grained Access Control to Observability Metrics (ACM 2.11)
  
  * Usage instructions and examples can be found [here](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html-single/observability/index#configure-fine-grain-rbac)

### Configurable Collection in Search (ACM 2.7)
  
  * The process for filtering resources is outlined [here](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.11/html-single/observability/index#creating-search-configurable-collection).  

### Search-v2 - Odyssey
  
  * Search-v2 brings a re-architected backbone facilitating greater scale and resiliance within the service.  
