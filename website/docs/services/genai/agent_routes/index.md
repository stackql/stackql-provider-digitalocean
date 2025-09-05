--- 
title: agent_routes
hide_title: false
hide_table_of_contents: false
keywords:
  - agent_routes
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

Creates, updates, deletes, gets or lists an <code>agent_routes</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>agent_routes</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.genai.agent_routes" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="genai_get_agent_children"
    values={[
        { label: 'genai_get_agent_children', value: 'genai_get_agent_children' }
    ]}
>
<TabItem value="genai_get_agent_children">

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
    <td><CopyableCode code="children" /></td>
    <td><code>array</code></td>
    <td>Child agents</td>
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
    <td><a href="#genai_get_agent_children"><CopyableCode code="genai_get_agent_children" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-uuid"><code>uuid</code></a></td>
    <td></td>
    <td>To view agent routes for an agent, send a GET requtest to `/v2/gen-ai/agents/&#123;uuid&#125;/child_agents`.</td>
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
<tr id="parameter-uuid">
    <td><CopyableCode code="uuid" /></td>
    <td><code>string</code></td>
    <td>Agent id (example: "123e4567-e89b-12d3-a456-426614174000")</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="genai_get_agent_children"
    values={[
        { label: 'genai_get_agent_children', value: 'genai_get_agent_children' }
    ]}
>
<TabItem value="genai_get_agent_children">

To view agent routes for an agent, send a GET requtest to `/v2/gen-ai/agents/&#123;uuid&#125;/child_agents`.

```sql
SELECT
children
FROM digitalocean.genai.agent_routes
WHERE uuid = '{{ uuid }}' -- required;
```
</TabItem>
</Tabs>
