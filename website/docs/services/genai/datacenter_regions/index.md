--- 
title: datacenter_regions
hide_title: false
hide_table_of_contents: false
keywords:
  - datacenter_regions
  - genai
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

Creates, updates, deletes, gets or lists a <code>datacenter_regions</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>datacenter_regions</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.genai.datacenter_regions" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="genai_list_datacenter_regions"
    values={[
        { label: 'genai_list_datacenter_regions', value: 'genai_list_datacenter_regions' }
    ]}
>
<TabItem value="genai_list_datacenter_regions">

A successful response.

<table>
<thead>
    <tr>
    <th>Name</th>
    <th>Datatype</th>
    <th>Description</th>
    </tr>
</thead>
<tbody>
<tr>
    <td><CopyableCode code="regions" /></td>
    <td><code>array</code></td>
    <td>Region code</td>
</tr>
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
    <td><a href="#genai_list_datacenter_regions"><CopyableCode code="genai_list_datacenter_regions" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td><a href="#parameter-serves_inference"><code>serves_inference</code></a>, <a href="#parameter-serves_batch"><code>serves_batch</code></a></td>
    <td>To list all datacenter regions, send a GET request to `/v2/gen-ai/regions`.</td>
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
<tr id="parameter-serves_batch">
    <td><CopyableCode code="serves_batch" /></td>
    <td><code>boolean</code></td>
    <td>Include datacenters that are capable of running batch jobs. (example: true)</td>
</tr>
<tr id="parameter-serves_inference">
    <td><CopyableCode code="serves_inference" /></td>
    <td><code>boolean</code></td>
    <td>Include datacenters that serve inference. (example: true)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="genai_list_datacenter_regions"
    values={[
        { label: 'genai_list_datacenter_regions', value: 'genai_list_datacenter_regions' }
    ]}
>
<TabItem value="genai_list_datacenter_regions">

To list all datacenter regions, send a GET request to `/v2/gen-ai/regions`.

```sql
SELECT
regions
FROM digitalocean.genai.datacenter_regions
WHERE serves_inference = '{{ serves_inference }}'
AND serves_batch = '{{ serves_batch }}';
```
</TabItem>
</Tabs>
