--- 
title: droplets_neighbors
hide_title: false
hide_table_of_contents: false
keywords:
  - droplets_neighbors
  - compute
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

Creates, updates, deletes, gets or lists a <code>droplets_neighbors</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>droplets_neighbors</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.compute.droplets_neighbors" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="droplets_list_neighbors"
    values={[
        { label: 'droplets_list_neighbors', value: 'droplets_list_neighbors' }
    ]}
>
<TabItem value="droplets_list_neighbors">

A JSON object with an `droplets` key.

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
    <td><a href="#droplets_list_neighbors"><CopyableCode code="droplets_list_neighbors" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-droplet_id"><code>droplet_id</code></a></td>
    <td></td>
    <td>To retrieve a list of any "neighbors" (i.e. Droplets that are co-located on<br />the same physical hardware) for a specific Droplet, send a GET request to<br />`/v2/droplets/$DROPLET_ID/neighbors`.<br /><br />The results will be returned as a JSON object with a key of `droplets`. This<br />will be set to an array containing objects representing any other Droplets<br />that share the same physical hardware. An empty array indicates that the<br />Droplet is not co-located any other Droplets associated with your account.<br /></td>
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
<tr id="parameter-droplet_id">
    <td><CopyableCode code="droplet_id" /></td>
    <td><code>integer</code></td>
    <td>A unique identifier for a Droplet instance. (example: 3164444)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="droplets_list_neighbors"
    values={[
        { label: 'droplets_list_neighbors', value: 'droplets_list_neighbors' }
    ]}
>
<TabItem value="droplets_list_neighbors">

To retrieve a list of any "neighbors" (i.e. Droplets that are co-located on<br />the same physical hardware) for a specific Droplet, send a GET request to<br />`/v2/droplets/$DROPLET_ID/neighbors`.<br /><br />The results will be returned as a JSON object with a key of `droplets`. This<br />will be set to an array containing objects representing any other Droplets<br />that share the same physical hardware. An empty array indicates that the<br />Droplet is not co-located any other Droplets associated with your account.<br />

```sql
SELECT
*
FROM digitalocean.compute.droplets_neighbors
WHERE droplet_id = '{{ droplet_id }}' -- required;
```
</TabItem>
</Tabs>
