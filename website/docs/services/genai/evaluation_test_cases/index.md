--- 
title: evaluation_test_cases
hide_title: false
hide_table_of_contents: false
keywords:
  - evaluation_test_cases
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

Creates, updates, deletes, gets or lists an <code>evaluation_test_cases</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>evaluation_test_cases</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.genai.evaluation_test_cases" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="genai_list_evaluation_test_cases"
    values={[
        { label: 'genai_list_evaluation_test_cases', value: 'genai_list_evaluation_test_cases' },
        { label: 'genai_list_evaluation_runs_by_test_case', value: 'genai_list_evaluation_runs_by_test_case' },
        { label: 'genai_get_evaluation_test_case', value: 'genai_get_evaluation_test_case' },
        { label: 'genai_list_evaluation_test_cases_by_workspace', value: 'genai_list_evaluation_test_cases_by_workspace' }
    ]}
>
<TabItem value="genai_list_evaluation_test_cases">

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
    <td><CopyableCode code="evaluation_test_cases" /></td>
    <td><code>array</code></td>
    <td>Alternative way of authentication for internal usage only - should not be exposed to public api</td>
</tr>
</tbody>
</table>
</TabItem>
<TabItem value="genai_list_evaluation_runs_by_test_case">

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
    <td><CopyableCode code="evaluation_runs" /></td>
    <td><code>array</code></td>
    <td>List of evaluation runs.</td>
</tr>
</tbody>
</table>
</TabItem>
<TabItem value="genai_get_evaluation_test_case">

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
    <td><CopyableCode code="evaluation_test_case" /></td>
    <td><code>object</code></td>
    <td></td>
</tr>
</tbody>
</table>
</TabItem>
<TabItem value="genai_list_evaluation_test_cases_by_workspace">

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
    <td><CopyableCode code="evaluation_test_cases" /></td>
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
    <td><a href="#genai_list_evaluation_test_cases"><CopyableCode code="genai_list_evaluation_test_cases" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td></td>
    <td>To list all evaluation test cases, send a GET request to `/v2/gen-ai/evaluation_test_cases`.</td>
</tr>
<tr>
    <td><a href="#genai_list_evaluation_runs_by_test_case"><CopyableCode code="genai_list_evaluation_runs_by_test_case" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-evaluation_test_case_uuid"><code>evaluation_test_case_uuid</code></a></td>
    <td><a href="#parameter-evaluation_test_case_version"><code>evaluation_test_case_version</code></a></td>
    <td>To list all evaluation runs by test case, send a GET request to `/v2/gen-ai/evaluation_test_cases/&#123;evaluation_test_case_uuid&#125;/evaluation_runs`.</td>
</tr>
<tr>
    <td><a href="#genai_get_evaluation_test_case"><CopyableCode code="genai_get_evaluation_test_case" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-test_case_uuid"><code>test_case_uuid</code></a></td>
    <td><a href="#parameter-evaluation_test_case_version"><code>evaluation_test_case_version</code></a></td>
    <td>To retrive information about an existing evaluation test case, send a GET request to `/v2/gen-ai/evaluation_test_case/&#123;test_case_uuid&#125;`.</td>
</tr>
<tr>
    <td><a href="#genai_list_evaluation_test_cases_by_workspace"><CopyableCode code="genai_list_evaluation_test_cases_by_workspace" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-workspace_uuid"><code>workspace_uuid</code></a></td>
    <td></td>
    <td>To list all evaluation test cases by a workspace, send a GET request to `/v2/gen-ai/workspaces/&#123;workspace_uuid&#125;/evaluation_test_cases`.</td>
</tr>
<tr>
    <td><a href="#genai_create_evaluation_test_case"><CopyableCode code="genai_create_evaluation_test_case" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td></td>
    <td></td>
    <td>To create an evaluation test-case send a POST request to `/v2/gen-ai/evaluation_test_cases`.</td>
</tr>
<tr>
    <td><a href="#genai_update_evaluation_test_case"><CopyableCode code="genai_update_evaluation_test_case" /></a></td>
    <td><CopyableCode code="replace" /></td>
    <td><a href="#parameter-test_case_uuid"><code>test_case_uuid</code></a></td>
    <td></td>
    <td>To update an evaluation test-case send a PUT request to `/v2/gen-ai/evaluation_test_cases/&#123;test_case_uuid&#125;`.</td>
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
<tr id="parameter-evaluation_test_case_uuid">
    <td><CopyableCode code="evaluation_test_case_uuid" /></td>
    <td><code>string</code></td>
    <td>Evaluation run UUID. (example: "123e4567-e89b-12d3-a456-426614174000")</td>
</tr>
<tr id="parameter-test_case_uuid">
    <td><CopyableCode code="test_case_uuid" /></td>
    <td><code>string</code></td>
    <td>Test-case UUID to update (example: "123e4567-e89b-12d3-a456-426614174000")</td>
