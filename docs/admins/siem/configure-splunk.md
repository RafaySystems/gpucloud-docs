---
title: Aggregate Audit Logs to SIEM - Splunk and Splunk Cloud
description: Stream your organization's audit logs to Splunk and Splunk Cloud for monitoring and analysis
tags:
  - Audit Logs
  - SIEM
  - Splunk
  - Splunk Cloud
  - Log Aggregation
---


To scrape and send audit log data to a Splunk server using the web console or the command line (RCTL).


=== "Web Console"

    Use the web console to configure your audit logs.

    ## Prerequisites

    - Customize the Values file (YAML). (See [below for creating a values.yaml file](#creating--values--yaml)).
    - Create a namespace in your cluster.


    ## Configure Workload

    **Note**: Only one audit log workload is needed for an organization.

    1. In the web console, select **Catalog**.
    2. For Filter by Catalog, select **default-rafay**.
      ![Repositories](img/catalog-default.png)
    3. Select **rafay-splunk**, then select **Create Workload**.
      ![Create Workload](img/createworkload-splunk.png)
    4. Enter a name for the workload. Example: rafay-audit-logs.
    5. Select the namespace.
      ![New Repository](img/helmrepo-namespace-splunk.png)
    6. Click **Continue**.
    7. On the Repository tab, for **Values yaml**:
        - Create a **values.yaml** file. (See [below for creating a values.yaml file](#creating--values--yaml))
        - Click **Upload Files**.
        - Select the **values.yaml** file.
        - Click **Open**.
          ![Workload Configuration](img/workloadconfig-splunk.png)
    8. Click **Save and Go to Placement**.
    9. Update the following for Placements:
        - Select the appropriate **Drift Action**.
        - Select **Specified Clusters** for the Placement Policy.
        - Select the cluster from the cluster list.
        - Click **Save and go to Publish**.
    10. Click **Publish**.


=== "RCTL"

    Use the Command Line Interface (RCTL) to automate reproducible workflows without having to use the web console.

    ## Prerequisites

    - Download RCTL
    - Configure RCTL
    - Customize the Values file (YAML). (See [below for creating a values.yaml file](#creating--values--yaml)).
    - Create a namespace in your cluster.

    **Note**: Set the correct project using RCTL.


    ## Create a Repository

    Create a repository.yaml file using the following example. Replace **demo** with the name of the project you are adding this repository to. Optionally, you can change **helm-repo** to another name; if you change the name, use that name for **repository_ref** in the workload.yaml file (see [Create a Workload](#create--workload)).

    ```
    apiVersion: config.rafay.dev/v2
    kind: Repository
    metadata:
      name: helm-repo
      project: demo
    spec:
      repositoryType: HelmRepository
      endpoint: https://rafaysystems.github.io/rafay-helm-charts/
      credentialType: CredentialTypeNotSet
    ```

    Run the create repository command and include the repository.yaml file.
    ```
    ./rctl create repository -f repository.yaml
    ```


    <a id="create--workload"></a>
    ## Create a Workload

    Create a workload.yaml file using the following example. Replace the names used in **clusters**, **namespace**, and **project** to match your environment where you want to publish the workload.

    ```
    name: audit-logs
    namespace: ns-name
    type: Helm
    project: demo
    clusters: demo-cluster
    repository_ref: helm-repo
    repo_artifact_meta:
      helm:
        chartName: rafay-splunk
    values: ./values.yaml
    ```

    Run the create workload command and include the workload.yaml file.
    ```
    ./rctl create workload workload.yaml
    ```


    ## Publish a Workload

    Run the publish workload command. Replace **workload-name** with the name used in the workload.yaml file. Example: audit-logs.
    ```
    ./rctl publish workload workload-name
    ```


---
<a id="creating--values--yaml"></a>
## Values YAML File

Create a values.yaml file that contains your Splunk information. Use the example below and change the following:

- `rafay_api_key` - Your organization's API key. In the web console, select **My Tools > Manage Keys**.
- `rafay_api_secret` - Your organization's API Secret key. In the web console, select **My Tools > Manage Keys**.
- `host` - The root domain of your Splunk Server. You can find this in the URL field after you log in to your Splunk console. Example: `splunkserver.mycompany.com`.
- `index` - The name of the Splunk index. (See [below for creating a Splunk index](#creating--splunk--index))
- `ssl_verify` (Optional) - Only change to `False` if you are using an insecure Splunk server.
- `token` - The Splunk HTTP Event Collector (Splunk HEC) token value. (See [below for creating a Splunk HEC](#creating--splunk--hec))
- `secret_name` - (Optional) Specify existing k8s secret name that contains your organization's API key, secret and splunk token. (See [below is an example of k8s secret](#example--k8s--secret))


```yaml
# Default values for rafay splunk audit log integration.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

config:
  ## Rafay console URL
  url: https://console.rafay.dev
  ## Rafay API Key
  rafay_api_key: API_KEY
  ## Rafay API Secret
  rafay_api_secret: API_SECRET
  ## Send Initial logs to splunk adog based on following value. Defaults to "14d" days
  filter: 14d
  ## Time Interval to send logs to splunk
  interval: 1m
  ## Splunk Server Host
  host: splunkserver.mycompany.com
  ## Splunk Server Port
  port: 8088
  ## Splunk HEC Token
  splunk_token: SPLUNK_TOKEN
  ## Set to False for insecure splunk server
  ssl_verify: True
  ## Index name to store audit logs to
  index: k8s-cluster-audit
  ## Existning Secret Name or leave it empty
  secret_name: ""
image:
  repository: registry.rafay-edge.net/rafay-logs/rafay-splunk
  pullPolicy: Always
  # Overrides the image tag whose default is the chart appVersion.
  tag: 0.3.9
serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # Annotations to add to the service account
  annotations: {}
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name:
rbac:
  create: true
replicaCount: 1
imagePullSecrets: []
nameOverride: ""
fullnameOverride: ""
deploymentAnnotations: {}
podAnnotations: {}
resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #   cpu: 100m
  #   memory: 128Mi
  # requests:
  #   cpu: 100m
  #   memory: 128Mi
nodeSelector: {}
tolerations: []
affinity: {}
```


---
<a id="creating--splunk--index"></a>
## Creating a Splunk Index

1. In the Splunk console, select **Settings > Indexes**.
2. Click **New Index**.
3. Enter a name for the index. Example: **audit-logs-splunk**.
4. Make sure **Events** is selected.
5. For **Max raw data size**, enter the maximum size of the index. Example: 2GB.
6. For **Searchable time (days)**, enter the number of days to include in the search results. Example: 30 days.
7. Click **Save**.
8. Copy the index name and paste it for the `index` in the **values.yaml** file.

<a id="creating--splunk--hec"></a>
## Creating a Splunk HEC

Create a Splunk HTTP Event Collector (HEC).

1. In the Splunk console, select **Settings > Data Inputs**.
2. Click **HTTP Event Collector**.
3. Click **New Token**.
4. Enter a name for the collector (example: audit-Logs), then click **Next**.
5. For **Source type**, click **Select**, type **json**, then select `_json`.
6. Click **Review**.
7. Click **Submit**.
8. Copy the token value and paste it for the `token` in the **values.yaml** file.


---
<a id="example--k8s--secret"></a>
## Example of k8s secret with API Key, Secret and Splink token.
```yaml
apiVersion: v1
kind: Secret
data:
  rafaykey: cmFmYXlrZXkK
  rafaysecret: cmFmYXlzZWNyZXQK
  token: dG9rZW4K
```
