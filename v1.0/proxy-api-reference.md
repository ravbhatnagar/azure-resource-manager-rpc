# Proxy API Reference

- [Proxy API Reference](#proxy-api-reference) <br/>
  - [Resource Action Requests](#resource-action-requests) <br/>
    - [Request](#request) <br/>
    - [Response](#response) <br/>
  - [Subscription wide Reads and Actions] (proxy-api-reference.md#sub-wide-id) <br/>
    - [Request] (proxy-api-reference.md#sub-wide-req-id) <br/>
    - [Response] (proxy-api-reference.md#sub-wide-res-id) <br/>
  - [Exposing Available Operations (for Client discovery)] (proxy-api-reference.md#available-ops-id) <br/>
    - [Request] (proxy-api-reference.md#available-ops-req-id) <br/>
    - [Response] (proxy-api-reference.md#available-ops-res-id) <br/>
  - [Check Name Availability Requests] (proxy-api-reference.md#check-name-id) <br/>
    - [Request (for Global Uniqueness)] (proxy-api-reference.md#check-name-req-id) <br/>
    - [Request (for local uniqueness)] (proxy-api-reference.md#check-name-req-loc-id) <br/>
    - [Response] (proxy-api-reference.md#check-name-res-id) <br/>

## Proxy API reference ##

ARM will proxy requests to backing resource providers even if they are not related directly to resource management or subscription lifecycle changes.

These requests are considered to be part of the "Proxy API" and examples include: restart a VM; fetch storage account keys; or increase the capacity of a mobile service.

### Resource Action Requests ###

Actions can be performed on objects (e.g. reimage VM instance), but still need to be modeled in a consistent way across internal and external resource providers. Through this consistency, resource providers will be able to "light-up" authorization / RBAC scenarios without changing their API surface.

In order to make the "action" consistent across resource providers, the action name must be included in the URL via a specific format (which is aligned with OData).

The HTTP verb and request body will \*not\* be used in identifying the "action" being taken on the resource provider if the action name is provided.

**If no action name is provided, the HTTP Verb (e.g. GET / PUT) will be used as the action name.**

#### Request ###

| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}/{actionName}?api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

Examples of action names include: "restartVM" or "listStorageKeys".

**Request Body**

    {
    "resourceDefinedProperty": "Resource defined value";
    }

All parameters for the action request should be contained in the request body – and not in the URL. This matches the OData and Azure REST guidelines and will avoid impacting the authZ checks.

#### Response ###

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the action completed successfully. 202 (Accepted) can be returned to indicate that the action will complete asynchronously.

If the resource group or a relevant resource does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will be specific to the resource provider and the action, but it \*must\* adhere to the REST CEC guidelines and be JSON by default.

### Subscription Wide Reads and Actions ###

This applies to GETs and POSTs where some data needs to be exposed in a read-only fashion across a subscription or tenant. The Resource Provider contract allows for this functionality but recommends caution when exposing it (since it requires a &quot;global&quot; endpoint for the RP &amp; does not support regional routing).

Examples include: available platform images for a subscription; available locations for their offer type; quotas or restrictions imposed on their subscription.

**Please review all instances where this API is used with the current owners of the RP API document. Manageable entities should \*never\* be updated at this level.**

#### Request (Subscription wide operations) ####

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{resourceType}?api-version={api-version} |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{actionName}?api-version={api-version} |

#### Request (Tenant wide operations) ####
| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/providers/{resourceProviderNamespace}/{actionName}?api-version={api-version} |

**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[{-preview} or  {-alpha}or{-beta}or{-rc}or{-privatepreview}]. |
| resourceProviderNamespace| The resource provider namespace can only be ASCII alphanumeric characters and the "." character. |
| resourceType| The type of the resource – the resource providers declare the resource types they support at the time of registering with Azure. The resourceType should follow the lowerCamelCase convention and be plural (e.g. virtualMachines, resourceGroups, jobCollections, virtualNetworks). The resource type can only be ASCII alphanumeric characters.|

**Request Headers**

Only headers common to all requests.

**Request Body**

Controlled by the resource provider (e.g. GETs should have no body; POSTs can have a body as part of the action).

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body if it applies.

**Status Code**

The resource provider should return 200 (OK) to indicate that the action completed successfully. 202 (Accepted) can be returned to indicate that the action will complete asynchronously.

If the Provider does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will be specific to the resource provider and the URL, but it \*must\* adhere to the REST CEC guidelines and be JSON by default.

### Exposing Available Operations (for client discovery) ###

As part of the management experience, clients (e.g. portal / CLI / powershell) need an ability to discover the available operations for a particular resource provider. The set of operations should include both registered and non-registered types (e.g. Virtual Machines and Disks).

This API is unique in that it is not scoped to a subscription – it is considered to be tenant-wide and should \*not\* vary based on particular subscriptions.

#### Request ####

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/providers/{resourceProviderNamespace}/operations?api-version={api-version} |

**Arguments**

| Argument | Description |
| --- | --- |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

#### Response ####

    {
    "value": [
    {
      "name": "{resourceProviderNamespace}/{resourceType}/{read|write|delete|action}",
      "display": {
        "provider": "{Name of the provider for display purposes}",
        "resource": "{Name of the resource type for display purposes}",
        "operation": "{Name of the operation for display purposes}",
        "description": "{Description of the operation for display purposes}"
      },

      "origin": "user|system|user,system",
      "properties": { }
    },

    {
      "name": "{resourceProviderNamespace}/{resourceType}/{read|write|delete|action}",
      "display": {
        "provider": "{Name of the provider for display purposes}",
        "resource": "{Name of the resource type for display purposes}",
        "operation": "{Name of the operation for display purposes}",
        "description": "{Description of the operation for display purposes}"
      },
      "origin": "user|system|user,system",
      "properties": { }
    },
    ],
    "nextLink": "{originalRequestUrl}?$skipToken={opaqueString}"
    }

| Element name | Description |
| --- | --- |
| name | **Required**.The name of the operation being performed on this particular object. It should match the action name that appears in RBAC / the event service.  Examples of operations include:- <ul><li>Microsoft.Compute/virtualMachines/capture/action</li> <li>Microsoft.Compute/virtualMachines/restart/action</li> <li>Microsoft.Compute/virtualMachines/write</li> <li>Microsoft.Compute/virtualMachines/read</li> <li>Microsoft.Compute/virtualMachines/delete</li></ul> Each action should include, in order: <ul> <li> Resource Provider Namespace</li> <li> Type hierarchy for which the action applies (e.g. server/databases for a SQL Azure database)</li> <li>If an &quot;action,&quot; the custom action name (e.g. capture / restart / etc.)</li> <li>Read, Write, Action or Delete indicating which type applies.</li> <ul><li>If it is a PUT/PATCH on a collection or named value, Write should be used.</li> <li> If it is a GET, Read should be used.</li> <li>If it is a DELETE, Delete should be used.</li> <li>If it is a POST, Action should be used.</li></ul> </ul> As an example: <ul> <li>Microsoft.Compute/virtualMachines/extensions/capture/action</li> <ul> <li>Namespace: Microsoft.Compute</li> <li>Resource Type: virtualMachines/extensions</li> <li>Custom action name: capture</li> <li>Action verb: action (because it is a POST)</li></ul> <li>Microsoft.Compute/virtualMachines/extensions/write</li><ul><li>Namespace: Microsoft.Compute</li> <li>Resource Type: virtualMachines/extensions</li> <li>Custom action name: \*none\*</li> <li>Action verb: write (because it is a PUT/PATCH)</li> </ul> </ul> As a note: all resource providers would need to include the "{Resource Provider Namespace}/register/action" operation in their response. This API is used to register for their service, and should include details about the operation (e.g. a localized name for the resource provider + any special considerations like PII release). Example values can be seen below:<ul> <li>Resource: "Storage Resource Provider" </li> <li>Operation: "Registers the Storage Resource Provider"</li> <li>Description: "Registers the subscription for the storage resource provider and enables the creation of storage accounts." </li> </ul> |
| display | **Required.** Contains the localized display information for this particular operation / action. These value will be used by several clients for (1) custom role definitions for RBAC; (2) complex query filters for the event service; and (3) audit history / records for management operations. |
| display.provider | **Required**.The localized friendly form of the resource provider name – it is expected to also include the publisher/company responsible. It should use Title Casing and begin with "Microsoft" for 1st party services.  e.g. "Microsoft Monitoring Insights" or "Microsoft Compute." |
| display.resource | **Required**.The localized friendly form of the resource type related to this action/operation – it should match the public documentation for the resource provider. It should use Title Casing – for examples, please refer to the "name" section.<br/>  **This value should be unique for a particular URL type** (e.g. nested types should \*not\* reuse their parent&#39;s display.resource field). <br/> e.g. "Virtual Machines" or "Scheduler Job Collections", or "Virtual Machine VM Sizes" or "Scheduler Jobs" |
| display.operation  | **Required**.The localized friendly name for the operation, as it should be shown to the user. It should be concise (to fit in drop downs) but clear (i.e. self-documenting). It should use Title Casing and include the entity/resource to which it applies.<br/>  Prescriptive guidance: <br/> Read {Resource Type Name} <br/>Create or Update {Resource Type Name} <br/>Delete {Resource Type Name} <br/> <User Friendly Action Name> {Resource Type Name} <br/> As examples:Read Virtual Machine <br/>Create or Update Virtual Machine <br/>Delete Virtual Machine <br/> Restart Virtual Machine  |
| display.description | **Required**.The localized friendly description for the operation, as it should be shown to the user. It should be thorough, yet concise – it will be used in tool tips and detailed views.<br/>  Prescriptive guidance for resources: <br/>Read any <display.resource> <br/>Create or Update any <display.resource> <br/>Delete any <display.resource> <br/> <User Friendly Action Name> any <display.resources>  |
| origin | **Optional.** The intended executor of the operation; governs the display of the operation in the RBAC UX and the audit logs UX.<br/> Default value is "user,system"<br/> Details below |
| properties | **Reserved for future use.  Optional.** |

#### Origin details ####

<table>
<th>origin</th>
<th>initiator</th>
<th>Appears in RBAC UX </th>
<th>Appears in Audit Logs UX </th>
<tr><td>user</td><td>end user/service principal</td><td>Yes</td><td>Yes</td></tr>
<tr><td>system</td><td>svc backend</td><td>No</td><td>Yes</td></tr>
<tr><td>user, system</td><td>end user/service principal/ svc backend</td><td>Yes</td><td>Yes</td></tr>
</table> 

### Check Name Availability Requests ###

Many resource providers have resource name uniqueness requirements – usually requiring global or local uniqueness.  The following APIs provide a common pattern for verifying name availability.

#### Request (for global uniqueness) ####

| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/checkNameAvailability?api-version={api-version} |

#### Request (for local uniqueness) ####

| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/locations/{location}/checkNameAvailability?api-version={api-version} |


**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| location | The location in which uniqueness will be verified. |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

**Request Body**

    {
    "name": "{resourceNameToVerify}",
    "type": "{fully qualified resource type which includes provider namespace}"
    }

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the name availability check completed successfully.

**Response Headers**

Headers common to all responses.

**Response Body**

    {
    "nameAvailable": true|false,
    "reason": "Invalid|AlreadyExists",
    "message": "<error message>"
    }

| Element name | Description |
| --- | --- |
| nameAvailable | **Required.**  True indicates name is valid and available.  False indicates the name is invalid, unavailable, or both. |
| reason | **Required if nameAvailable == false.**  Invalid indicates the name provided does not match the resource provider&#39;s naming requirements (incorrect length, unsupported characters, etc.)  AlreadyExists indicates that the name is already in use and is therefore unavailable. |
| message | **Required if nameAvailable == false.**  Localized. If reason == invalid, provide the user with the reason why the given name is invalid, and provide the resource naming requirements so that the user can select a valid name.  If reason == AlreadyExists, explain that <resourceName> is already in use, and direct them to select a different name. |