</tr>
<tr id="parameter-workspace_uuid">
    <td><CopyableCode code="workspace_uuid" /></td>
    <td><code>string</code></td>
    <td>Workspace UUID. (example: "123e4567-e89b-12d3-a456-426614174000")</td>
</tr>
<tr id="parameter-evaluation_test_case_version">
    <td><CopyableCode code="evaluation_test_case_version" /></td>
    <td><code>integer</code></td>
    <td>Version of the test case. (example: 1)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="genai_list_evaluation_test_cases"
    values={[
        { label: 'genai_list_evaluation_test_cases', value: 'genai_list_evaluation_test_cases' },
        { label: 'genai_list_evaluation_runs_by_test_case', value: 'genai_list_evaluation_runs_by_test_case' },
        { label: 'genai_get_evaluation_test_case', value: 'genai_get_evaluation_test_case' },
        { label: 'genai_list_evaluation_test_cases_by_workspace', value: 'genai_list_evaluation_test_cases_by_workspace' }
    ]}
>
<TabItem value="genai_list_evaluation_test_cases">

To list all evaluation test cases, send a GET request to `/v2/gen-ai/evaluation_test_cases`.

```sql
SELECT
evaluation_test_cases
FROM digitalocean.genai.evaluation_test_cases;
```
</TabItem>
<TabItem value="genai_list_evaluation_runs_by_test_case">

To list all evaluation runs by test case, send a GET request to `/v2/gen-ai/evaluation_test_cases/&#123;evaluation_test_case_uuid&#125;/evaluation_runs`.

```sql
SELECT
evaluation_runs
FROM digitalocean.genai.evaluation_test_cases
WHERE evaluation_test_case_uuid = '{{ evaluation_test_case_uuid }}' -- required
AND evaluation_test_case_version = '{{ evaluation_test_case_version }}';
```
</TabItem>
<TabItem value="genai_get_evaluation_test_case">

To retrive information about an existing evaluation test case, send a GET request to `/v2/gen-ai/evaluation_test_case/&#123;test_case_uuid&#125;`.

```sql
SELECT
evaluation_test_case
FROM digitalocean.genai.evaluation_test_cases
WHERE test_case_uuid = '{{ test_case_uuid }}' -- required
AND evaluation_test_case_version = '{{ evaluation_test_case_version }}';
```
</TabItem>
<TabItem value="genai_list_evaluation_test_cases_by_workspace">

To list all evaluation test cases by a workspace, send a GET request to `/v2/gen-ai/workspaces/&#123;workspace_uuid&#125;/evaluation_test_cases`.

```sql
SELECT
evaluation_test_cases
FROM digitalocean.genai.evaluation_test_cases
WHERE workspace_uuid = '{{ workspace_uuid }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="genai_create_evaluation_test_case"
    values={[
        { label: 'genai_create_evaluation_test_case', value: 'genai_create_evaluation_test_case' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="genai_create_evaluation_test_case">

To create an evaluation test-case send a POST request to `/v2/gen-ai/evaluation_test_cases`.

```sql
INSERT INTO digitalocean.genai.evaluation_test_cases (
data__dataset_uuid,
data__description,
data__metrics,
data__name,
data__star_metric,
data__workspace_uuid
)
SELECT 
'{{ dataset_uuid }}',
'{{ description }}',
'{{ metrics }}',
'{{ name }}',
'{{ star_metric }}',
'{{ workspace_uuid }}'
RETURNING
test_case_uuid
;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: evaluation_test_cases
  props:
    - name: dataset_uuid
      value: string
      description: >
        Dataset against which the test‑case is executed.
        
    - name: description
      value: string
      description: >
        Description of the test case.
        
    - name: metrics
      value: array
      description: >
        Full metric list to use for evaluation test case.
        
    - name: name
      value: string
      description: >
        Name of the test case.
        
    - name: star_metric
      value: object
    - name: workspace_uuid
      value: string
      description: >
        The workspace uuid.
        
```
</TabItem>
</Tabs>


## `REPLACE` examples

<Tabs
    defaultValue="genai_update_evaluation_test_case"
    values={[
        { label: 'genai_update_evaluation_test_case', value: 'genai_update_evaluation_test_case' }
    ]}
>
<TabItem value="genai_update_evaluation_test_case">

To update an evaluation test-case send a PUT request to `/v2/gen-ai/evaluation_test_cases/&#123;test_case_uuid&#125;`.

```sql
REPLACE digitalocean.genai.evaluation_test_cases
SET 
data__dataset_uuid = '{{ dataset_uuid }}',
data__description = '{{ description }}',
data__metrics = '{{ metrics }}',
data__name = '{{ name }}',
data__star_metric = '{{ star_metric }}',
data__test_case_uuid = '{{ test_case_uuid }}'
WHERE 
test_case_uuid = '{{ test_case_uuid }}' --required
RETURNING
test_case_uuid,
version;
```
</TabItem>
</Tabs>
