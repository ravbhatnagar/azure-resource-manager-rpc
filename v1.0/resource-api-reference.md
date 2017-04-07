# Resource API Reference

- [Resource API Reference](#resource-api-reference) <br/>
- [Arguments for CRUD on Resource](#arguments-for-crud-on-resource) <br/>
  - [Put Resource](#put-resource) <br/>
  - [Patch Resource](#patch-resource) <br/>
  - [Delete Resource](#delete-resource) <br/>
  - [Get Resource](#get-resource) <br/>
  - [Move Resource](#move-resource) <br/>

## Resource API Reference ##

These are the APIs that are implemented by the resource provider. Below is the description of arguments that will be used in PUT, PATCH, DELETE and GET. 

### Arguments for CRUD on Resource ###
| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| resourceGroupName | The resource group name uniquely identifies the resource group within the user subscriptionId. The resource group name must be no longer than 80 characters long, and must be alphanumeric characters (Char.IsLetterOrDigit()) and &#39;-&#39;, &#39;\_&#39;, &#39;(&#39;, &#39;)&#39; and&#39;.&#39;.  Note that the name cannot end with &#39;.&#39; |
| resourceProviderNamespace | The resource provider namespace can only be ASCII alphanumeric characters and the &quot;.&quot; character. |
| resourceType | The type of the resource – the resource providers declare the resource types they support at the time of registering with Azure. The resourceType should follow the lowerCamelCase convention and be plural (e.g. virtualMachines, resourceGroups, jobCollections, virtualNetworks).  The resource type can only be ASCII alphanumeric characters. |
| resourceName | The name of the resource. The name cannot include:   &#39;&lt;&#39;, &#39;&gt;&#39;, &#39;%&#39;, &#39;&amp;&#39;, &#39;:&#39;, &#39;\\&#39;, &#39;?&#39;, &#39;/&#39; OR any control characters. The max length is 260 characters. All other characters are allowed. The RP is expected to be more restrictive and have its own validation. |
| actionName | The action that is being performed on the resource (or a container that is inside the resource). |
| api-version | Specifies the version of the protocol used to make this request.  Format must match YYYY-MM-DD. It can be followed by a  -preview or -alpha or -beta or -rc or -privatepreview to indicate the appropriate milestone. |

### Put Resource ###

Creates or updates a resource belonging to a resource group. Resource types can be nested and, if so, must follow the Resource API guidelines.

ARM does not distinguish between creation and update. The resource provider should consult its datastore if a distinction is necessary. However, a PUT should always be allowed to overwrite an existing resource.

#### Request ####

| Method | Request URI |
| --- | --- |
| PUT | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

The resource group names and resource names should be matched case insensitively. That means, for example, if a user creates a resource in resource group &quot;rG1&quot;, and then calls a read operation on &quot;RG1&quot;, the same resource should be returned even though the casing differs.

Additionally, we MUST preserve the casing provided by the user. That means we should return back the most recently specified casing to the client (and we MUST not normalize / return back a toupper/tolower form of the resource group or resource name, for example).

The resource group name and resource name **MUST** come from the URL and not the request body. That is because there is no writable property for resource group, and the property is optional for PUT / PATCH (but the URL is REQUIRED).

**Request Body**

    {
      "location": "North US",
      "tags": {
          	"key": "value"
    },
      "properties": { 
            	"comment: Resource defined structure" 
      },
      "sku" : {
           	"name" : "sku code, such as P3",
           	"capacity" : {number}
     },
     "plan" : {
        	"name": "User defined name of the 3rd Party Artifact",
          "publisher": "Publisher of the 3rd Party Artifact ",
    		  "product": "OfferID for the 3rd Party Artifact ",
    		  "promotionCode": "Promotion Code",
    		  "version" : "Version of the 3rd Party Artifact"
    }
     "kind" : "resource kind"
    }
    
| **Field** | Description |
| --- | --- |
| **location** | Required, string. The location of the resource.  This would be one amongst the supported Azure Geo Regions registered by the RP:West US | East US | North Central US | South Central US | West Europe | North Europe | East Asia | Southeast Asia | East US 2 | etc.  Resource Providers should ignore whitespace and capitalization when accepting geo regions. That is, &quot;West US,&quot; &quot;westus&quot; and &quot;West us&quot; should all be acceptable for the georegion. This will greatly simplify the pattern for CLI / Powershell / SDK clients. An RP should use this to create the resource in the appropriate geo-affinity region.  The geo region of a resource never changes after it is created. |
| **tags** | A list of key value pairs that describe the resource. These tags can be used in viewing and grouping this resource (across resource groups). A maximum of 15 tags can be provided for a resource, and each tag must have a key no greater than 512 characters (and value no greater than 256 characters).  The resource provider is expected to store these tags with the resource.  For fields like &quot;label&quot; or &quot;description,&quot; it is recommended that the RP does not expose this as a separate property and instead leverage tags with these keys (clients will handle these &quot;recognized&quot; tags differently).  The tag name cannot include:   &#39;&lt;&#39;, &#39;&gt;&#39;, &#39;\*&#39;, &#39;%&#39;, &#39;&amp;&#39;, &#39;:&#39;, &#39;\\&#39;, &#39;?&#39;, &#39;+&#39;, &#39;/&#39;, and any control characters. |
| **properties** | Optional. Format not defined by ARM.Settings used to provision or configure the resource. The order of parameters in the request is unspecified. RPs should not rely on any particular ordering. |
| **kind** | Optional, string. Metadata used by portal/tooling/etc to render different UX experiences for resources of the same type; e.g. ApiApps are a kind of Microsoft.Web/sites type.  If supported, the resource provider must validate and persist this value. |
| **sku.name** | Required (if sku is specified), string. The name of the SKU. This is typically a letter + number code, such as A0 or P3 |
| **sku.tier** | Optional, string. The tier of this particular SKU. Typically one of: Free, Basic, Standard, Premium. This field is required to be implemented by the RP if the service has more than one tier, but is not required on a PUT. |
| **sku.size** | Optional, string. When the name field is the combination of tier and some other value, this would be the standalone code.|
| **sku.family** | Optional, string. If the service has different generations of hardware, for the same SKU, then that can be captured here. |
| **sku.capacity** | Optional, integer. If the SKU supports scale out/in then the capacity integer should be included. If scale out/in is not possible for the resource this may be omitted. |
| **plan** | Optional, Complex Type. Format defined by Azure.Fixed set of fields that provide the purchase context for a 3rd Party Product that is made available in Azure through Data Market. E.g. 3rd Party VM images that can be used in the VM Resource Type. |
| **plan.name** | Required (if plan is specified), string. A publisher defined name of the 3rd Party Artifact that is being procured. |
| **plan.publisher** | Required (if plan is specified), string. The publisher of the 3 rd Party Artifact that is being bought. E.g. NewRelic |
| **plan.product** | Required (if plan is specified), string. The 3rd Party artifact that is being procured. E.g. NewRelic. Product maps to the OfferID specified for the artifact at the time of Data Market onboarding. |
| **plan.promotionCode** | Optional, string. A publisher provided promotion code as provisioned in Data Market for the said product/artifact. |
| **plan.version** | Optional, string. The version of the desired product/artifact.  Ignored by commerce. |

##### Representing SKUs ####

The "sku" property should be used for defining the billing information of your resource (e.g. basic vs. standard). Any field that can have a billing impact for 1st party _services_ should be in the "sku" object. Note that 1st
party _artifacts_ are addressed via the plan entity.

The "sku" property is a complex type because it allows differentiation based on tiers (e.g. premium, free), families (e.g. generates of hardware) and other important details. The "sku" value should be **outside** the properties envelope.

##### Purchasing 3rd Party Artifacts #####

The Plan entity **MUST** be used for establishing the purchase context of any 3rd Party Artifact that is made available through the Azure Data Market. These artifacts can be 3rd Party Extension Resources like MySql Databases or an artifacts used in first party resources like images deployed in Azure Virtual Machines. Additionally, the plan entity can be used for procuring 1st
party artifacts which incur usage/billing in addition to the cost of the service (e.g. VMs running SQL/BizTalk/etc).

##### Resource Request Properties Envelope #####

Every resource can have a section with properties. These are the settings that describe or configure the resource. For example, the configuration for a job collection can be seen below:

PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}?api-version=2016-01-01

    {
     	"location": "North US",
     	"tags": {
         "department": "Finance",
         "app": "Quarterly Reports",
         "owner": "chlama"
       },
       	"sku": {  
           "name": "standard"  
        },
     	"properties": {  
        "quota": {  
           "maxJobCount": "10",  
           "maxRecurrence": {  
              "Frequency": "minute",  
              "interval": "1"  
              }  
            }  
    	}  
    }

Since different types of resources have different settings, the contents of this field are left under the control of the resource provider and ARM will never be made aware of these fields. However, in the case of ARM templates, the template execution engine will replace all parameters and expressions \*before\* passing the instantiated object to the RPs.

 It is important to note that, properties already defined outside of "properties" envelope **MUST** not be repeated inside "properties" in any form. Example of such properties is 'name', 'tags', 'location', etc. 

The settings can range from simple key-value pairs to complex nested structures. The user specifies these settings and Azure will pass them to the resource provider unmodified.

**NOTE** For proxy only resources, location and tags are not applicable in the request body.

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) or 201 (Created) to indicate that the operation completed successfully synchronously.

If the create request cannot be fulfilled quickly, the RP should return and follow the _Asynchronous Operations_ addendum. The resource provider can return 202 (Accepted) in these cases, but 201 + provisioningState is generally preferred.

If the subscription or the resource group does not exist, 404 (NotFound) should be returned.

412 (Precondition Failed) should be returned if the resource doesn&#39;t pass the condition specified by the If-Match header.

403 (Forbidden) should only be returned if the client certificate (used by ARM) is not trusted, it should not be used for any other case.

For other errors, use the appropriate HTTP error code.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body should contain _at least_ the original request that was PUT (and any other properties that would be returned in a GET, such as provisioningState, name, Id and type).

### Patch Resource ###

Updates a resource belonging to a resource group. ARM requires RPs to support PATCH for updating tags for a resource.

#### Request ####

| Method | Request URI |
| --- | --- |
| PATCH | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}? api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

**Request Body**

The request body can contain one to many of the properties present in the normal resource definition. For the explanation of these fields please see the PUT Resource section.

Of note, just like for PUT resource, a user can \*not\* change the location, type or name of their resource with a PATCH call. These fields are immutable.

An example of a common pattern is to PATCH an update to the Tags section of a resource. The behavior for a PATCH of the tags property is to replace all tags with the provided tag keys and values. As an example: if the resource currently has tag1 and tag2, and a PATCH request sends tag3, the final resource should have tag3 (and \*not\* tag1, tag2 and tag3).

The behavior for patching of the fields inside the properties envelope is left to the resource provider, although it should follow the Azure REST guidelines.

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully. 202 (Accepted) can be returned to indicate that the operation will complete asynchronously.

If the resource group \*or\* resource does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will contain the updated resource (using the existing value + the request in the PATCH) per the Azure REST guidelines [here] (https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md).

##### Representing SKUs #####

In addition, the PATCH operation must be supported for the SKU property to support scaling. For example, the following operation should update the SKU of the resource to be Free and not affect any of the other properties of the resource:

**Request Body**

    {
    "sku" : {
      	"name" : "F0",
      	"capacity" : 1
       }
    }

### Delete Resource ###

Deletes a resource from the resource group.

#### Request ####

| Method | Request URI |
| --- | --- |
| DELETE | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider can return 200 (OK) or 204 (NoContent) to indicate that the operation completed successfully. A 200 (OK) should be returned if the object exists and was deleted successfully; and a 204 (NoContent) should be used if the resource does not exist and the request is well formed.

202 (Accepted) can be returned to indicate that the operation will complete asynchronously.

If the resource group does not exist, 404 (NotFound) will be returned by the proxy layer and will not reach the resource provider. 412 (PreconditionFailed) and other normal REST codes are acceptable as long as they match the REST guidelines.

**Response Headers**

Only headers common to all responses.

**Response Body**

Empty

### Get Resource ###

Returns a resource belonging to a resource group. Resource types can be nested and, if so, must follow the REST guidelines (full details in the nested resource type section). Below are the three different request URIs to get resource or resource collection under a resource group or subscription. 

#### Request - Get a specific resource under resource group ####

| Method | Request URI |
| --- | --- |
| GET | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

#### Request - Get resource collection under resource group ####

Returns all the resources of a particular type belonging to a resource group. This is *not\* required for nested resource types (e.g. the SQL Azure databases underneath a SQL Azure server).

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}?api-version={api-version} |

#### Request - Get resource collection under subscription ####

Returns all the resources of a particular type belonging to a _subscription_. This is **\*not\*** required for nested resource types (e.g. the SQL Azure databases underneath a SQL Azure server).

ARM will query each regional endpoint that has at least one resource for the subscription and aggregate the responses for the client.

This allows the resource provider to remain regional and still support this query pattern (i.e. each regional endpoint needs only return the resources for that subscription in its region).

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{resourceType}?api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully.

If the resource does not exist, 404 (NotFound) should be returned. For other errors (e.g. internal errors) use the appropriate HTTP error code.

If the resource group does not exist, 404 (NotFound) will be returned by the proxy \*without\* reaching the resource provider.

If the subscription does not exist, 404 (NotFound) will be returned by the proxy \*without\* reaching the resource provider. If the subscription is not registered with the resource provider, it should return a 404 (NotFound) or an empty collection. It must not return a 5xx status code or 403.

**Response Headers**

Headers common to all responses.

**Response Body**

    {
     "id": "/subscriptions/{id}/resourceGroups/{group}/providers/{rpns}/{type}/{name}",
     "name": "{name}",
     "type": "{resourceProviderNamespace}/{resourceType}",
     "location": "North US",
     "tags": {
              "key1": "value 1",
              "key2": "value 2"
       },
    "kind" : "resource kind",
    "properties": { "comment: "Resource defined structure" }
    }

For a detailed explanation of each field in the response body, please refer to the request body description in the PUT resource section. The only GET specific properties are "name," "type" and "id."

| Field | Description |
| --- | --- |
| id | Required, stringThe id field should be the URL (excluding the hostname/scheme and api version) for the entity. It should not be URL encoded. E.g. /subscriptions/{id}/resourceGroups/{rgName}/providers/{rpns}/{typeName}/{name} This field is important to the platform – it is used as the identifier for references on other objects (e.g. if a virtual machine &quot;points&quot; to a vNet, it uses the id of the vNet as its reference), displaying links / references between resources in the portal, Authorization checks / validation, auditing / operational logs, etc. |
| name | Required, stringThe name does not need to be URL encoded or match exactly what is seen in the URL. It should be the name of the resource and is not expected to be globally unique (only unique for that particular collection / type in the resource group). |
| type | Required, stringThe type does not need to be URL encoded or match exactly what is seen in the URL.  It should include the resource provider namespace \*and\* the type of the entity. Examples include Microsoft.Web/Sites. |
| etag | Optional, stringThe Etag field is \*not\* required. If it is provided in the response body, it must also be provided as a header per [the normal ETag convention](http://www.rfc-editor.org/rfc/rfc2616.txt).  Entity tags are used for comparing two or more entities from the same requested resource. HTTP/1.1 uses entity tags in the ETag (section 14.19), If-Match (section 14.24), If-None-Match (section 14.26), and If-Range (section 14.27) header fields. The full guidance can be found in the Addendum. |
| kind | Optional.  String.Metadata used by portal/tooling/etc to render different UX experiences for resources of the same type; e.g. ApiApps are a kind of Microsoft.Web/sites type.  If supported, the resource provider must validate and persist this value. |

**Paging Response Body**

The paging approach required by ARM is server side paging, as described below.

    {
      "value": [
        {
        "id": "{url to resource 1}",
        "name": "Name1",
        "type": "{resourceProviderNamespace}/{resourceType}",
        "location": "North US"
        "properties": { "comment: "Resource defined structure" },
        "kind" : "resource kind"
    },
    {
        "id": "{url to resource 2}",
        "name": "Name2",
        "type": "{resourceProviderNamespace}/{resourceType}",
        "location": "North US",
        "properties": { "comment: "Resource defined structure" }.
        "kind" : "resource kind"
    }
    ],
    "nextLink": "{originalRequestUrl}?$skipToken={opaqueString}"
    }

The nextLink field is expected to point to the URL the client should use to fetch the next page (per server side paging). This matches the OData guidelines for paged responses [here](http://docs.oasis-open.org/odata/odata-json-format/v4.0/cos01/odata-json-format-v4.0-cos01.html#_Toc372793055). If a resource provider does not support paging, it should return the same body (JSON object with &quot;value&quot; property) but omit nextLink entirely (or set to null, \*not\* empty string) for future compatibility.

The nextLink should be implemented using following query parameters:

- skipToken: opaque token that allows the resource provider to skip resources already enumerated. This value is defined and returned by the RP after first request via nextLink.
- top: the optional client query parameter which defines the maximum number of records to be returned by the server.

Implementation details:

- NextLink may include all the query parameters (specifically OData $filter) used by the client in the first query.
- Server may return less records than requested with nextLink. Returning zero records with NextLink is an acceptable response.
- Clients must fetch records until the nextLink is not returned back / null. Clients should never rely on number of returned records to determinate if pagination is completed.

### Move Resource ###

Moves resources from the resource group to a target resource group. The target resource group **may** be in a different subscription.

The resource provider may choose to enforce its own set of restrictions – for example, it can require that all resources that are linked together move together. If a move request does not satisfy these restrictions, it can reject the move request with a specific and actionable error.

As some examples: (1) the website RP may require that all websites belonging to the same server farm move across resource groups together (along with the server farm); (2) the compute RP may require that all virtual machines belonging to the same availability set move across resource groups together (along with the availability set).

#### Request ####

| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/moveResources?api-version={api-version} |

**Arguments**

[Description here] (resource-api-reference.md#crud-arguments-id).

**Request Headers**

See common client request headers.

**Request Body**

    {
    "targetResourceGroup": "/subscriptions/{targetId}/resourceGroups/{targetName}",
    "resources":
    [
     "/subscriptions/{id}/resourceGroups/{source}/providers/{namespace}/{type}/{name}",
     "/subscriptions/{id}/resourceGroups/{source}/providers/{namespace}/{type}/{name}"
    ]
    }

| Element name | Description |
| --- | --- |
| targetResourceGroup | **Required** , string.The target resource group id to move the resources to.  The target resource group cannot be the same as the current (source) resource group. If the subscriptionId is different than the current resource group&#39;s subscriptionId, then additional checks will be performed in the frontdoor. |
| resources | **Required** , array of resource ids.The collection of resources to move to the target resource group.  The resources must be from the current resource group from the request URL. At most 250 resources can be moved with a single request. The resources can span several different resource providers and resource types. |

#### Response ####

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

ARM will perform some basic validation before forwarding the request to the resource provider. This includes:

| Failure Reason | Error Code |
| --- | --- |
| The target resource group is the same as the source resource group. | 400 |
| The target resource group's subscription (if different) does not have the same location placement / geo fencing requirements as the source subscription. | 400 |
| The target resource group&#39;s subscription (if different) does not exist, is disabled, or is deleted. | 400 |
| The target resource group&#39;s subscription (if different) is not registered for the resource types present in the request. | 400 |
| The target resource group&#39;s subscription (if different) does not belong to the same AAD directory / tenant. | 403 |
| The target resource group does not exist. | 400 |
| One of the values in the resources collection is not from current resource group. | 400 |
| One of the resources in the resources list is a child resource (only top level resources can be moved; their children are assumed to be moved). | 400 |
| The resource type does not support move. | 400 |
| Too many resources are present in the request (250 is the limit). | 400 |
| The resource move would cause the quota for the subscription / resource group quotas to be exceeded. | 409 |
| The source or target resource group is locked (e.g. move already in progress, resource group is being deleted). | 409 |
| Target resource group already has resource with the same Id as given in the request. | 409 |
| The user is not authorized to perform move operation on target or destination resource group. | 403 |

If the request reaches the resource provider, it should return 200 (OK) to indicate that the operation completed successfully.

202 (Accepted) can be returned to indicate that the operation will [complete asynchronously](Addendum.md#async-id).

If the resource group \*or\* resource does not exist, 404 (NotFound) should be returned. A 400 (BadRequest) can be used if the request does not satisfy the RP specific requirements.

**Response Headers**

Headers common to all responses.

**Response Body**

Empty
