--- 
title: images
hide_title: false
hide_table_of_contents: false
keywords:
  - images
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

Creates, updates, deletes, gets or lists an <code>images</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>images</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.compute.images" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="images_list"
    values={[
        { label: 'images_list', value: 'images_list' },
        { label: 'images_get', value: 'images_get' }
    ]}
>
<TabItem value="images_list">

The response will be a JSON object with a key called `images`.  This will be set to an array of image objects, each of which will contain the standard image attributes.

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
<TabItem value="images_get">

The response will be a JSON object with a key called `image`.  The value of this will be an image object containing the standard image attributes.

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
    <td><a href="#images_list"><CopyableCode code="images_list" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td></td>
    <td><a href="#parameter-type"><code>type</code></a>, <a href="#parameter-private"><code>private</code></a>, <a href="#parameter-tag_name"><code>tag_name</code></a>, <a href="#parameter-per_page"><code>per_page</code></a>, <a href="#parameter-page"><code>page</code></a></td>
    <td>To list all of the images available on your account, send a GET request to /v2/images.<br /><br />## Filtering Results<br />-----<br /><br />It's possible to request filtered results by including certain query parameters.<br /><br />**Image Type**<br /><br />Either 1-Click Application or OS Distribution images can be filtered by using the `type` query parameter.<br /><br />&gt; Important: The `type` query parameter does not directly relate to the `type` attribute.<br /><br />To retrieve only ***distribution*** images, include the `type` query parameter set to distribution, `/v2/images?type=distribution`.<br /><br />To retrieve only ***application*** images, include the `type` query parameter set to application, `/v2/images?type=application`.<br /><br />**User Images**<br /><br />To retrieve only the private images of a user, include the `private` query parameter set to true, `/v2/images?private=true`.<br /><br />**Tags**<br /><br />To list all images assigned to a specific tag, include the `tag_name` query parameter set to the name of the tag in your GET request. For example, `/v2/images?tag_name=$TAG_NAME`.<br /></td>
</tr>
<tr>
    <td><a href="#images_get"><CopyableCode code="images_get" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-image_id"><code>image_id</code></a></td>
    <td></td>
    <td>To retrieve information about an image, send a `GET` request to<br />`/v2/images/$IDENTIFIER`.<br /></td>
</tr>
<tr>
    <td><a href="#images_create_custom"><CopyableCode code="images_create_custom" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td><a href="#parameter-data__name"><code>data__name</code></a>, <a href="#parameter-data__url"><code>data__url</code></a>, <a href="#parameter-data__region"><code>data__region</code></a></td>
    <td></td>
    <td>To create a new custom image, send a POST request to /v2/images.<br />The body must contain a url attribute pointing to a Linux virtual machine<br />image to be imported into DigitalOcean.<br />The image must be in the raw, qcow2, vhdx, vdi, or vmdk format.<br />It may be compressed using gzip or bzip2 and must be smaller than 100 GB after<br /> being decompressed.<br /></td>
</tr>
<tr>
    <td><a href="#images_update"><CopyableCode code="images_update" /></a></td>
    <td><CopyableCode code="replace" /></td>
    <td><a href="#parameter-image_id"><code>image_id</code></a></td>
    <td></td>
    <td>To update an image, send a `PUT` request to `/v2/images/$IMAGE_ID`.<br />Set the `name` attribute to the new value you would like to use.<br />For custom images, the `description` and `distribution` attributes may also be updated.<br /></td>
</tr>
<tr>
    <td><a href="#images_delete"><CopyableCode code="images_delete" /></a></td>
    <td><CopyableCode code="delete" /></td>
    <td><a href="#parameter-image_id"><code>image_id</code></a></td>
    <td></td>
    <td>To delete a snapshot or custom image, send a `DELETE` request to `/v2/images/$IMAGE_ID`.<br /></td>
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
<tr id="parameter-image_id">
    <td><CopyableCode code="image_id" /></td>
    <td><code>integer</code></td>
    <td>A unique number that can be used to identify and reference a specific image. (example: 62137902)</td>
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
<tr id="parameter-private">
    <td><CopyableCode code="private" /></td>
    <td><code>boolean</code></td>
    <td>Used to filter only user images. (example: true)</td>
</tr>
<tr id="parameter-tag_name">
    <td><CopyableCode code="tag_name" /></td>
    <td><code>string</code></td>
    <td>Used to filter images by a specific tag. (example: base-image)</td>
</tr>
<tr id="parameter-type">
    <td><CopyableCode code="type" /></td>
    <td><code>string</code></td>
    <td>Filters results based on image type which can be either `application` or `distribution`. (example: distribution)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="images_list"
    values={[
        { label: 'images_list', value: 'images_list' },
        { label: 'images_get', value: 'images_get' }
    ]}
>
<TabItem value="images_list">

