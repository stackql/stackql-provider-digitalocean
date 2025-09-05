--- 
title: indexing_job_data_sources
hide_title: false
hide_table_of_contents: false
keywords:
  - indexing_job_data_sources
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

Creates, updates, deletes, gets or lists an <code>indexing_job_data_sources</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>indexing_job_data_sources</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.genai.indexing_job_data_sources" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="genai_list_indexing_job_data_sources"
    values={[
        { label: 'genai_list_indexing_job_data_sources', value: 'genai_list_indexing_job_data_sources' }
    ]}
>
<TabItem value="genai_list_indexing_job_data_sources">

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
    <td><CopyableCode code="indexed_data_sources" /></td>
    <td><code>array</code></td>
    <td></td>
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
    <td><a href="#genai_list_indexing_job_data_sources"><CopyableCode code="genai_list_indexing_job_data_sources" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-indexing_job_uuid"><code>indexing_job_uuid</code></a></td>
    <td></td>
    <td>To list all datasources for an indexing job, send a GET request to `/v2/gen-ai/indexing_jobs/&#123;indexing_job_uuid&#125;/data_sources`.</td>
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
<tr id="parameter-indexing_job_uuid">
    <td><CopyableCode code="indexing_job_uuid" /></td>
    <td><code>string</code></td>
    <td>Uuid of the indexing job (example: "123e4567-e89b-12d3-a456-426614174000")</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="genai_list_indexing_job_data_sources"
    values={[
        { label: 'genai_list_indexing_job_data_sources', value: 'genai_list_indexing_job_data_sources' }
    ]}
>
<TabItem value="genai_list_indexing_job_data_sources">

To list all datasources for an indexing job, send a GET request to `/v2/gen-ai/indexing_jobs/&#123;indexing_job_uuid&#125;/data_sources`.

```sql
SELECT
indexed_data_sources
FROM digitalocean.genai.indexing_job_data_sources
WHERE indexing_job_uuid = '{{ indexing_job_uuid }}' -- required;
```
</TabItem>
</Tabs>
