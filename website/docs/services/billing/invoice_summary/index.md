--- 
title: invoice_summary
hide_title: false
hide_table_of_contents: false
keywords:
  - invoice_summary
  - billing
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

Creates, updates, deletes, gets or lists an <code>invoice_summary</code> resource.

## Overview
<table><tbody>
<tr><td><b>Name</b></td><td><code>invoice_summary</code></td></tr>
<tr><td><b>Type</b></td><td>Resource</td></tr>
<tr><td><b>Id</b></td><td><CopyableCode code="digitalocean.billing.invoice_summary" /></td></tr>
</tbody></table>

## Fields

The following fields are returned by `SELECT` queries:

<Tabs
    defaultValue="invoices_get_summary_by_uuid"
    values={[
        { label: 'invoices_get_summary_by_uuid', value: 'invoices_get_summary_by_uuid' }
    ]}
>
<TabItem value="invoices_get_summary_by_uuid">

To retrieve a summary for an invoice, send a GET request to  `/v2/customers/my/invoices/$INVOICE_UUID/summary`.

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
    <td><a href="#invoices_get_summary_by_uuid"><CopyableCode code="invoices_get_summary_by_uuid" /></a></td>
    <td><CopyableCode code="select" /></td>
    <td><a href="#parameter-invoice_uuid"><code>invoice_uuid</code></a></td>
    <td></td>
    <td>To retrieve a summary for an invoice, send a GET request to `/v2/customers/my/invoices/$INVOICE_UUID/summary`.</td>
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
<tr id="parameter-invoice_uuid">
    <td><CopyableCode code="invoice_uuid" /></td>
    <td><code>string</code></td>
    <td>UUID of the invoice (example: 22737513-0ea7-4206-8ceb-98a575af7681)</td>
</tr>
</tbody>
</table>

## `SELECT` examples

<Tabs
    defaultValue="invoices_get_summary_by_uuid"
    values={[
        { label: 'invoices_get_summary_by_uuid', value: 'invoices_get_summary_by_uuid' }
    ]}
>
<TabItem value="invoices_get_summary_by_uuid">

To retrieve a summary for an invoice, send a GET request to `/v2/customers/my/invoices/$INVOICE_UUID/summary`.

```sql
SELECT
*
FROM digitalocean.billing.invoice_summary
WHERE invoice_uuid = '{{ invoice_uuid }}' -- required;
```
</TabItem>
</Tabs>
