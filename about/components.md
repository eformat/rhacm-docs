---

copyright:
  years: 2020
lastupdated: "2020-03-30"

---

# Components

See the following tables for information about components that are installed and enabled on the hub cluster by default and the managed cluster. See what components are required and if it applies, the default value that is required.


- [Default enabled services](#default-enabled-services)
- [Default enabled hub cluster components](#default-enabled-hub-cluster-components)
- [Default enabled components managed cluster](#default-enabled-managed-cluster-components)

## Default enabled services

|Service|Description|Required|
|--------|-----------|-------------------|
|management-ingress|Unifies all management services behind a network ingress controller with predictable annotations and TLS protection. This service should not be accessed directly.|Yes|
|cert-manager|This service manages the lifecycle of certificates.|Yes|
|cert-manager-webhook|This service extends the Kubernetes API server so the certificate manager resources can be dynamically validated.|Yes|
|configmap-watcher|This service can be used to restart pods when a dependent config map is updated.|Yes|
|mongo-db|All platform services that require a persistent data store use the MongoDB service. Highly available topologies for MongoDB are supported out of the box. This is a service that should not be accessed directly.|Yes, 5G|
|etcd|A distributed key-value store|Yes|
{: caption="Table 1. Red Hat Advanced Cluster Management for Kubernetes default enabled services" caption-side="top"}

## Default enabled hub cluster components

|Service|Description (needed)|Required|
|--------|-----------|---------------------|
|application-ui|The web console for managing the lifecycle of applications.|Yes|
|console-api|Provide the backend API for the console-ui service.|Yes|
|console-ui|Provide a view of the resources available in the cluster with support for creation, modification, or removal.|Yes|
|console-header|Provides a set of services available in the header of the web console|Yes|
|grc-ui|The web console for Governance and Risk management in Red Hat Advanced Cluster Management for Kubernetes|Yes|
|grc-ui-api|The API service for managing Governance and Risk in Red Hat Advanced Cluster Management for Kubernetes|Yes|
|grc-policy-propogator|Process events and requests to Red Hat Advanced Cluster Management for Kubernetes resources|Yes|
|hive|Provides cluster provisioning and life cycle management|Yes|
|kui-web-terminal|Provides the Visual Web Terminal.|Yes|
|mcm-apiserver|A REST API server for managing Kubernetes objects related to Red Hat Advanced Cluster Management for Kubernetes|Yes|
|mcm-controller|Service that processes events and requests to Red Hat Advanced Cluster Management for Kubernetes resources|Yes|
|mcm-webhook|This service extends the Kubernetes API server so the `mcm-apiserver` resources can be dynamically validated.|Yes|
|multicluster-operators|Manages and reconciles subscriptions|Yes|
|multiclusterhub-operator| Operator for installing Red Hat Advanced Cluster Management for Kubernetes on a hub cluster|Yes|
|multiclusterhub-repo| Service for hosting internal-facing Helm repository, pre-populated with required component Helm charts |Yes|
|rcm-api|Handles API requests related to cluster lifecycle management|Yes|
|rcm-controller|Controller that handles cluster lifecycle management|Yes|
|redisgraph-tls|Cache for search data|Yes|
|search-aggregator|Receives and indexes data from `search-collector` in managed clusters|Yes|
|search-api|Provides the API for the search service|Yes|
|search-collector|Provides the capability to search for resources using the console and Visual Web Terminal |Yes|
|topology-aggregator|Indexes data received for the topology views|Yes|
|topology|Provides the user interface for the Topology dashboard|Yes|
|topology-api|Provides the backend services for the topology-ui service|Yes|
{: caption="Table 2. Red Hat Advanced Cluster Management for Kubernetes default enabled components on the hub cluster" caption-side="top"}

## Default enabled managed cluster components

The following table shows the services that are installed on the managed cluster:

|Service|Description (needed)|Required need dev input|
|--------|-----------|-------------------|
|applicationManager|Processes events and other requests to managed resources.|Yes|
|certPolicyController|Monitors certificate expiration based on distributed policies.|Yes|
|component-operator|Handles the deployment of internal components on the endpoint|Yes|
|connmgr|Manages connection from the managed cluster to the hub|Yes|
|iamPolicyController|Monitors identity controls based on distributed policies|Yes|
|imageRegistry|quay.io/open-cluster-management|Yes|
|operator|Handles the deployment of internal Helm chart components|Yes|
|policyController|Distributes configured policies and monitors Kubernetes-based policies|Yes|
|searchCollector|Collects cluster data to be indexed by search components on the hub cluster|Yes|
|svcreg|Internal service registry that processes events|Yes|
|svcreg-coredns|DNS service used by the endpoint|Yes|
|topologyCollector|Collects cluster data to be indexed by the topology components on the hub cluster|Yes|
|workmgr|Component that handles endpoint work requests  and managed cluster status|Yes|
{: caption="Table 3. Red Hat Advanced Cluster Management for Kubernetes enabled components on the managed cluster" caption-side="top"}
