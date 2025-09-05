--- 
title: load_balancers
hide_title: false
hide_table_of_contents: false
keywords:
  - load_balancers
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

Creates, updates, deletes, gets or lists a <code>load_balancers</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>load_balancers</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.compute.load_balancers" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="load_balancers_list"
    values={[
        { label: 'load_balancers_list', value: 'load_balancers_list' },
        { label: 'load_balancers_get', value: 'load_balancers_get' }
    ]}
>
<TabItem value="load_balancers_list">

A JSON object with a key of `load_balancers`. This will be set to an array of objects, each of which will contain the standard load balancer attributes.

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
<TabItem value="load_balancers_get">

The response will be a JSON object with a key called `load_balancer`. The<br />value of this will be an object that contains the standard attributes<br />associated with a load balancer<br />

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
    <td><a href="#load_balancers_list"><CopyableCode code="load_balancers_list" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td><a href="#parameter-per_page"><code>per_page</code></a>, <a href="#parameter-page"><code>page</code></a></td>
    <td>To list all of the load balancer instances on your account, send a GET request<br />to `/v2/load_balancers`.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_get"><CopyableCode code="load_balancers_get" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a></td>
    <td></td>
    <td>To show information about a load balancer instance, send a GET request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_create"><CopyableCode code="load_balancers_create" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td></td>
    <td></td>
    <td>To create a new load balancer instance, send a POST request to<br />`/v2/load_balancers`.<br /><br />You can specify the Droplets that will sit behind the load balancer using one<br />of two methods:<br /><br />* Set `droplet_ids` to a list of specific Droplet IDs.<br />* Set `tag` to the name of a tag. All Droplets with this tag applied will be<br />  assigned to the load balancer. Additional Droplets will be automatically<br />  assigned as they are tagged.<br /><br />These methods are mutually exclusive.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_update"><CopyableCode code="load_balancers_update" /></a></td>
    <td><CopyableCode code="replace" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a></td>
    <td></td>
    <td>To update a load balancer's settings, send a PUT request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`. The request should contain a full<br />representation of the load balancer including existing attributes. It may<br />contain _one of_ the `droplets_ids` or `tag` attributes as they are mutually<br />exclusive. **Note that any attribute that is not provided will be reset to its<br />default value.**<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_delete"><CopyableCode code="load_balancers_delete" /></a></td>
    <td><CopyableCode code="delete" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a></td>
    <td></td>
    <td>To delete a load balancer instance, disassociating any Droplets assigned to it<br />and removing it from your account, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_delete_cache"><CopyableCode code="load_balancers_delete_cache" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a></td>
    <td></td>
    <td>To delete a Global load balancer CDN cache, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/cache`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_add_droplets"><CopyableCode code="load_balancers_add_droplets" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a>, <a href="#parameter-droplet_ids"><code>droplet_ids</code></a></td>
    <td></td>
    <td>To assign a Droplet to a load balancer instance, send a POST request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/droplets`. In the body of the request,<br />there should be a `droplet_ids` attribute containing a list of Droplet IDs.<br />Individual Droplets can not be added to a load balancer configured with a<br />Droplet tag. Attempting to do so will result in a "422 Unprocessable Entity"<br />response from the API.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_remove_droplets"><CopyableCode code="load_balancers_remove_droplets" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a>, <a href="#parameter-droplet_ids"><code>droplet_ids</code></a></td>
    <td></td>
    <td>To remove a Droplet from a load balancer instance, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/droplets`. In the body of the request,<br />there should be a `droplet_ids` attribute containing a list of Droplet IDs.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_add_forwarding_rules"><CopyableCode code="load_balancers_add_forwarding_rules" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a>, <a href="#parameter-forwarding_rules"><code>forwarding_rules</code></a></td>
    <td></td>
    <td>To add an additional forwarding rule to a load balancer instance, send a POST<br />request to `/v2/load_balancers/$LOAD_BALANCER_ID/forwarding_rules`. In the body<br />of the request, there should be a `forwarding_rules` attribute containing an<br />array of rules to be added.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br /></td>
</tr>
<tr>
    <td><a href="#load_balancers_remove_forwarding_rules"><CopyableCode code="load_balancers_remove_forwarding_rules" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-lb_id"><code>lb_id</code></a>, <a href="#parameter-forwarding_rules"><code>forwarding_rules</code></a></td>
    <td></td>
    <td>To remove forwarding rules from a load balancer instance, send a DELETE<br />request to `/v2/load_balancers/$LOAD_BALANCER_ID/forwarding_rules`. In the<br />body of the request, there should be a `forwarding_rules` attribute containing<br />an array of rules to be removed.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br /></td>
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
<tr id="parameter-lb_id">
    <td><CopyableCode code="lb_id" /></td>
    <td><code>string</code></td>
    <td>A unique identifier for a load balancer. (example: 4de7ac8b-495b-4884-9a69-1050c6793cd6)</td>
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
    defaultValue="load_balancers_list"
    values={[
        { label: 'load_balancers_list', value: 'load_balancers_list' },
        { label: 'load_balancers_get', value: 'load_balancers_get' }
    ]}
>
<TabItem value="load_balancers_list">

To list all of the load balancer instances on your account, send a GET request<br />to `/v2/load_balancers`.<br />

```sql
SELECT
*
FROM digitalocean.compute.load_balancers
WHERE per_page = '{{ per_page }}'
AND page = '{{ page }}';
```
</TabItem>
<TabItem value="load_balancers_get">

To show information about a load balancer instance, send a GET request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`.<br />

