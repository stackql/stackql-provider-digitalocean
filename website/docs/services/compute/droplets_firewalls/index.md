--- 
title: droplets_firewalls
hide_title: false
hide_table_of_contents: false
keywords:
  - droplets_firewalls
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

Creates, updates, deletes, gets or lists a <code>droplets_firewalls</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>droplets_firewalls</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.compute.droplets_firewalls" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="droplets_list_firewalls"
    values={[
        { label: 'droplets_list_firewalls', value: 'droplets_list_firewalls' }
    ]}
>
<TabItem value="droplets_list_firewalls">

A JSON object that has a key called `firewalls`.

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
    <td><a href="#droplets_list_firewalls"><CopyableCode code="droplets_list_firewalls" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-droplet_id"><code>droplet_id</code></a></td>
    <td><a href="#parameter-per_page"><code>per_page</code></a>, <a href="#parameter-page"><code>page</code></a></td>
    <td>To retrieve a list of all firewalls available to a Droplet, send a GET request<br />to `/v2/droplets/$DROPLET_ID/firewalls`<br /><br />The response will be a JSON object that has a key called `firewalls`. This will<br />be set to an array of `firewall` objects, each of which contain the standard<br />`firewall` attributes.<br /></td>
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
<tr id="parameter-page">
    <td><CopyableCode code="page" /></td>
    <td><code>integer</code></td>
    <td>Which 'page' of paginated results to return. (example: 1)</td>
</tr>
<tr id="parameter-per_page">
    <td><CopyableCode code="per_page" /></td>
    <td><code>integer</code></td>
    <td>Number of items returned per page (example: 2)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="droplets_list_firewalls"
    values={[
        { label: 'droplets_list_firewalls', value: 'droplets_list_firewalls' }
    ]}
>
<TabItem value="droplets_list_firewalls">

To retrieve a list of all firewalls available to a Droplet, send a GET request<br />to `/v2/droplets/$DROPLET_ID/firewalls`<br /><br />The response will be a JSON object that has a key called `firewalls`. This will<br />be set to an array of `firewall` objects, each of which contain the standard<br />`firewall` attributes.<br />

```sql
SELECT
*
FROM digitalocean.compute.droplets_firewalls
WHERE droplet_id = '{{ droplet_id }}' -- required
AND per_page = '{{ per_page }}'
AND page = '{{ page }}';
```
</TabItem>
</Tabs>
