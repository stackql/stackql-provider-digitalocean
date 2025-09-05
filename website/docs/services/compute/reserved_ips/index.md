--- 
title: reserved_ips
hide_title: false
hide_table_of_contents: false
keywords:
  - reserved_ips
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

Creates, updates, deletes, gets or lists a <code>reserved_ips</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>reserved_ips</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.compute.reserved_ips" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="reserved_ips_list"
    values={[
        { label: 'reserved_ips_list', value: 'reserved_ips_list' },
        { label: 'reserved_ips_get', value: 'reserved_ips_get' }
    ]}
>
<TabItem value="reserved_ips_list">

The response will be a JSON object with a key called `reserved_ips`. This will be set to an array of reserved IP objects, each of which will contain the standard reserved IP attributes

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
<TabItem value="reserved_ips_get">

The response will be a JSON object with a key called `reserved_ip`. The value of this will be an object that contains the standard attributes associated with a reserved IP.

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
    <td><a href="#reserved_ips_list"><CopyableCode code="reserved_ips_list" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td><a href="#parameter-per_page"><code>per_page</code></a>, <a href="#parameter-page"><code>page</code></a></td>
    <td>To list all of the reserved IPs available on your account, send a GET request to `/v2/reserved_ips`.</td>
</tr>
<tr>
    <td><a href="#reserved_ips_get"><CopyableCode code="reserved_ips_get" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-reserved_ip"><code>reserved_ip</code></a></td>
    <td></td>
    <td>To show information about a reserved IP, send a GET request to `/v2/reserved_ips/$RESERVED_IP_ADDR`.</td>
</tr>
<tr>
    <td><a href="#reserved_ips_create"><CopyableCode code="reserved_ips_create" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td></td>
    <td></td>
    <td>On creation, a reserved IP must be either assigned to a Droplet or reserved to a region.<br />* To create a new reserved IP assigned to a Droplet, send a POST<br />  request to `/v2/reserved_ips` with the `droplet_id` attribute.<br /><br />* To create a new reserved IP reserved to a region, send a POST request to<br />  `/v2/reserved_ips` with the `region` attribute.<br /><br />**Note**:  In addition to the standard rate limiting, only 12 reserved IPs may be created per 60 seconds.</td>
</tr>
<tr>
    <td><a href="#reserved_ips_delete"><CopyableCode code="reserved_ips_delete" /></a></td>
    <td><CopyableCode code="delete" /></td>
    <td><a href="#parameter-reserved_ip"><code>reserved_ip</code></a></td>
    <td></td>
    <td>To delete a reserved IP and remove it from your account, send a DELETE request<br />to `/v2/reserved_ips/$RESERVED_IP_ADDR`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br /></td>
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
<tr id="parameter-reserved_ip">
    <td><CopyableCode code="reserved_ip" /></td>
    <td><code>string (ipv4)</code></td>
    <td>A reserved IP address. (example: 45.55.96.47)</td>
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
    defaultValue="reserved_ips_list"
    values={[
        { label: 'reserved_ips_list', value: 'reserved_ips_list' },
        { label: 'reserved_ips_get', value: 'reserved_ips_get' }
    ]}
>
<TabItem value="reserved_ips_list">

To list all of the reserved IPs available on your account, send a GET request to `/v2/reserved_ips`.

```sql
SELECT
*
FROM digitalocean.compute.reserved_ips
WHERE per_page = '{{ per_page }}'
AND page = '{{ page }}';
```
</TabItem>
<TabItem value="reserved_ips_get">

To show information about a reserved IP, send a GET request to `/v2/reserved_ips/$RESERVED_IP_ADDR`.

```sql
SELECT
*
FROM digitalocean.compute.reserved_ips
WHERE reserved_ip = '{{ reserved_ip }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="reserved_ips_create"
    values={[
        { label: 'reserved_ips_create', value: 'reserved_ips_create' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="reserved_ips_create">

On creation, a reserved IP must be either assigned to a Droplet or reserved to a region.<br />* To create a new reserved IP assigned to a Droplet, send a POST<br />  request to `/v2/reserved_ips` with the `droplet_id` attribute.<br /><br />* To create a new reserved IP reserved to a region, send a POST request to<br />  `/v2/reserved_ips` with the `region` attribute.<br /><br />**Note**:  In addition to the standard rate limiting, only 12 reserved IPs may be created per 60 seconds.

```sql
INSERT INTO digitalocean.compute.reserved_ips (

)
SELECT 

;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: reserved_ips
  props:
```
</TabItem>
</Tabs>


## `DELETE` examples

<Tabs
    defaultValue="reserved_ips_delete"
    values={[
        { label: 'reserved_ips_delete', value: 'reserved_ips_delete' }
    ]}
>
<TabItem value="reserved_ips_delete">

To delete a reserved IP and remove it from your account, send a DELETE request<br />to `/v2/reserved_ips/$RESERVED_IP_ADDR`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br />

```sql
DELETE FROM digitalocean.compute.reserved_ips
WHERE reserved_ip = '{{ reserved_ip }}' --required;
```
</TabItem>
</Tabs>