```sql
SELECT
*
FROM digitalocean.compute.load_balancers
WHERE lb_id = '{{ lb_id }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="load_balancers_create"
    values={[
        { label: 'load_balancers_create', value: 'load_balancers_create' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="load_balancers_create">

To create a new load balancer instance, send a POST request to<br />`/v2/load_balancers`.<br /><br />You can specify the Droplets that will sit behind the load balancer using one<br />of two methods:<br /><br />* Set `droplet_ids` to a list of specific Droplet IDs.<br />* Set `tag` to the name of a tag. All Droplets with this tag applied will be<br />  assigned to the load balancer. Additional Droplets will be automatically<br />  assigned as they are tagged.<br /><br />These methods are mutually exclusive.<br />

```sql
INSERT INTO digitalocean.compute.load_balancers (

)
SELECT 

;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: load_balancers
  props:
```
</TabItem>
</Tabs>


## `REPLACE` examples

<Tabs
    defaultValue="load_balancers_update"
    values={[
        { label: 'load_balancers_update', value: 'load_balancers_update' }
    ]}
>
<TabItem value="load_balancers_update">

To update a load balancer's settings, send a PUT request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`. The request should contain a full<br />representation of the load balancer including existing attributes. It may<br />contain _one of_ the `droplets_ids` or `tag` attributes as they are mutually<br />exclusive. **Note that any attribute that is not provided will be reset to its<br />default value.**<br />

```sql
REPLACE digitalocean.compute.load_balancers
SET 
-- No updatable properties
WHERE 
lb_id = '{{ lb_id }}' --required;
```
</TabItem>
</Tabs>


## `DELETE` examples

<Tabs
    defaultValue="load_balancers_delete"
    values={[
        { label: 'load_balancers_delete', value: 'load_balancers_delete' }
    ]}
>
<TabItem value="load_balancers_delete">

To delete a load balancer instance, disassociating any Droplets assigned to it<br />and removing it from your account, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br />

```sql
DELETE FROM digitalocean.compute.load_balancers
WHERE lb_id = '{{ lb_id }}' --required;
```
</TabItem>
</Tabs>


## Lifecycle Methods

<Tabs
    defaultValue="load_balancers_delete_cache"
    values={[
        { label: 'load_balancers_delete_cache', value: 'load_balancers_delete_cache' },
        { label: 'load_balancers_add_droplets', value: 'load_balancers_add_droplets' },
        { label: 'load_balancers_remove_droplets', value: 'load_balancers_remove_droplets' },
        { label: 'load_balancers_add_forwarding_rules', value: 'load_balancers_add_forwarding_rules' },
        { label: 'load_balancers_remove_forwarding_rules', value: 'load_balancers_remove_forwarding_rules' }
    ]}
>
<TabItem value="load_balancers_delete_cache">

To delete a Global load balancer CDN cache, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/cache`.<br /><br />A successful request will receive a 204 status code with no body in response.<br />This indicates that the request was processed successfully.<br />

```sql
EXEC digitalocean.compute.load_balancers.load_balancers_delete_cache 
@lb_id='{{ lb_id }}' --required;
```
</TabItem>
<TabItem value="load_balancers_add_droplets">

To assign a Droplet to a load balancer instance, send a POST request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/droplets`. In the body of the request,<br />there should be a `droplet_ids` attribute containing a list of Droplet IDs.<br />Individual Droplets can not be added to a load balancer configured with a<br />Droplet tag. Attempting to do so will result in a "422 Unprocessable Entity"<br />response from the API.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br />

```sql
EXEC digitalocean.compute.load_balancers.load_balancers_add_droplets 
@lb_id='{{ lb_id }}' --required 
@@json=
'{
"droplet_ids": "{{ droplet_ids }}"
}';
```
</TabItem>
<TabItem value="load_balancers_remove_droplets">

To remove a Droplet from a load balancer instance, send a DELETE request to<br />`/v2/load_balancers/$LOAD_BALANCER_ID/droplets`. In the body of the request,<br />there should be a `droplet_ids` attribute containing a list of Droplet IDs.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br />

```sql
EXEC digitalocean.compute.load_balancers.load_balancers_remove_droplets 
@lb_id='{{ lb_id }}' --required 
@@json=
'{
"droplet_ids": "{{ droplet_ids }}"
}';
```
</TabItem>
<TabItem value="load_balancers_add_forwarding_rules">

To add an additional forwarding rule to a load balancer instance, send a POST<br />request to `/v2/load_balancers/$LOAD_BALANCER_ID/forwarding_rules`. In the body<br />of the request, there should be a `forwarding_rules` attribute containing an<br />array of rules to be added.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br />

```sql
EXEC digitalocean.compute.load_balancers.load_balancers_add_forwarding_rules 
@lb_id='{{ lb_id }}' --required 
@@json=
'{
"forwarding_rules": "{{ forwarding_rules }}"
}';
```
</TabItem>
<TabItem value="load_balancers_remove_forwarding_rules">

To remove forwarding rules from a load balancer instance, send a DELETE<br />request to `/v2/load_balancers/$LOAD_BALANCER_ID/forwarding_rules`. In the<br />body of the request, there should be a `forwarding_rules` attribute containing<br />an array of rules to be removed.<br /><br />No response body will be sent back, but the response code will indicate<br />success. Specifically, the response code will be a 204, which means that the<br />action was successful with no returned body data.<br />

```sql
EXEC digitalocean.compute.load_balancers.load_balancers_remove_forwarding_rules 
@lb_id='{{ lb_id }}' --required 
@@json=
'{
"forwarding_rules": "{{ forwarding_rules }}"
}';
```
</TabItem>
</Tabs>
