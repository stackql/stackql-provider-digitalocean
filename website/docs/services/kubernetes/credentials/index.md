--- 
title: credentials
hide_title: false
hide_table_of_contents: false
keywords:
  - credentials
  - kubernetes
  - digitalocean
  - infrastructure-as-code
  - configuration-as-data
  - cloud inventory
description: Query, deploy and manage digitalocean resources using SQL
custom_edit_url: null
image: /img/stackql-digitalocean-provider-featured-image.png
---

import CopyableCode from '@site/src/components/CopyableCode/CopyableCode';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Creates, updates, deletes, gets or lists a <code>credentials</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>credentials</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.kubernetes.credentials" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="kubernetes_get_credentials"
    values={[
        { label: 'kubernetes_get_credentials', value: 'kubernetes_get_credentials' }
    ]}
>
<TabItem value="kubernetes_get_credentials">

A JSON object containing credentials for a cluster.

<table>
<thead>
    <tr>
    <th>Name</th>
    <th>Datatype</th>
    <th>Description</th>
    </tr>
</thead>
<tbody>
</tbody>
</table>
</TabItem>
</Tabs>

## Methods

The following methods are available for this resource:

<table>
<thead>
    <tr>
    <th>Name</th>
    <th>Accessible by</th>
    <th>Required Params</th>
    <th>Optional Params</th>
    <th>Description</th>
    </tr>
</thead>
<tbody>
<tr>
    <td><a href="#kubernetes_get_credentials"><CopyableCode code="kubernetes_get_credentials" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-cluster_id"><code>cluster_id</code></a></td>
    <td><a href="#parameter-expiry_seconds"><code>expiry_seconds</code></a></td>
    <td>This endpoint returns a JSON object . It can be used to programmatically<br />construct Kubernetes clients which cannot parse kubeconfig files.<br /><br />The resulting JSON object contains token-based authentication for clusters<br />supporting it, and certificate-based authentication otherwise. For a list of<br />supported versions and more information, see "[How to Connect to a DigitalOcean<br />Kubernetes Cluster](https://docs.digitalocean.com/products/kubernetes/how-to/connect-to-cluster/)".<br /><br />To retrieve credentials for accessing a Kubernetes cluster, send a GET<br />request to `/v2/kubernetes/clusters/$K8S_CLUSTER_ID/credentials`.<br /><br />Clusters supporting token-based authentication may define an expiration by<br />passing a duration in seconds as a query parameter to<br />`/v2/kubernetes/clusters/$K8S_CLUSTER_ID/credentials?expiry_seconds=$DURATION_IN_SECONDS`.<br />If not set or 0, then the token will have a 7 day expiry. The query parameter<br />has no impact in certificate-based authentication.<br /></td>
</tr>
</tbody>
</table>

## Parameters

Parameters can be passed in the `WHERE` clause of a query. Check the [Methods](#methods) section to see which parameters are required or optional for each operation.

<table>
<thead>
    <tr>
    <th>Name</th>
    <th>Datatype</th>
    <th>Description</th>
    </tr>
</thead>
<tbody>
<tr id="parameter-cluster_id">
    <td><CopyableCode code="cluster_id" /></td>
    <td><code>string (uuid)</code></td>
    <td>A unique ID that can be used to reference a Kubernetes cluster. (example: bd5f5959-5e1e-4205-a714-a914373942af)</td>
</tr>
<tr id="parameter-expiry_seconds">
    <td><CopyableCode code="expiry_seconds" /></td>
    <td><code>integer</code></td>
    <td>The duration in seconds that the returned Kubernetes credentials will be valid. If not set or 0, the credentials will have a 7 day expiry. (example: 300)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="kubernetes_get_credentials"
    values={[
        { label: 'kubernetes_get_credentials', value: 'kubernetes_get_credentials' }
    ]}
>
<TabItem value="kubernetes_get_credentials">

This endpoint returns a JSON object . It can be used to programmatically<br />construct Kubernetes clients which cannot parse kubeconfig files.<br /><br />The resulting JSON object contains token-based authentication for clusters<br />supporting it, and certificate-based authentication otherwise. For a list of<br />supported versions and more information, see "[How to Connect to a DigitalOcean<br />Kubernetes Cluster](https://docs.digitalocean.com/products/kubernetes/how-to/connect-to-cluster/)".<br /><br />To retrieve credentials for accessing a Kubernetes cluster, send a GET<br />request to `/v2/kubernetes/clusters/$K8S_CLUSTER_ID/credentials`.<br /><br />Clusters supporting token-based authentication may define an expiration by<br />passing a duration in seconds as a query parameter to<br />`/v2/kubernetes/clusters/$K8S_CLUSTER_ID/credentials?expiry_seconds=$DURATION_IN_SECONDS`.<br />If not set or 0, then the token will have a 7 day expiry. The query parameter<br />has no impact in certificate-based authentication.<br />

```sql
SELECT
*
FROM digitalocean.kubernetes.credentials
WHERE cluster_id = '{{ cluster_id }}' -- required
AND expiry_seconds = '{{ expiry_seconds }}';
```
</TabItem>
</Tabs>
