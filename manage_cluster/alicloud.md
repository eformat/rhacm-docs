---

copyright:
  years: 2019, 2020
lastupdated: "2020-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:child: .link .ulchildlink}
{:childlinks: .ullinks}

# Importing an Alibaba Cloud cluster

**Important: This content is a technical preview, and should not be relied on in a production environment.** <!--this is expected to be removed, but waiting on confirmation-->

You can import existing Alibaba Cloud clusters.

**Note:** By default, the `multicluster-endpoint` deployment pulls all of the required images from Docker Hub. You only need to install images from DockerHub if you are working in an air gapped environment.

1. From the navigation menu, click **Clusters**.

2. Click **Add cluster**.

3. Click **Import an existing cluster...** > **Select**.

4. Provide a unique cluster name and a unique cluster namespace on the _Configure cluster_ page.

5. Click to expand **Edit cluster import YAML file** and edit the file.

   See [_Table 1. YAML file parameters and description_](#table_1) for details about each parameter.

   **Note:** Do not remove parameters, as the console might not properly render.
   
6. Click **Generate Command** to retrieve the command to deploy the `multicluster-endpoint`.

   **Optional**: You can add labels by clicking **Configure advanced parameters** and use these labels to search.

7. From the _Import an existing cluster_ window, hover and click the **Copy command** icon to copy the import command and the token that you are provided. Note: You must click this icon to receive the accurate copy.

8. Go to your terminal and configure your `kubectl` for your targeted managed cluster.

9. Prepare the `import.yaml` file for the Alibaba Cloud cluster.

    **Note:** If your managed Alibaba Cloud cluster cannot resolve the domain name of your Red Hat Advanced Cluster Management for Kubernetes hub cluster, you must manually download the `import.yaml` file and change the domain name to IP from bootstrap secret.

    1. Paste the following command in the terminal, then modify the command to download the `import.yaml` file:

    ```
    curl -k -H <token> https://<mcm-hub-cluster-IP>:443/api/v1/clusters/<clustername>/<clusternamespace>/import.yaml > importAlicluster.yaml
    ```
    {:codeblock}

    2. Change domain name to IP from bootstrap secret. Modify the `import.yaml` file and copy the kubeconfig data from ` multicluster-endpoint-bootstrap` secret section.
    
    Run the following command to decode the kubeconfig data:
    
    ```
    echo <kubeconfig-data> | base64 -d
    ```
    {:codeblock}

    Change the server URL from hub cluster domain name to IP, then paste the kubeconfig into a temporary file.

    Run the following command to encode your kubeconfig data:

    ```
    cat <kubeconfig-temp-file> | base64 --warp=0
    ```
    {:codeblock}

    Replace the data of ` multicluster-endpoint-bootstrap` secret with your kubeconfig data. 
    
    **Note:** If your managed Alibaba Cloud cluster ingress type is `LoadBalancer`, you can predefine the `service type` of `work-manager` in endpoint section.

    3. Add the following configuration to the `import.yaml` endpoint `spec`:

      ```
      workManager:
        service:
          type: LoadBalancer
      ```
      {:codeblock}

10. Run the following command to deploy the `multicluster-endpoint`:

      ```
      kubectl apply -f <importAlicluster.yaml>
      ```
      {:codeblock}

      If you receive the following error, run the command again:

      ```
      error: unable to recognize "STDIN": no matches for kind "Endpoint" in version "multicloud.ibm.com/v1beta1"
      ```
      {:codeblock}

11. Go back to your console and click **View cluster** to view the _Overview_ page and a summary of your cluster