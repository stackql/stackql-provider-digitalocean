--- 
title: defaults
hide_title: false
hide_table_of_contents: false
keywords:
  - defaults
  - projects
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

Creates, updates, deletes, gets or lists a <code>defaults</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>defaults</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.projects.defaults" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="projects_get_default"
    values={[
        { label: 'projects_get_default', value: 'projects_get_default' }
    ]}
>
<TabItem value="projects_get_default">

The response will be a JSON object with a key called `project`. The value of this will be an object with the standard project attributes

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
    <td><a href="#projects_get_default"><CopyableCode code="projects_get_default" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td></td>
    <td>To get your default project, send a GET request to `/v2/projects/default`.</td>
</tr>
<tr>
    <td><a href="#projects_patch_default"><CopyableCode code="projects_patch_default" /></a></td>
    <td><CopyableCode code="update" /></td>
    <td></td>
    <td></td>
    <td>To update only specific attributes of your default project, send a PATCH request to `/v2/projects/default`. At least one of the following attributes needs to be sent.</td>
</tr>
<tr>
    <td><a href="#projects_update_default"><CopyableCode code="projects_update_default" /></a></td>
    <td><CopyableCode code="replace" /></td>
    <td><a href="#parameter-data__name"><code>data__name</code></a>, <a href="#parameter-data__description"><code>data__description</code></a>, <a href="#parameter-data__purpose"><code>data__purpose</code></a>, <a href="#parameter-data__environment"><code>data__environment</code></a>, <a href="#parameter-data__is_default"><code>data__is_default</code></a></td>
    <td></td>
    <td>To update you default project, send a PUT request to `/v2/projects/default`. All of the following attributes must be sent.</td>
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
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="projects_get_default"
    values={[
        { label: 'projects_get_default', value: 'projects_get_default' }
    ]}
>
<TabItem value="projects_get_default">

To get your default project, send a GET request to `/v2/projects/default`.

```sql
SELECT
*
FROM digitalocean.projects.defaults;
```
</TabItem>
</Tabs>


## `UPDATE` examples

<Tabs
    defaultValue="projects_patch_default"
    values={[
        { label: 'projects_patch_default', value: 'projects_patch_default' }
    ]}
>
<TabItem value="projects_patch_default">

To update only specific attributes of your default project, send a PATCH request to `/v2/projects/default`. At least one of the following attributes needs to be sent.

```sql
UPDATE digitalocean.projects.defaults
SET 
data__name = '{{ name }}',
data__description = '{{ description }}',
data__purpose = '{{ purpose }}',
data__environment = '{{ environment }}',
data__is_default = {{ is_default }}
WHERE 
;
```
</TabItem>
</Tabs>


## `REPLACE` examples

<Tabs
    defaultValue="projects_update_default"
    values={[
        { label: 'projects_update_default', value: 'projects_update_default' }
    ]}
>
<TabItem value="projects_update_default">

To update you default project, send a PUT request to `/v2/projects/default`. All of the following attributes must be sent.

```sql
REPLACE digitalocean.projects.defaults
SET 
data__name = '{{ name }}',
data__description = '{{ description }}',
data__purpose = '{{ purpose }}',
data__environment = '{{ environment }}',
data__is_default = {{ is_default }}
WHERE 
data__name = '{{ name }}' --required
AND data__description = '{{ description }}' --required
AND data__purpose = '{{ purpose }}' --required
AND data__environment = '{{ environment }}' --required
AND data__is_default = {{ is_default }} --required;
```
</TabItem>
</Tabs>
