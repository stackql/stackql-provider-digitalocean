--- 
title: namespaces
hide_title: false
hide_table_of_contents: false
keywords:
  - namespaces
  - serverless
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

Creates, updates, deletes, gets or lists a <code>namespaces</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>namespaces</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.serverless.namespaces" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="functions_list_namespaces"
    values={[
        { label: 'functions_list_namespaces', value: 'functions_list_namespaces' },
        { label: 'functions_get_namespace', value: 'functions_get_namespace' }
    ]}
>
<TabItem value="functions_list_namespaces">

An array of JSON objects with a key called `namespaces`.  Each object represents a namespace and contains<br />the properties associated with it. 

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
<TabItem value="functions_get_namespace">

A JSON response object with a key called `namespace`. The object contains the properties associated<br />with the namespace.

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
    <td><a href="#functions_list_namespaces"><CopyableCode code="functions_list_namespaces" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td></td>
    <td>Returns a list of namespaces associated with the current user. To get all namespaces, send a GET request to `/v2/functions/namespaces`.</td>
</tr>
<tr>
    <td><a href="#functions_get_namespace"><CopyableCode code="functions_get_namespace" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-namespace_id"><code>namespace_id</code></a></td>
    <td></td>
    <td>Gets the namespace details for the given namespace UUID. To get namespace details, send a GET request to `/v2/functions/namespaces/$NAMESPACE_ID` with no parameters.</td>
</tr>
<tr>
    <td><a href="#functions_create_namespace"><CopyableCode code="functions_create_namespace" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td><a href="#parameter-data__region"><code>data__region</code></a>, <a href="#parameter-data__label"><code>data__label</code></a></td>
    <td></td>
    <td>Creates a new serverless functions namespace in the desired region and associates it with the provided label. A namespace is a collection of functions and their associated packages, triggers, and project specifications. To create a namespace, send a POST request to `/v2/functions/namespaces` with the `region` and `label` properties.</td>
</tr>
<tr>
    <td><a href="#functions_delete_namespace"><CopyableCode code="functions_delete_namespace" /></a></td>
    <td><CopyableCode code="delete" /></td>
    <td><a href="#parameter-namespace_id"><code>namespace_id</code></a></td>
    <td></td>
    <td>Deletes the given namespace.  When a namespace is deleted all assets, in the namespace are deleted, this includes packages, functions and triggers. Deleting a namespace is a destructive operation and assets in the namespace are not recoverable after deletion. Some metadata is retained, such as activations, or soft deleted for reporting purposes.<br />To delete namespace, send a DELETE request to `/v2/functions/namespaces/$NAMESPACE_ID`.<br />A successful deletion returns a 204 response.</td>
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
<tr id="parameter-namespace_id">
    <td><CopyableCode code="namespace_id" /></td>
    <td><code>string</code></td>
    <td>The ID of the namespace to be managed. (example: fn-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="functions_list_namespaces"
    values={[
        { label: 'functions_list_namespaces', value: 'functions_list_namespaces' },
        { label: 'functions_get_namespace', value: 'functions_get_namespace' }
    ]}
>
<TabItem value="functions_list_namespaces">

Returns a list of namespaces associated with the current user. To get all namespaces, send a GET request to `/v2/functions/namespaces`.

```sql
SELECT
*
FROM digitalocean.serverless.namespaces;
```
</TabItem>
<TabItem value="functions_get_namespace">

Gets the namespace details for the given namespace UUID. To get namespace details, send a GET request to `/v2/functions/namespaces/$NAMESPACE_ID` with no parameters.

```sql
SELECT
*
FROM digitalocean.serverless.namespaces
WHERE namespace_id = '{{ namespace_id }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="functions_create_namespace"
    values={[
        { label: 'functions_create_namespace', value: 'functions_create_namespace' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="functions_create_namespace">

Creates a new serverless functions namespace in the desired region and associates it with the provided label. A namespace is a collection of functions and their associated packages, triggers, and project specifications. To create a namespace, send a POST request to `/v2/functions/namespaces` with the `region` and `label` properties.

```sql
INSERT INTO digitalocean.serverless.namespaces (
data__region,
data__label
)
SELECT 
'{{ region }}' --required,
'{{ label }}' --required
;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: namespaces
  props:
    - name: region
      value: string
      description: >
        The [datacenter region](https://docs.digitalocean.com/products/platform/availability-matrix/#available-datacenters) in which to create the namespace.
        
    - name: label
      value: string
      description: >
        The namespace's unique name.
        
```
</TabItem>
</Tabs>


## `DELETE` examples

<Tabs
    defaultValue="functions_delete_namespace"
    values={[
        { label: 'functions_delete_namespace', value: 'functions_delete_namespace' }
    ]}
>
<TabItem value="functions_delete_namespace">

Deletes the given namespace.  When a namespace is deleted all assets, in the namespace are deleted, this includes packages, functions and triggers. Deleting a namespace is a destructive operation and assets in the namespace are not recoverable after deletion. Some metadata is retained, such as activations, or soft deleted for reporting purposes.<br />To delete namespace, send a DELETE request to `/v2/functions/namespaces/$NAMESPACE_ID`.<br />A successful deletion returns a 204 response.

```sql
DELETE FROM digitalocean.serverless.namespaces
WHERE namespace_id = '{{ namespace_id }}' --required;
```
</TabItem>
</Tabs>
