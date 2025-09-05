--- 
title: ca
hide_title: false
hide_table_of_contents: false
keywords:
  - ca
  - databases
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

Creates, updates, deletes, gets or lists a <code>ca</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>ca</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.databases.ca" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="databases_get_ca"
    values={[
        { label: 'databases_get_ca', value: 'databases_get_ca' }
    ]}
>
<TabItem value="databases_get_ca">

A JSON object with a key of `ca`.

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
    <td><a href="#databases_get_ca"><CopyableCode code="databases_get_ca" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a></td>
    <td></td>
    <td>To retrieve the public certificate used to secure the connection to the database cluster send a GET request to<br />`/v2/databases/$DATABASE_ID/ca`.<br /><br />The response will be a JSON object with a `ca` key. This will be set to an object<br />containing the base64 encoding of the public key certificate.<br /></td>
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
<tr id="parameter-database_cluster_uuid">
    <td><CopyableCode code="database_cluster_uuid" /></td>
    <td><code>string (uuid)</code></td>
    <td>A unique identifier for a database cluster. (example: 9cc10173-e9ea-4176-9dbc-a4cee4c4ff30)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="databases_get_ca"
    values={[
        { label: 'databases_get_ca', value: 'databases_get_ca' }
    ]}
>
<TabItem value="databases_get_ca">

To retrieve the public certificate used to secure the connection to the database cluster send a GET request to<br />`/v2/databases/$DATABASE_ID/ca`.<br /><br />The response will be a JSON object with a `ca` key. This will be set to an object<br />containing the base64 encoding of the public key certificate.<br />

```sql
SELECT
*
FROM digitalocean.databases.ca
WHERE database_cluster_uuid = '{{ database_cluster_uuid }}' -- required;
```
</TabItem>
</Tabs>
