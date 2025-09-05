--- 
title: instance_sizes
hide_title: false
hide_table_of_contents: false
keywords:
  - instance_sizes
  - apps
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

Creates, updates, deletes, gets or lists an <code>instance_sizes</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>instance_sizes</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.apps.instance_sizes" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="apps_list_instance_sizes"
    values={[
        { label: 'apps_list_instance_sizes', value: 'apps_list_instance_sizes' },
        { label: 'apps_get_instance_size', value: 'apps_get_instance_size' }
    ]}
>
<TabItem value="apps_list_instance_sizes">

A JSON with key `instance_sizes`

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
<TabItem value="apps_get_instance_size">

A JSON with key `instance_size`

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
    <td><a href="#apps_list_instance_sizes"><CopyableCode code="apps_list_instance_sizes" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td></td>
    <td>List all instance sizes for `service`, `worker`, and `job` components.</td>
</tr>
<tr>
    <td><a href="#apps_get_instance_size"><CopyableCode code="apps_get_instance_size" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-slug"><code>slug</code></a></td>
    <td></td>
    <td>Retrieve information about a specific instance size for `service`, `worker`, and `job` components.</td>
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
<tr id="parameter-slug">
    <td><CopyableCode code="slug" /></td>
    <td><code>string</code></td>
    <td>The slug of the instance size (example: apps-s-1vcpu-0.5gb)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="apps_list_instance_sizes"
    values={[
        { label: 'apps_list_instance_sizes', value: 'apps_list_instance_sizes' },
        { label: 'apps_get_instance_size', value: 'apps_get_instance_size' }
    ]}
>
<TabItem value="apps_list_instance_sizes">

List all instance sizes for `service`, `worker`, and `job` components.

```sql
SELECT
*
FROM digitalocean.apps.instance_sizes;
```
</TabItem>
<TabItem value="apps_get_instance_size">

Retrieve information about a specific instance size for `service`, `worker`, and `job` components.

```sql
SELECT
*
FROM digitalocean.apps.instance_sizes
WHERE slug = '{{ slug }}' -- required;
```
</TabItem>
</Tabs>
