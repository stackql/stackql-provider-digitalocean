--- 
title: users
hide_title: false
hide_table_of_contents: false
keywords:
  - users
  - databases
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

Creates, updates, deletes, gets or lists a <code>users</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>users</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.databases.users" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="databases_list_users"
    values={[
        { label: 'databases_list_users', value: 'databases_list_users' },
        { label: 'databases_get_user', value: 'databases_get_user' }
    ]}
>
<TabItem value="databases_list_users">

A JSON object with a key of `users`.

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
<TabItem value="databases_get_user">

A JSON object with a key of `user`.

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
    <td><a href="#databases_list_users"><CopyableCode code="databases_list_users" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a></td>
    <td></td>
    <td>To list all of the users for your database cluster, send a GET request to<br />`/v2/databases/$DATABASE_ID/users`.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />The result will be a JSON object with a `users` key. This will be set to an array<br />of database user objects, each of which will contain the standard database user attributes.<br />User passwords will not show without the `database:view_credentials` scope.<br /><br />For MySQL clusters, additional options will be contained in the mysql_settings object.<br /><br />For MongoDB clusters, additional information will be contained in the mongo_user_settings object<br /></td>
</tr>
<tr>
    <td><a href="#databases_get_user"><CopyableCode code="databases_get_user" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a>, <a href="#parameter-username"><code>username</code></a></td>
    <td></td>
    <td>To show information about an existing database user, send a GET request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME`.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />The response will be a JSON object with a `user` key. This will be set to an object<br />containing the standard database user attributes. The user's password will not show<br />up unless the `database:view_credentials` scope is present.<br /><br />For MySQL clusters, additional options will be contained in the `mysql_settings`<br />object.<br /><br />For Kafka clusters, additional options will be contained in the `settings` object.<br /><br />For MongoDB clusters, additional information will be contained in the mongo_user_settings object<br /></td>
</tr>
<tr>
    <td><a href="#databases_add_user"><CopyableCode code="databases_add_user" /></a></td>
    <td><CopyableCode code="insert" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a>, <a href="#parameter-data__name"><code>data__name</code></a></td>
    <td></td>
    <td>To add a new database user, send a POST request to `/v2/databases/$DATABASE_ID/users`<br />with the desired username.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />When adding a user to a MySQL cluster, additional options can be configured in the<br />`mysql_settings` object.<br /><br />When adding a user to a Kafka cluster, additional options can be configured in<br />the `settings` object.<br /><br /> When adding a user to a MongoDB cluster, additional options can be configured in<br />the `settings.mongo_user_settings` object.<br /><br />The response will be a JSON object with a key called `user`. The value of this will be an<br />object that contains the standard attributes associated with a database user including<br />its randomly generated password.<br /></td>
</tr>
<tr>
    <td><a href="#databases_update_user"><CopyableCode code="databases_update_user" /></a></td>
    <td><CopyableCode code="replace" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a>, <a href="#parameter-username"><code>username</code></a>, <a href="#parameter-data__settings"><code>data__settings</code></a></td>
    <td></td>
    <td>To update an existing database user, send a PUT request to `/v2/databases/$DATABASE_ID/users/$USERNAME`<br />with the desired settings.<br /><br />**Note**: only `settings` can be updated via this type of request. If you wish to change the name of a user,<br />you must recreate a new user.<br /><br />The response will be a JSON object with a key called `user`. The value of this will be an<br />object that contains the name of the update database user, along with the `settings` object that<br />has been updated.<br /></td>
</tr>
<tr>
    <td><a href="#databases_delete_user"><CopyableCode code="databases_delete_user" /></a></td>
    <td><CopyableCode code="delete" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a>, <a href="#parameter-username"><code>username</code></a></td>
    <td></td>
    <td>To remove a specific database user, send a DELETE request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME`.<br /><br />A status of 204 will be given. This indicates that the request was processed<br />successfully, but that no response body is needed.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /></td>
</tr>
<tr>
    <td><a href="#databases_reset_auth"><CopyableCode code="databases_reset_auth" /></a></td>
    <td><CopyableCode code="exec" /></td>
    <td><a href="#parameter-database_cluster_uuid"><code>database_cluster_uuid</code></a>, <a href="#parameter-username"><code>username</code></a></td>
    <td></td>
    <td>To reset the password for a database user, send a POST request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME/reset_auth`.<br /><br />For `mysql` databases, the authentication method can be specifying by<br />including a key in the JSON body called `mysql_settings` with the `auth_plugin`<br />value specified.<br /><br />The response will be a JSON object with a `user` key. This will be set to an<br />object containing the standard database user attributes.<br /></td>
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
<tr id="parameter-database_cluster_uuid">
    <td><CopyableCode code="database_cluster_uuid" /></td>
    <td><code>string (uuid)</code></td>
    <td>A unique identifier for a database cluster. (example: 9cc10173-e9ea-4176-9dbc-a4cee4c4ff30)</td>
</tr>
<tr id="parameter-username">
    <td><CopyableCode code="username" /></td>
    <td><code>string</code></td>
    <td>The name of the database user. (example: app-01)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="databases_list_users"
    values={[
        { label: 'databases_list_users', value: 'databases_list_users' },
        { label: 'databases_get_user', value: 'databases_get_user' }
    ]}
>
<TabItem value="databases_list_users">

To list all of the users for your database cluster, send a GET request to<br />`/v2/databases/$DATABASE_ID/users`.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />The result will be a JSON object with a `users` key. This will be set to an array<br />of database user objects, each of which will contain the standard database user attributes.<br />User passwords will not show without the `database:view_credentials` scope.<br /><br />For MySQL clusters, additional options will be contained in the mysql_settings object.<br /><br />For MongoDB clusters, additional information will be contained in the mongo_user_settings object<br />

```sql
SELECT
*
FROM digitalocean.databases.users
WHERE database_cluster_uuid = '{{ database_cluster_uuid }}' -- required;
```
</TabItem>
<TabItem value="databases_get_user">

To show information about an existing database user, send a GET request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME`.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />The response will be a JSON object with a `user` key. This will be set to an object<br />containing the standard database user attributes. The user's password will not show<br />up unless the `database:view_credentials` scope is present.<br /><br />For MySQL clusters, additional options will be contained in the `mysql_settings`<br />object.<br /><br />For Kafka clusters, additional options will be contained in the `settings` object.<br /><br />For MongoDB clusters, additional information will be contained in the mongo_user_settings object<br />