To list all of the images available on your account, send a GET request to /v2/images.<br /><br />## Filtering Results<br />-----<br /><br />It's possible to request filtered results by including certain query parameters.<br /><br />**Image Type**<br /><br />Either 1-Click Application or OS Distribution images can be filtered by using the `type` query parameter.<br /><br />&gt; Important: The `type` query parameter does not directly relate to the `type` attribute.<br /><br />To retrieve only ***distribution*** images, include the `type` query parameter set to distribution, `/v2/images?type=distribution`.<br /><br />To retrieve only ***application*** images, include the `type` query parameter set to application, `/v2/images?type=application`.<br /><br />**User Images**<br /><br />To retrieve only the private images of a user, include the `private` query parameter set to true, `/v2/images?private=true`.<br /><br />**Tags**<br /><br />To list all images assigned to a specific tag, include the `tag_name` query parameter set to the name of the tag in your GET request. For example, `/v2/images?tag_name=$TAG_NAME`.<br />

```sql
SELECT
*
FROM digitalocean.compute.images
WHERE type = '{{ type }}'
AND private = '{{ private }}'
AND tag_name = '{{ tag_name }}'
AND per_page = '{{ per_page }}'
AND page = '{{ page }}';
```
</TabItem>
<TabItem value="images_get">

To retrieve information about an image, send a `GET` request to<br />`/v2/images/$IDENTIFIER`.<br />

```sql
SELECT
*
FROM digitalocean.compute.images
WHERE image_id = '{{ image_id }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="images_create_custom"
    values={[
        { label: 'images_create_custom', value: 'images_create_custom' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="images_create_custom">

To create a new custom image, send a POST request to /v2/images.<br />The body must contain a url attribute pointing to a Linux virtual machine<br />image to be imported into DigitalOcean.<br />The image must be in the raw, qcow2, vhdx, vdi, or vmdk format.<br />It may be compressed using gzip or bzip2 and must be smaller than 100 GB after<br /> being decompressed.<br />

```sql
INSERT INTO digitalocean.compute.images (
data__name,
data__distribution,
data__description,
data__url,
data__region,
data__tags
)
SELECT 
'{{ name }}' --required,
'{{ distribution }}',
'{{ description }}',
'{{ url }}' --required,
'{{ region }}' --required,
'{{ tags }}'
;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: images
  props:
    - name: name
      value: string
      description: >
        The display name that has been given to an image.  This is what is shown in the control panel and is generally a descriptive title for the image in question.
        
    - name: distribution
      value: string
      description: >
        The name of a custom image's distribution. Currently, the valid values are  `Arch Linux`, `CentOS`, `CoreOS`, `Debian`, `Fedora`, `Fedora Atomic`,  `FreeBSD`, `Gentoo`, `openSUSE`, `RancherOS`, `Rocky Linux`, `Ubuntu`, and `Unknown`.  Any other value will be accepted but ignored, and `Unknown` will be used in its place.
        
      valid_values: ['Arch Linux', 'CentOS', 'CoreOS', 'Debian', 'Fedora', 'Fedora Atomic', 'FreeBSD', 'Gentoo', 'openSUSE', 'RancherOS', 'Rocky Linux', 'Ubuntu', 'Unknown']
    - name: description
      value: string
      description: >
        An optional free-form text field to describe an image.
        
    - name: url
      value: string
      description: >
        A URL from which the custom Linux virtual machine image may be retrieved.  The image it points to must be in the raw, qcow2, vhdx, vdi, or vmdk format.  It may be compressed using gzip or bzip2 and must be smaller than 100 GB after being decompressed.
        
    - name: region
      value: string
      description: >
        The slug identifier for the region where the resource will initially be  available.
        
      valid_values: ['ams1', 'ams2', 'ams3', 'blr1', 'fra1', 'lon1', 'nyc1', 'nyc2', 'nyc3', 'sfo1', 'sfo2', 'sfo3', 'sgp1', 'tor1', 'syd1']
    - name: tags
      value: array
      description: >
        A flat array of tag names as strings to be applied to the resource. Tag names may be for either existing or new tags. <br><br>Requires `tag:create` scope.
        
```
</TabItem>
</Tabs>


## `REPLACE` examples

<Tabs
    defaultValue="images_update"
    values={[
        { label: 'images_update', value: 'images_update' }
    ]}
>
<TabItem value="images_update">

To update an image, send a `PUT` request to `/v2/images/$IMAGE_ID`.<br />Set the `name` attribute to the new value you would like to use.<br />For custom images, the `description` and `distribution` attributes may also be updated.<br />

```sql
REPLACE digitalocean.compute.images
SET 
data__name = '{{ name }}',
data__distribution = '{{ distribution }}',
data__description = '{{ description }}'
WHERE 
image_id = '{{ image_id }}' --required;
```
</TabItem>
</Tabs>


## `DELETE` examples

<Tabs
    defaultValue="images_delete"
    values={[
        { label: 'images_delete', value: 'images_delete' }
    ]}
>
<TabItem value="images_delete">

To delete a snapshot or custom image, send a `DELETE` request to `/v2/images/$IMAGE_ID`.<br />

```sql
DELETE FROM digitalocean.compute.images
WHERE image_id = '{{ image_id }}' --required;
```
</TabItem>
</Tabs>