```sql
SELECT
*
FROM digitalocean.databases.users
WHERE database_cluster_uuid = '{{ database_cluster_uuid }}' -- required
AND username = '{{ username }}' -- required;
```
</TabItem>
</Tabs>


## `INSERT` examples

<Tabs
    defaultValue="databases_add_user"
    values={[
        { label: 'databases_add_user', value: 'databases_add_user' },
        { label: 'Manifest', value: 'manifest' }
    ]}
>
<TabItem value="databases_add_user">

To add a new database user, send a POST request to `/v2/databases/$DATABASE_ID/users`<br />with the desired username.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br /><br />When adding a user to a MySQL cluster, additional options can be configured in the<br />`mysql_settings` object.<br /><br />When adding a user to a Kafka cluster, additional options can be configured in<br />the `settings` object.<br /><br /> When adding a user to a MongoDB cluster, additional options can be configured in<br />the `settings.mongo_user_settings` object.<br /><br />The response will be a JSON object with a key called `user`. The value of this will be an<br />object that contains the standard attributes associated with a database user including<br />its randomly generated password.<br />

```sql
INSERT INTO digitalocean.databases.users (
data__name,
data__mysql_settings,
data__settings,
data__readonly,
database_cluster_uuid
)
SELECT 
'{{ name }}' --required,
'{{ mysql_settings }}',
'{{ settings }}',
{{ readonly }},
'{{ database_cluster_uuid }}'
;
```
</TabItem>
<TabItem value="manifest">

```yaml
# Description fields are for documentation purposes
- name: users
  props:
    - name: database_cluster_uuid
      value: string (uuid)
      description: Required parameter for the users resource.
    - name: name
      value: string
      description: >
        The name of a database user.
        
    - name: mysql_settings
      value: object
    - name: settings
      value: object
    - name: readonly
      value: boolean
      description: >
        (To be deprecated: use settings.mongo_user_settings.role instead for access controls to MongoDB databases). 
For MongoDB clusters, set to `true` to create a read-only user.
This option is not currently supported for other database engines.
           

```
</TabItem>
</Tabs>


## `REPLACE` examples

<Tabs
    defaultValue="databases_update_user"
    values={[
        { label: 'databases_update_user', value: 'databases_update_user' }
    ]}
>
<TabItem value="databases_update_user">

To update an existing database user, send a PUT request to `/v2/databases/$DATABASE_ID/users/$USERNAME`<br />with the desired settings.<br /><br />**Note**: only `settings` can be updated via this type of request. If you wish to change the name of a user,<br />you must recreate a new user.<br /><br />The response will be a JSON object with a key called `user`. The value of this will be an<br />object that contains the name of the update database user, along with the `settings` object that<br />has been updated.<br />

```sql
REPLACE digitalocean.databases.users
SET 
data__settings = '{{ settings }}'
WHERE 
database_cluster_uuid = '{{ database_cluster_uuid }}' --required
AND username = '{{ username }}' --required
AND data__settings = '{{ settings }}' --required;
```
</TabItem>
</Tabs>


## `DELETE` examples

<Tabs
    defaultValue="databases_delete_user"
    values={[
        { label: 'databases_delete_user', value: 'databases_delete_user' }
    ]}
>
<TabItem value="databases_delete_user">

To remove a specific database user, send a DELETE request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME`.<br /><br />A status of 204 will be given. This indicates that the request was processed<br />successfully, but that no response body is needed.<br /><br />Note: User management is not supported for Caching or Valkey clusters.<br />

```sql
DELETE FROM digitalocean.databases.users
WHERE database_cluster_uuid = '{{ database_cluster_uuid }}' --required
AND username = '{{ username }}' --required;
```
</TabItem>
</Tabs>


## Lifecycle Methods

<Tabs
    defaultValue="databases_reset_auth"
    values={[
        { label: 'databases_reset_auth', value: 'databases_reset_auth' }
    ]}
>
<TabItem value="databases_reset_auth">

To reset the password for a database user, send a POST request to<br />`/v2/databases/$DATABASE_ID/users/$USERNAME/reset_auth`.<br /><br />For `mysql` databases, the authentication method can be specifying by<br />including a key in the JSON body called `mysql_settings` with the `auth_plugin`<br />value specified.<br /><br />The response will be a JSON object with a `user` key. This will be set to an<br />object containing the standard database user attributes.<br />

```sql
EXEC digitalocean.databases.users.databases_reset_auth 
@database_cluster_uuid='{{ database_cluster_uuid }}' --required, 
@username='{{ username }}' --required 
@@json=
'{
"mysql_settings": "{{ mysql_settings }}"
}';
```
</TabItem>
</Tabs>
