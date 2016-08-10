# Resource Provider API v2.0

## Contents
1. [Related Documents](https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#related-documents-id) 
2. [Common API Details] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#common-api-details-id) </br>
    a. [Common API Request Details] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#common-api-req-details-id) </br>
         i) [Proxy Request Header Modifications] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-req-header-mod-id) </br>
         ii) [Client Request Headers] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#client-req-header-id) </br>
         iii) [Request Query Parameters] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#req-query-param-id) </br>
	    	iv) [Case Insensitivity for Requests] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#case-insensitivity-req-id) </br>
	    	v) [Client Request Timeout] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#client-req-timeout-id) </br>
	    	vi) [Request Throttling] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#req-throttle-id) </br>
    b. [Common API Response Details] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#common-api-res-details-id) </br>
	    	i) [Response Headers] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#res-headers-id) </br>
	    	ii) [Error Response Content] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#err-res-content-id) </br>
	    	iii) [Max Response Size] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#max-res-size-id) </br>
	    	iv) [Transfer-Encoding] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#xfer-encoding-id) </br>
	    	v) [Redirecting the Client] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#redirect-client-id) </br>
3. [Subscription Lifecycle API Reference] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#sub-lifecyclye-ref-id) <br/>
    a. [Updating a subscription] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#sub-lifecyclye-ref-id) <br/>
	i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#sub-lifecyclye-ref-id) <br/>
	ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#sub-lifecyclye-ref-id) <br/>
	iii) [Subscription States] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#sub-lifecyclye-ref-id) <br/>
4. [Resource API Reference] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#resource-ref-id) <br/>
    a. [Put Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#put-resource-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#put-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#put-resource-id) <br/>
    b. [Patch Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#patch-resource-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#patch-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#patch-resource-id) <br/>
    c. [Delete Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#delete-resource-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#delete-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#delete-resource-id) <br/>
    d. [Get Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
    e. [Get Resources in Resource Group] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
                i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
     f. [Get Resources in Subscription] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
                i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
      g. [Move Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
                i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#get-resource-id) <br/>
5. [Proxy API Reference] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
    a. [Routing Requests] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
    b. [Resource Action Requests] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
     c. [Subscription wide Reads and Actions i.e. GETs/POSTs] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
     d. [Exposing Available Operations (for Client discovery)] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		i) [Request] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		ii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
      e. [Check Name Availability Requests] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		i) [Request (for Global Uniqueness)] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		ii) [Request (for local uniqueness)] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
		iii) [Response] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#proxy-ref-id) <br/>
6. [Addendum] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     a. [Instrumentation and Tracing across services] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     b. [ETags for Resources] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     c. [Regional Endpoints] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     d. [Nested Resources] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     e. [Resource Group Deletes] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     f. [Asynchronous Operations] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     g. [Creating or Updating Resources (PUT/PATCH)] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     h. [DELETE Resource] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     i. [Call Action (POST {resourceUrl/action})] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     j. [Provisioning State Property] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     k. [202 Accepted and Location Headers] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>
     l. [Operation Resource Format (returned by Azure-AsyncOperation Header)] (https://github.com/azure/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#addendum-id) <br/>

This document covers the API contract that must be implemented by each Resource Provider in order to onboard to the Azure management API surface (as well as RBAC, tags, and templates).

<div id='related-documents-id'/>
## Related Documents

- [Cloud Service Model](http://sharepoint/sites/azure-arc/Windows%20Azure%20Service%20Model/Cloud%20Service%20Model.docx), for the high-level description of resource groups, resources, extensions and how they are modeled.
- [Resource Manager Template Language Specification](https://azure.microsoft.com/en-us/documentation/articles/resource-group-authoring-templates/#resources), for the detailed specification of the template language.
- [Resource Manager API](https://msdn.microsoft.com/en-us/library/dn790568.aspx), for the specification of the APIs exposed by ARM.

<div id='common-api-details-id'/>
## Common API Details

<div id='common-api-req-details-id'/>
### Common API Request Details

<div id='proxy-req-header-mod-id'/>
#### Proxy Request Header Modifications

The resource provider proxy will preserve all the client requests headers, with the exception of modifications per the details below. The headers below are reserved and cannot be set by clients.


| Header                                       | Description | 
| :------------------------------------------- | :------------------------------------------------ |
| referer | Always added (1st and 3rd party) Set to the full URI that the client connected to (which will be different than the RP URI, since it will have the public hostname instead of the RP hostname).This value can be used in generating FQDN for Location headers or other requests since RPs should not reference their endpoint name. |  
| authorization | Always removed/changed (1st and 3rd party). The authorization used by the client to the proxy will be different than the authorization used to communicate from the proxy to the resource provider. |
| x-ms-correlation-request-id | Always added (1st and 3rd party). Specifies the tracing correlation Id for the request; the resource provider \*must\* log this so that end-to-end requests can be correlated across Azure. |
| x-ms-client-ip-address | Always added (1st and 3rd party). Set to the client IP address used in the request; this is required since the resource provider will not have access to the client IP. |
| x-ms-client-principal-name | Always added (1st party only). Set to the principal name / UPN of the client JWT making the request. |
| x-ms-client-principal-id | Added when available (1st party only). Set to the principal Id of the client JWT making the request. Service principal will not have the principal Id. |
| x-ms-client-tenant-id | Always added (1st party only). Set to the tenant ID of the client JWT making the request. |
| x-ms-client-audience | Always added (1st party only). Set to the audience of the client JWT making the request. |
| x-ms-client-issuer | Always added (1st party only). Set to the issuer of the client JWT making the request. |
| x-ms-client-object-id | Always added (1st party only). Set to the object Id of the client JWT making the request. Not all users have object Id. For CSP (reseller) scenarios for example, object Id is not available. |
| x-ms-client-app-id | Always added (1st party only). Set to the app Id of the client JWT making the request. |
| x-ms-client-app-id-acr | Always added (1st party only). Set to the app Id acr claim of the client JWT making the request. This is the application authentication context class reference claim which indicates how the client was authenticated. |
| x-ms-client-authorization-source | Always added (1st party only). Specifies the authorization source of the token. It&#39;s value can be NotSpecified, Legacy, RoleBased, Bypassed, Direct and Management. |
| x-ms-client-identity-provider | Always added (1st party only). Set to the identity provider of the client JWT. |
| x-ms-client-wids | Always added (1st party only). Set to the wids of the client JWT. These identify the admins of the tenant which issued the JWT. |
| x-ms-client-authentication-methods | Always added (1st party only). Set to the authentication method references of client JWT. |

<div id='client-req-header-id'/>
#### Client Request Headers

Any non-reserved headers provided by the client will pass as-is to the resource provider. All requests to resource providers may include the following standard headers and \*must\* be supported:

| Header | Description |
| --- | --- |
| Content-Type | Set to application/json. This header is not sent in requests that don&#39;t have any content, such as all GET calls. |
| Accept-Language | Specifies the preferred language for the response; all RPs should use this header when generating error messages or client facing text. |
| x-ms-client-request-id | Caller-specified value identifying the request, in the form of a GUID with no decoration such as curly braces (e.g. client-request-id: 9C4D50EE-2D56-4CD3-8152-34347DC9F2B0). If the caller provides this header – the resource provider \*must\* log this with their traces to facilitate tracing a single request.If specified, this will be included in response information as a way to map the request if "x-ms-return-client-request-id"; is specified as "true". |
| x-ms-return-client-request-id | Optional. True or false and indicates if a client-request-id should be included in the response. Default is false. |

<div id='req-query-param-id'/>
#### Request Query Parameters

The RP-FD will proxy request parameters (e.g. $filter; $expand; $skipToken; etc.) as-is to the Resource Providers. It will not delete, modify or add any query parameters before relaying the request.

<div id='case-insensitivity-req-id'/>
#### Case Insensitivity for Requests

When satisfying incoming requests, it is assumed that the following values are stored / indexed / compared in a case \*insensitive\* way:

- Resource group name
- Resource name
- Other names of entities in the URL, even if they are not resources.

<div id='client-req-timeout-id'/>
#### Client Request Timeout

Requests proxied to the resource provider are made with a client timeout of 60 seconds. If request take more than 60 seconds please consider using asynchronous request/response pattern.

The resource provider must respond within that time interval or the client will receive a 504 (timeout) error code and will not see the response from the RP.

<div id='req-throttle-id'/>
#### Request Throttling

ARM provides subscription level throttling. More details on these limits can be found [here] (https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/#overview)

<div id='common-api-res-details-id'/>
### Common API Response Details

<div id='res-headers-id'/>
#### Response Headers

All responses from resource providers should include the following headers:

| Header | Description |
| --- | --- |
| Content-Type | Set to application/json. This header is not required in responses that don&#39;t have any content. |
| Date | The date that the request was processed, in RFC 1123 format. |
| x-ms-request-id | A unique identifier for the current operation, service generated.All the resource providers \*must\* return this value in the response headers to facilitate debugging. |

All long running operations (i.e. those that return 202 Accepted) will use these headers:

| Header | Description |
| --- | --- |
| Location | Set to the URL where the status of the long running operation can be checked. |
| Azure-AsyncOperation | Set to the URL where the result of the long running operation can be checked; to optionally be used in addition to the Location header. |
| Retry-After | Set to the delay that the client should use when checking for the status of the operation. This value is an integer and represents the seconds. |

<div id='error-res-content-id'/>
#### Error Response Content

If the resource provider needs to return an error to any operation, it should return the appropriate HTTP error code and a message body as can be seen below. The message should be localized per the Accept-Language header specified in the original request such that it could be directly be exposed to users.

The resource providers must return the \*code\* and \*message\* fields; however, the other fields are acceptable as additions. This format matches [the OData v4.0 schema](http://docs.oasis-open.org/odata/odata-json-format/v4.0/os/odata-json-format-v4.0-os.html#_Toc372793091) for error responses.

**Response Body**

{

    "error": {
      "code": "BadArgument",
      "message": "The provided database &#39;foo&#39; has an invalid username.",
      "target": "query",
      "details": [
        {
	
         "code": "301",
         "target": "$search"
         "message": "$search query option not supported",
        }
      ]

      "innererror": {
        "trace": [...],
        "context": {...}

      }

    }

}


| Element name | Description |
| --- | --- |
| message | Required, string.Describes the error in detail and provides debugging information. If Accept-Language is set in the request, it must be localized to that language. |
| code | Required, string.String that can be used to programmatically identify the error. Some will be standardized for all Azure REST services, some will be domain specific. These error code should not be localized, but are typically a string like &quot;BadArgument&quot;, &quot;NotFound&quot;, etc. |
| target | Optional, string.The target of the particular error (for example, the name of the property in error). |
| details | Optional, string.An array of JSON objects that MUST contain name/value pairs for code and message, and MAY contain a name/value pair for target, as described above.The contents of this section are service-defined but must adhere to the aforementioned schema. |
| innererror | Optional, string.The contents of this object are service-defined. Usually this object contains information that will help debug the service. |

<div id='max-res-size-id'/>
#### Max Response Size

In all the calls that ARM makes to the resource provider, the maximum size of a response that ARM will accept from the resource providers is 4 MB.

Any response greater than 4 MB in size will be dropped by ARM, and **500 Internal Server Error** will be returned to the client.  In general, APIs exposed by the resource provider should be designed to transmit relatively little data in keeping with the management nature of the API.

<div id='xfer-encoding-id'/>
#### Transfer-Encoding

Chucked transfer encoding is supported and can be used for larger payloads.

<div id='redirect-client-id'/>
#### Redirecting the Client

The Resource Provider may return a 307 response code to the customer if they want to expose a direct URL / host (with no proxy) to the user. As an example – when downloading a large file, the RP may return a 307 to a URL on storage to download that file.

The frontdoor will \*not\* follow any redirects and will instead proxy them directly back to the client.

<div id='sub-lifecyclye-ref-id'/>
## Subscription Lifecycle API Reference

### Creating or Updating a Subscription

Creates or updates a subscription for this particular resource provider. It includes changes in the state of the subscription which may trigger other actions (setup or teardown).

This API uses the &quot;system&quot; version of 2.0 because it can be triggered by commerce and not necessarily by a user request.

#### Request

| Method | Request URI |
| --- | --- |
| PUT | https://&lt;registered-resource-provider-endpoint&gt;/subscriptions/{subscriptionId}?api-version=2.0 |

**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |

**Request Body**

    {
    "state": "Registered" | "Unregistered" | "Warned" | "Suspended" | "Deleted",

    "registrationDate": "Tue, 15 Nov 1994 08:12:31 GMT"

    "properties": {

         "tenantId":"ac430efe-1866-4124-9ed9-ee67f9cb75db",
         "locationPlacementId":"Internal\_2014-09-01",

         "quotaId":"Default\_2014-09-01",

         "accountOwner": { "puid": "<account\_puid>", "email": "<account\_email>" }

    "registeredFeatures": [{ "name": "<featureName>", "state": "Registered" }]
      }
    }

| **Element name** | Description |
| --- | --- |
| **state** | **Required**.One of &quot;Registered&quot;, &quot;Unregistered&quot;, &quot;Warned&quot;, &quot;Suspended&quot; , or &quot;Deleted&quot;; used to indicate the current state of the subscription. The resource provider should always take the latest state. Transition among any states is valid (it is possible to receive Suspended / Warned before Registered, for example).<br/> **Registered:** The subscription was entitled to use your &quot;ResourceProviderNamespace&quot;.   Azure will use this subscription in future communications. You may also do any initial state setup as a result of this notification type.  When a subscription is &quot;fixed&quot; / restored from being suspended, it will return to the &quot;Registered&quot; state.  All management APIs must function (PUT/PATCH/DELETE/POST/GET), all resources must run normally; bill normally. <br/>  **Warned:** The subscription has been warned (generally due to forthcoming suspension resulting from fraud or non-payment). Resources must be offline but in running (or quickly recoverable state).  Do **not** deallocate resources.   GET/DELETE management APIs must function; PUT/PATCH/POST must not.  Any emitted usage will be ignored. <br/>    **Suspended:** The subscription has been suspended (generally due to fraud or non-payment) and the Resource Provider should stop the subscription from generating any additional usage. Pay-for-use resource should have access rights revoked when the subscription is disabled.   In such cases the Resource Provider should also mark the Resource State as &quot;Suspended.&quot;  We recommend that you treat this as a soft-delete so as to get appropriate customer attention. GET/DELETE management APIs must function; PUT/PATCH/POST must not. <br/>  **Deleted:** The customer has cancelled their Windows Azure subscription and its content \*must\* be cleaned up by the resource provider.The resource provider does \*not\* receive a DELETE call for each resource – this is expected to be a &quot;cascade&quot; deletion. <br/>  **Unregistered:** Either the customer has not yet chosen to use the resource provider, or the customer has decided to stop using the Resource Provider. Only GETs are permitted. In the case of formerly registered subscriptions, all existing resources would already have been deleted by the customer explicitly. |
| **properties** | Required.Property bag contains other name/value pairs that can be used for telemetry and logging. The resource provider should handle unexpected property key/value pairs without issue, as we will introduce new metadata without updating the contract version. The value inside the properties envelope may be a complex type / object / token itself. |
| **properties.tenantId** | Optional.The AAD directory/tenant to which the subscription belongs. |
| **properties.locationPlacementId** | Optional.The placement requirement for the subscription based on its country of origin / offer type / offer category / etc. This is used in geo-fencing of certain regions or regulatory boundaries (e.g. Australia ring-fencing). |
| **properties.quotaId** | Optional.The quota requirement for the subscription based on the offer type / category (e.g. free vs. pay-as-you-go). This can be used to inform quota information for the subscription (e.g. max # of resource groups or max # of virtual machines. |
| **Properties.registeredFeatures** | Optional.All AFEC features that the subscriptions has been registered under RP namespace and platform namespace (Microsoft.Resources) |
| **Properties.accountOwner** | Optional.This is the account owner of the subscription. |

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully. 202 (Accepted) can be returned to indicate that the operation will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

The location header is not followed as part of the notification; instead, the notification will be retried with a delay. It is expected that subsequent updates that are a no-op will complete synchronously.

This operation is expected to be idempotent, so the resource provider should return a 200 status code if the notification can be honored correctly. As an example, if the RP only sees an &quot;unregistered&quot; subscription state for a subscription it has no record of, it should return a 200.

**Response Headers**

Headers common to all responses.

**Response Body**

If a 200, the response body will contain the original request that was PUT per the Azure REST guidelines.

#### Subscription States contents here

<div id='resource-ref-id'/>
## Resource API Reference

These are the APIs that are implemented by the resource provider. Below is the description of arguments that will be used in PUT, PATCH, DELETE and GET. 

<div id='crud-arguments-id'/>
###Arguments for CRUD on Resource
| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| resourceGroupName | The resource group name uniquely identifies the resource group within the user subscriptionId. The resource group name must be no longer than 80 characters long, and must be alphanumeric characters (Char.IsLetterOrDigit()) and &#39;-&#39;, &#39;\_&#39;, &#39;(&#39;, &#39;)&#39; and&#39;.&#39;.  Note that the name cannot end with &#39;.&#39; |
| resourceProviderNamespace | The resource provider namespace can only be ASCII alphanumeric characters and the &quot;.&quot; character. |
| resourceType | The type of the resource – the resource providers declare the resource types they support at the time of registering with Azure. The resourceType should follow the lowerCamelCase convention and be plural (e.g. virtualMachines, resourceGroups, jobCollections, virtualNetworks).  The resource type can only be ASCII alphanumeric characters. |
| resourceName | The name of the resource. The name cannot include:   &#39;&lt;&#39;, &#39;&gt;&#39;, &#39;%&#39;, &#39;&amp;&#39;, &#39;:&#39;, &#39;\\&#39;, &#39;?&#39;, &#39;/&#39; and any control characters. The max length is 260 characters. All other characters are allowed. The RP is expected to be more restrictive and have its own validation. |
| actionName | The action that is being performed on the resource (or a container that is inside the resource). |
| api-version | Specifies the version of the protocol used to make this request.  Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

<div id='put-resource-id'/>
### Put Resource

Creates or updates a resource belonging to a resource group. Resource types can be nested and, if so, must follow the REST guidelines (full details in the nested resource type section).

Azure does not distinguish between creation and update. The resource provider should consult its database if a distinction is necessary. However, a PUT should always be allowed to overwrite an existing resource.

#### Request

| Method | Request URI |
| --- | --- |
| PUT | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

The resource group names and resource names should be matched case insensitively. That means, for example, if a user creates a resource in resource group &quot;rG1&quot;, and then calls a read operation on &quot;RG1&quot;, the same resource should be returned even though the casing differs.

Additionally, we MUST preserve the casing provided by the user. That means we should return back the most recently specified casing to the client (and we MUST not normalize / return back a toupper/tolower form of the resource group or resource name, for example).

The resource group name and resource name should come from the URL and not the request body. That is because there is no writable property for resource group, and the property is optional for PUT / PATCH (but the URL is REQUIRED).

**Request Body**

    {
    "location": "North US",
    "tags": {
        "key": "value"
    },
    "properties": { "comment: Resource defined structure" },
    "kind" : "resource kind"
    }
| **Field** | Description |
| --- | --- |
| **location** | Required, string.The location of the resource.  This would be one amongst the supported Azure Geo Regions registered by the RP:West US | East US | North Central US | South Central US | West Europe | North Europe | East Asia | Southeast Asia | East US 2 | etc.  Resource Providers should ignore whitespace and capitalization when accepting geo regions. That is, &quot;West US,&quot; &quot;westus&quot; and &quot;West us&quot; should all be acceptable for the georegion. This will greatly simplify the pattern for CLI / Powershell / SDK clients. An RP should use this to create the resource in the appropriate geo-affinity region.  The geo region of a resource never changes after it is created. |
| **tags** | A list of key value pairs that describe the resource. These tags can be used in viewing and grouping this resource (across resource groups).  A maximum of 15 tags can be provided for a resource, and each tag must have a key no greater than 512 characters (and value no greater than 256 characters).  The resource provider is expected to store these tags with the resource.  For fields like &quot;label&quot; or &quot;description,&quot; it is recommended that the RP does not expose this as a separate property and instead leverage tags with these keys (clients will handle these &quot;recognized&quot; tags differently).  The tag name cannot include:   &#39;&lt;&#39;, &#39;&gt;&#39;, &#39;\*&#39;, &#39;%&#39;, &#39;&amp;&#39;, &#39;:&#39;, &#39;\\&#39;, &#39;?&#39;, &#39;+&#39;, &#39;/&#39;, and any control characters. |
| **properties** | Optional, format not defined by Azure.Settings used to provision or configure the resource. The order of parameters in the request is unspecified. RPs should not rely on any particular ordering. |
| **kind** | Optional.  String.Metadata used by portal/tooling/etc to render different UX experiences for resources of the same type; e.g. ApiApps are a kind of Microsoft.Web/sites type.  If supported, the resource provider must validate and persist this value. |

##### Resource Request Properties Envelope

Every resource can have a section with properties. These are the settings that describe or configure the resource. For example, the configuration for a job collection can be seen below:

    {
    "id": "/subscriptions/{id}/resourceGroups/{group}/providers/{rpns}/{type}/{name}",
    "name": "Finance Report Jobs",
    "type": "Microsoft.Scheduler/jobCollections",
    "location": "North US",
    "tags": {
         "department": "Finance",
         "app": "Quarterly Reports",
         "owner": "chlama"
     },
    "properties": {
       "mode": "Standard",
        "quota": {
            "minimumRecurrence": "00:15:00",
            "maximumJobs": 100
        }
     },
    "kind" : "resource kind"
    }

Since different types of resources have different settings, the contents of this field are left under the control of the resource provider and CSM will never be made aware of these fields. However, in the case of CSM service templates, the template execution engine will replace all parameters and expressions \*before\* passing the instantiated object to the RPs.

[11/25/2015] It is important to note that, properties already defined outside of "properties" envelope should not be repeated inside "properties" in any form. Example of such proprieties is 'name', 'tags', 'location', etc. Failure to comply with this rule will be considered as RP contract violation and must be fixed.


The settings can range from simple key-value pairs to complex nested structures. The user specifies these settings and Azure will pass them to the resource provider unmodified.

The settings can range from simple key-value pairs to complex nested structures. The user specifies these settings and Azure will pass them to the resource provider unmodified.

##### Purchasing 3rd Party Artifacts

The Plan entity should be used for establishing the purchase context of any 3 rd Party Artifact that is made available through the Azure Data Market. These artifacts can be 3rd Party Extension Resources like MySql Databases or an artifacts used in first party resources like images deployed in Azure Virtual Machines.  Additionally, the plan entity can be used for procuring 1st
party artifacts which incur usage/billing in addition to the cost of the service (e.g. VMs running SQL/BizTalk/etc).

~~**Note: The Plan entity cannot be used to procure 1st Party Resources.**~~

    "plan": {
    "name": "User defined name of the 3rd Party Artifact",
    "publisher": "Publisher of the 3rd Party Artifact ",
    "product": "OfferID for the 3rd Party Artifact ",
    "promotionCode": "Promotion Code",
    "version" : "Version of the 3rd Party Artifact"
    }
| **Field** | **Description**|
|----|----|
| plan | Optional, Complex Type, format defined by Azure.Fixed set of fields that provide the purchase context for a 3rd Party Product that is made available in Azure through Data Market. E.g. 3rd Party VM images that can be used in the VM Resource Type. |
| plan.name | Required, string.A user defined name of the 3rd Party Artifact that is being procured. |
| plan.publisher | Required, string.The publisher of the 3 rd Party Artifact that is being bought. E.g. NewRelic |
| plan.product | Required, stringThe 3rd Party artifact that is being procured. E.g. NewRelic. Product maps to the OfferID specified for the artifact at the time of Data Market onboarding. |
| plan.promotionCode | Optional, stringA publisher provided promotion code as provisioned in Data Market for the said product/artifact. |
| plan.version | Optional, stringThe version of the desired product/artifact.  Ignored by commerce. |

##### Representing SKUs

The "sku" property should be used for defining the billing information of your resource (e.g. basic vs. standard). Any field that can have a billing impact for 1st party _services_ should be in the "sku" object. Note that 1st
party _artifacts_ are addressed via the plan entity.

The "sku" property is a complex type because it allows differentiation based on tiers (e.g. premium, free), families (e.g. generates of hardware) and other important details. The "sku" value should be **outside** the properties envelope.

    {
    "id": "/subscriptions/{id}/resourceGroups/{group}/providers/{rpns}/{type}/{name}",
    "name": "Finance Report Jobs",
    "type": "Microsoft.Scheduler/jobCollections",
    "location": "North US",
    "properties": {
    },

    "sku" : {
           "name" : "sku code, such as P3",
           "tier" : "free|basic|standard|premium",
           "size" : "A0",
           "family": "A", // later B, C, etc.
           "capacity" : {number}
     },
    "kind" : "resource kind"
    }

| **Field** | **Description** |
| --- | --- |
| **name** | Required, string The name of the SKU. This is typically a letter + number code, such as A0 or P3 |
| **tier** | Optional, string The tier of this particular SKU. Typically one of: Free, Basic, Standard, Premium. This field is required to be implemented by the RP if the service has more than one tier, but is not required on a PUT. |
| **size** | Optional, stringWhen the name field is the combination of tier and some other value, this would be the standalone code.|
| **family** | Optional, stringIf the service has different generations of hardware, for the same SKU, then that can be captured here. |
| **capacity** | Optional, integer If the SKU supports scale out/in then the capacity integer should be included. If scale out/in is not possible for the resource this may be omitted. |

#### Response

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

<div id='patch-resource-id'/>
### Patch Resource

Updates a resource belonging to a resource group.

#### Request

| Method | Request URI |
| --- | --- |
| PATCH | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}? api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

**Request Body**

The request body can contain one to many of the properties present in the normal resource definition. For the explanation of these fields please see the PUT Resource section.

Of note, just like for PUT resource, a user can \*not\* change the location, type or name of their resource with a PATCH call. These fields are immutable.

An example of a common pattern is to PATCH an update to the Tags section of a resource. The behavior for a PATCH of the tags property is to replace all tags with the provided tag keys and values. As an example: if the resource currently has tag1 and tag2, and a PATCH request sends tag3, the final resource should have tag3 (and \*not\* tag1, tag2 and tag3).

The behavior for patching of the fields inside the properties envelope is left to the resource provider, although it should follow the Azure REST guidelines.

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully. 202 (Accepted) can be returned to indicate that the operation will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

If the resource group \*or\* resource does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will contain the updated resource (using the existing value + the request in the PATCH) per the Azure REST guidelines (v2.1 can be seen [here](http://sharepoint/sites/azure-arc/REST%20Guidelines/Azure%20REST%20Design%20Guidelines%20v2.1.docx)).

##### Representing SKUs

In addition, the PATCH operation must be supported for the SKU property to support scaling. For example, the following operation should update the SKU of the resource to be Free and not affect any of the other properties of the resource:

**Request Body**

    {
    "sku" : {
      "name" : "F0",
      "tier" : "free",
      "capacity" : 1
       }
    }

<div id='delete-resource-id'/>
### Delete Resource

Deletes a resource from the resource group.

#### Request

| Method | Request URI |
| --- | --- |
| DELETE | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider can return 200 (OK) or 204 (NoContent) to indicate that the operation completed successfully. A 200 (OK) should be returned if the object exists and was deleted successfully; and a 204 (NoContent) should be used if the resource does not exist and the request is well formed.

202 (Accepted) can be returned to indicate that the operation will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

If the resource group does not exist, 404 (NotFound) will be returned by the proxy layer and will not reach the resource provider. 412 (PreconditionFailed) and other normal REST codes are acceptable as long as they match the REST guidelines.

**Response Headers**

Only headers common to all responses.

**Response Body**

Empty

<div id='get-resource-id'/>
### Get Resource

Returns a resource belonging to a resource group. Resource types can be nested and, if so, must follow the REST guidelines (full details in the nested resource type section).

#### Request

| Method | Request URI |
| --- | --- |
| GET | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully.

If the resource does not exist, 404 (NotFound) should be returned. For other errors (e.g. internal errors) use the appropriate HTTP error code.

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
    "etag": "00000000-0000-0000-0000-000000000000",
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

### Get Resources in the Resource Group

Returns all the resources of a particular type belonging to a resource group. This is **\*not\*** required for nested resource types (e.g. the SQL Azure databases underneath a SQL Azure server).

#### Request

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully. For other errors (e.g. internal errors) use the appropriate HTTP error code.

If the resource group does not exist, 404 (NotFound) will be returned by the proxy \*without\* reaching the resource provider.

**Response Headers**

Headers common to all responses.

**Paging Response Body**

The paging approach required by CSM is server side paging, as described [here](https://microsoft.sharepoint.com/teams/azure-arc/_layouts/15/WopiFrame.aspx?sourcedoc=%7b3379D14C-13C8-4B2C-B00F-15DDCF7E2F06%7d&amp;action=default).

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

### Get Resources in the Subscription

Returns all the resources of a particular type belonging to a _subscription_. This is **\*not\*** required for nested resource types (e.g. the SQL Azure databases underneath a SQL Azure server).

The front door will query each regional endpoint that has at least one resource for the subscription and aggregate the responses for the client.

This allows the resource provider to remain regional and still support this query pattern (i.e. each regional endpoint needs only return the resources for that subscription in its region).

#### Request

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{resourceType}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully. For other errors (e.g. internal errors) use the appropriate HTTP error code.

If the subscription does not exist, 404 (NotFound) will be returned by the proxy \*without\* reaching the resource provider. If the subscription is not registered with the resource provider, it should return a 404 (NotFound) or an empty collection. It must not return a 5xx status code or 403.

**Response Headers**

Headers common to all responses.

**Paging Response Body**

The paging approach required by CSM is server side paging, as described [here](https://microsoft.sharepoint.com/teams/azure-arc/_layouts/15/WopiFrame.aspx?sourcedoc=%7b3379D14C-13C8-4B2C-B00F-15DDCF7E2F06%7d&amp;action=default).

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
        "properties": { "comment: "Resource defined structure" },
        "kind" : "resource kind"
    }
    ],
     "nextLink": "{originalRequestUrl}?$skipToken={opaqueString}"
    }

The nextLink field is expected to point to the URL the client should use to fetch the next page (per server side paging). This matches the OData guidelines for paged responses [here](http://docs.oasis-open.org/odata/odata-json-format/v4.0/cos01/odata-json-format-v4.0-cos01.html#_Toc372793055). If a resource provider does not support paging, it should return the same body but leave nextLink null for future compatibility.

For a detailed explanation of each field in the response body, please refer to the request body description in the PUT resource section.

### Resource Move Reference

Moves resources from the resource group to a target resource group. The target resource group **may** be in a different subscription.

The resource provider may choose to enforce its own set of restrictions – for example, it can require that all resources that are linked together move together. If a move request does not satisfy these restrictions, it can reject the move request with a specific and actionable error.

As some examples: (1) the website RP may require that all websites belonging to the same server farm move across resource groups together (along with the server farm); (2) the compute RP may require that all virtual machines belonging to the same availability set move across resource groups together (along with the availability set).

#### Request

| Method | Request URI |
| --- | --- |
| POST | https://&lt;endpoint&gt;/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/moveResources?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

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

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The frontdoor will perform some basic validation before forwarding the request to the resource provider. This includes:

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

202 (Accepted) can be returned to indicate that the operation will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

If the resource group \*or\* resource does not exist, 404 (NotFound) should be returned. A 400 (BadRequest) can be used if the request does not satisfy the RP specific requirements.

**Response Headers**

Headers common to all responses.

**Response Body**

Empty

<div id='proxy-ref-id'/>
## Proxy API reference

The RP-FD will proxy requests to backing resource providers even if they are not related directly to resource management or subscription lifecycle changes.

These requests are considered to be part of the "Proxy API" and examples include: restart a VM; fetch storage account keys; or increase the capacity of a mobile service.

### Routing Requests

From a client's point of view, the Azure API head is flat across all resources. To disambiguate requests across resource providers, the resource provider namespace will always be present in proxied request URLs (e.g. "compute" or "web").

If the customer's request does \*not\* include a resource provider namespace, then the RP-FD itself will service the request (examples include: finding all resources in a resource group; finding all resources that match a particular tag key or value; finding all resources of a particular type in a subscription).

### Resource Action Requests

Actions can be performed on objects (e.g. reimage VM instance), but still need to be modeled in a consistent way across internal and external resource providers. Through this consistency, resource providers will be able to "light-up" authorization / RBAC scenarios without changing their API surface.

In order to make the "action" consistent across resource providers, the action name must be included in the URL via a specific format (which is aligned with OData). **This value is extracted as the last segment in the URL that does not have a matching type or container preceding it (i.e. the last odd segment).**

The HTTP verb and request body will \*not\* be used in identifying the "action" being taken on the resource provider if the action name is provided.

**If no action name is provided, the HTTP Verb (e.g. GET / PUT) will be used as the action name.**

#### Request

| Method | Request URI |
| --- | --- |
| POST | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}/{actionName}?api-version={api-version} |

**Arguments**

[Description here] (https://github.com/ravbhatnagar/azure-resource-manager-rpc/blob/master/Resource Provider API v2.0.md#crud-arguments-id).

Examples of action names include: "restartVM" or "listStorageKeys".

**Request Body**

    {
    "resourceDefinedProperty": "Resource defined value";
    }

All parameters for the action request should be contained in the request body – and not in the URL. This matches the OData and Azure REST guidelines and will avoid impacting the authZ checks.

#### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the action completed successfully. 202 (Accepted) can be returned to indicate that the action will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

If the resource group or a relevant resource does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will be specific to the resource provider and the action, but it \*must\* adhere to the REST CEC guidelines and be JSON by default.

### Subscription Wide Reads and Actions (i.e. GETs / POSTs)

Some data needs to be exposed in a read-only fashion across a subscription or tenant. The Resource Provider contract allows for this functionality but recommends caution when exposing it (since it requires a &quot;global&quot; endpoint for the RP &amp; does not support regional routing).

Examples include: available platform images for a subscription; available locations for their offer type; quotas or restrictions imposed on their subscription.

**Please review all instances where this API is used with the current owners of the RP API document. Manageable entities should \*never\* be updated at this level.**

#### Request

| Method | Request URI |
| --- | --- |
| GET/POST | https://<endpoint>/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/{rp-defined-uri}?api-version={api-version} |
| GET/POST | https://<endpoint>/providers/{resourceProviderNamespace}/{rp-defined-uri}?api-version={api-version} |

**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

**Request Headers**

Only headers common to all requests.

**Request Body**

Controlled by the resource provider (e.g. GETs should have no body; POSTs can have a body as part of the action).

#### Response

The response includes an HTTP status code, a set of response headers, and a response body if it applies.

**Status Code**

The resource provider should return 200 (OK) to indicate that the action completed successfully. 202 (Accepted) can be returned to indicate that the action will [complete asynchronously](http://sharepoint/sites/CIS/AzureRT/Shared%20Documents/Design%20Docs/Application%20Services/Resource%20Provider%20API%20v2.docx#_Asynchronous_operations).

If the Provider does not exist, 404 (NotFound) should be returned.

**Response Headers**

Headers common to all responses.

**Response Body**

The response body will be specific to the resource provider and the URL, but it \*must\* adhere to the REST CEC guidelines and be JSON by default.

### Exposing Available Operations (for client discovery)

As part of the management experience, clients (e.g. portal / CLI / powershell) need an ability to discover the available operations for a particular resource provider. The set of operations should include both registered and non-registered types (e.g. Virtual Machines and Disks).

This API is unique in that it is not scoped to a subscription – it is considered to be tenant-wide and should \*not\* vary based on particular subscriptions.

#### Request

| Method | Request URI |
| --- | --- |
| GET | https://&lt;endpoint&gt;/providers/{resourceProviderNamespace}/operations?api-version={api-version} |

**Arguments**

| Argument | Description |
| --- | --- |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

#### Response

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
| name | **Required**.The name of the operation being performed on this particular object. It should match the action name that appears in RBAC / the event service.  Examples of operations include:- <ul><li>Compute/virtualMachines/capture/action</li> <li>Compute/virtualMachines/restart/action</li> <li>Compute/virtualMachines/write</li> <li>Compute/virtualMachines/read</li> <li>Compute/virtualMachines/delete</li></ul> Each action should include, in order: <ul> <li> Resource Provider Namespace</li> <li> Type hierarchy for which the action applies (e.g. server/databases for a SQL Azure database)</li> <li>If an &quot;action,&quot; the custom action name (e.g. capture / restart / etc.)</li> <li>Read, Write, Action or Delete indicating which type applies.</li> <ul><li>If it is a PUT/PATCH on a collection or named value, Write should be used.</li> <li> If it is a GET, Read should be used.</li> <li>If it is a DELETE, Delete should be used.</li> <li>If it is a POST, Action should be used.</li></ul> </ul> As an example: <ul> <li>Compute/virtualMachines/extensions/capture/action</li> <ul> <li>Namespace: Microsoft.Compute</li> <li>Resource Type: virtualMachines/extensions</li> <li>Custom action name: capture</li> <li>Action verb: action (because it is a POST)</li></ul> <li>Compute/virtualMachines/extensions/write</li><ul><li>Namespace: Microsoft.Compute</li> <li>Resource Type: virtualMachines/extensions</li> <li>Custom action name: \*none\*</li> <li>Action verb: write (because it is a PUT/PATCH)</li> </ul> </ul> As a note: all resource providers would need to include the "{Resource Provider Namespace}/register/action" operation in their response. This API is used to register for their service, and should include details about the operation (e.g. a localized name for the resource provider + any special considerations like PII release). Example values can be seen below:<ul> <li>Resource: "Storage Resource Provider" </li> <li>Operation: "Registers the Storage Resource Provider"</li> <li>Description: "Registers the subscription for the storage resource provider and enables the creation of storage accounts." </li> </ul> |
| display | **Required.** Contains the localized display information for this particular operation / action. These value will be used by several clients for (1) custom role definitions for RBAC; (2) complex query filters for the event service; and (3) audit history / records for management operations. |
| display.provider | **Required**.The localized friendly form of the resource provider name – it is expected to also include the publisher/company responsible. It should use Title Casing and begin with "Microsoft" for 1st
 party services.  e.g. "Microsoft Monitoring Insights" or "Microsoft Compute." |
| display.resource | **Required**.The localized friendly form of the resource type related to this action/operation – it should match the public documentation for the resource provider. It should use Title Casing – for examples, please refer to the "name" section.  **This value should be unique for a particular URL type** (e.g. nested types should \*not\* reuse their parent&#39;s display.resource field). e.g. "Virtual Machines" or "Scheduler Job Collections", or "Virtual Machine VM Sizes" or "Scheduler Jobs" |
| display.operation  | **Required**.The localized friendly name for the operation, as it should be shown to the user. It should be concise (to fit in drop downs) but clear (i.e. self-documenting). It should use Title Casing and include the entity/resource to which it applies.   Prescriptive guidance:Read {Resource Type Name}Create or Update {Resource Type Name}Delete {Resource Type Name}<User Friendly Action Name> {Resource Type Name} As examples:Read Virtual MachineCreate or Update Virtual MachineDelete Virtual MachineRestart Virtual Machine  |
| display.description | **Required**.The localized friendly description for the operation, as it should be shown to the user. It should be thorough, yet concise – it will be used in tool tips and detailed views.  Prescriptive guidance for resources:Read any <display.resource>Create or Update any  <display. resource>Delete any <display. resource><User Friendly Action Name> any <display.resources>  |
| origin | **Optional.** The intended executor of the operation; governs the display of the operation in the RBAC UX and the audit logs UX.  Default value is "user,system"
| origin | initiator | Appears in RBAC UX | Appears inAudit Logs UX |
| --- | --- | --- | --- |
| user | end user / svc principal | Yes | Yes |
| system | Svc backend | No | Yes |
| user,system | end user / svc principal / svc backend | Yes | Yes |

  |
| properties | **Reserved for future use.  Optional.** |

### Check Name Availability Requests

Many resource providers have resource name uniqueness requirements – usually requiring global or local uniqueness.  The following APIs provide a common pattern for verifying name availability.

#### Request (for global uniqueness)

| Method | Request URI |
| --- | --- |
| POST | https://<endpoint>/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/checkNameAvailability?api-version={api-version} |

### Request (for local uniqueness)

| Method | Request URI |
| --- | --- |
| POST | https://<endpoint>/subscriptions/{subscriptionId}/providers/{resourceProviderNamespace}/locations/{location}/checkNameAvailability?api-version={api-version} |



**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| location | The location in which uniqueness will be verified. |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

**Request Body**

    {
    "name": "<resourceNameToVerify>",
    "type": "<resourceTypeUsedForVerification>"
    }

#### Response

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

<div id='addendum-id'/>
## Addendum

### Instrumentation and Tracing across services

Resource providers should associate the correlation Id and client request Id with all of their management operations.

This will enable end-to-end troubleshooting from the portal, through CSM and to the RP, via four key headers:

1. x-ms-client-request-id: associated with a logical action in the client; e.g. loading the portal monitoring part may have a single client request id for many calls to ARM (e.g. load VMs + load metric definitions + load metrics)
2. x-ms-correlation-id: associated with a logical action in ARM; e.g. deleting a resource group or running a template
3. x-ms-request-id: returned by the RP per request; typically maps to the RP's ActivityId
4. x-ms-routing-id: maps to ARM's activity id (which is not otherwise exposed). This maps to implementation boundaries in ARM / the platform –RPs should not use this as their ActivityId.

[http://sharepoint/sites/AzureUX/Sparta/Shared%20Documents/Specs/Ibiza\_CSM\_CorrelationIds.vsdx](http://sharepoint/sites/AzureUX/Sparta/Shared%20Documents/Specs/Ibiza_CSM_CorrelationIds.vsdx)

 ![Correlation IDs in Ibiza] (https://github.com/ravbhatnagar/testrepo1/blob/master/CorrelationIds.png)

### ETags for Resources

ETags may be returned for individual resources, and then sent via If-Match / If-None-Match headers for concurrency control. The resource provider is responsible for storing and validating ETags – the frontdoor will never inspect these values.

The behavior for ETags can be seen below:

| PUT | Resource does not exist | Resource exists |
| --- | --- | --- |
| If-Match = "" / absent | 201 Created | 200 OK |
| If-Match = "\*" | 412* Precondition Failed | 200 OK |
| If-Match = "xyz" | 412** Precondition Failed | 200 OK / 412 Precondition Failed |
| If-None-Match = "\*" | 201 Created | 412**** Precondition Failed |


| PATCH | Resource does not exist | Resource exists |
| --- | --- | --- |
| If-Match = "" / absent | 404 Not Found | 200 OK |
| If-Match = "\*" | 404** Not Found | 200 OK |
| If-Match = "xyz" | 404** Not Found | 200 OK / 412 Precondition Failed |

| DELETE | Resource does not exist | Resource exists |
| --- | --- | --- |
| If-Match = "" / absent | 204 No Content | 200 OK |
| If-Match = "\*" | 204*** No Content | 200 OK |
| If-Match = "xyz" | 204*** No Content | 200 OK / 412 Precondition Failed |

### Regional Endpoints

The Resource Provider should partition services across multiple regions in order to allow for continued service if there is a regional outage. It is recommended that the RP offer services in all Azure supported regions so that users may collocate interdependent resources within a resource group.

The RP should register all the regions that they support, and should provide a different regional endpoint for each region. This regional endpoint and its backing state/data should be isolated from the other regions in order to isolate failure within Azure. The RP-FD will proxy the request to the appropriate region based on the resource&#39;s location.

The resource provider should register regional DNS names for each regional endpoint. The naming of this region should follow the below convention:

1. <region>.<provider namespace>.azure.com
2. <region>.<subservice name>.<provider namespace>.azure.com

In a concrete form:

1. westus.cache.api.azure.com, eastus.cache.api.azure.com
2. westus.redis.cache.api.azure.com

### Nested Resources

The RPC supports registering "nested" resource types for an RP with this format:

 _{RPNS}/{TYPE1}/{NAME1}/{TYPE2}/{NAME2}._

The resource provider URIs are still expected to follow REST guidelines (e.g.: azure.com/subscriptions/{SubId}/resourceGroup/ {resourceGroup\_name}/providers/{namespace}/{type1}/{type1\_name}/{type2}/{type2\_name}

Please see example URLs for nested resource types below:

| PUT | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{namespace}/{resourceType}/{resourceName}/{nestedResourceType}/{nestedResourceName}?api-version={api-version} |
| --- | --- |
| GET | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{namespace}/{resourceType}/{resourceName}/{nestedResourceType}/{nestedResourceName}?api-version={api-version} |
| PATCH | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{namespace}/{resourceType}/{resourceName}/{nestedResourceType}/{nestedResourceName}?api-version={api-version} |
| DELETE | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{namespace}/{resourceType}/{resourceName}/{nestedResourceType}/{nestedResourceName}?api-version={api-version} |

### Resource Group Deletes

If the resource group containing resources is deleted, the RP will receive a DELETE call on each individual resource in that group. In some cases, the resources will have interdependencies and therefore can only be deleted in a certain order that RP-FD does not understand.

To address this, the RP-FD can simply ask each resource to delete in arbitrary order. If the resource refuses the deletion, then the CSM will revisit it after trying to delete the rest of the group&#39;s resources. It will continue to revisit resources until all resources are deleted, or there is no further delete progress (for example if a delete fails because of an ACL).

As a result, it is essential that the RPs follow proper REST guidelines when returning 2xx for a successful delete, and 4xx for a delete that is invalid (until a related resource is deleted first).

### Asynchronous Operations

Some REST operations can take a long time to complete. Althgouth REST is not supposed to be stateful, some operations are made asynchronouse while waiting for the state machine to create the resources, and will reply before the operation on resources are completed. For such operations, the following guidance applies.

### Creating or Updating Resources (PUT/PATCH)

The API flow should be to:

1. Respond to the initial PUT request with a 201 Created or 200 OK (per normal guidance);
2. Since provisioning is not complete, the PUT response body **MUST** contain a provisioningState set to a non-terminal value (e.g. &quot;Accepted&quot;, or &quot;Created&quot;);
3. **Optional** : The response headers may include a Azure-AsyncOperation header pointing to an Operation resource (as described below);
4. Future GETs on the resource that was created should continue to return a 200 Status Code and provisioningState field that is \*non-terminal\* as long as the provisioning is in progress;
5. After the provisioning completes, the provisioningState field should transition to one of the terminal states (as described below).
6. The provisioningState field should be returned on all future GETs, even after it is complete, until some other operation (e.g. a DELETE or UPDATE) causes it to transition to a non-terminal state.

### Delete Resource (DELETE)

The API flow should be to:

1. Respond to the initial DELETE request with a 202 Accepted;
2. The response headers **MUST** include a Location header that points to a URL where the ongoing operation can be monitored;
3. **Optional:** The response headers may include an Azure-AsyncOperation header pointing to an Operation resource (as described below).
4. If a provisioningState field is used for the resource, it **MUST** transition to a non-terminal state like &quot;Deleting&quot;;
5. If the DELETE completes successfully, the URL that was returned in the Location header **MUST** now return a 200 OK or 204 NoContent to indicate success and the resource **MUST** disappear.

### Call Action (POST {resourceUrl}/{action})

The API flow should be:

1. Respond to the initial POST request with a 202 Accepted;
2. The response headers **MUST** include a Location header that points to a URL where the ongoing operation can be monitored;
3. **Optional:** The response headers may include an Azure-AsyncOperation header pointing to an Operation resource (as described below).
4. If the POST completes successfully, the URL that was returned in the Location header **MUST** now return what would have been a successful response if the API completed (e.g. a response body / header / status code). It is acceptable for this to be a 200/204 NoContent if the action does not require a response (e.g. restarting a VM).

### ProvisioningState property

The provisioningState field has three terminal states: **Succeeded** , **Failed** and **Canceled**. If the resource returns no provisioningState, it is assumed to be **Succeeded**.

Each individual RP is able to define their own transitioning / ephemeral states that are set before the resource reaches these terminal states (e.g. "PreparingVMDisk", "MountingDrives", "SelectingHosts" etc.).

The basic functionality of the template orchestration engine and other clients is to:

1. PUT the resource to be created; and, then,
2. Poll at the resourceUri until the provisioningState enters a terminal state

before assuming that the resource creation has completed. In the case of the template orchestration engine, it would not create dependent resources until the resource creation is completed.

An example of the response body can be seen below:

**Response Body**

    {
    "location": "North US",
    "tags": {
      "key1": "value 1",
      "key2": "value 2"
     },

    "properties": {
    "provisioningState": "Succeeded",
    "comment: "Resource defined structure"

     },
    }

If the user does a PUT with provisioningState (e.g. after doing a GET), the resource provider should treat the field as a normal readonly property.

If the user provides a provisioningState matching the value \*on the server\*, the server should ignore it. If the user provides a provisioningState that does \*not\* match the value on the server, the resource provider should reject the call as a 400 BadReqeust.

### 202 Accepted and Location Headers

The asynchronous operation APIs frequently use the 202 Accepted status code and Location headers to indicate progress. The flow is described below:

1. Return HTTP code 202 (Accepted) with a Location header and, optionally, a Retry-After header. The time interval in the Retry-After header can only be specified in seconds, with a minimum of 10 seconds and a maximum of 10 minutes.
2. Clients invoke the URI specified in the Location header using the GET verb.
3. Clients should wait for the Retry-After interval, if it was specified, or the default of 60 seconds if it was not, before polling again.
4. If the operation is not complete, return 202 (Accepted) again with Location header and optionally an updated Retry-After header.
5. If the operation is complete, return the **exact same response** that would have been returned had the operation been executed synchronously.
6. If the 202 was returned in response to resource creation, the resource should \*not\* be visible until the async operation completes (i.e. GETs on the resource should return 404 and collection requests should not include the resource). If the resource should be visible, the provisioningState pattern should be used.

The Uri for the Location header can be either underneath the original request:

https://<endpoint>/subscriptions/{subscriptionId}/{Original-URL-Fo-Request}/operationresults/{operationId}&amp;api-version={api-version}

or underneath a subscription level operations URL:

https://<endpoint>/subscriptions/{subscriptionId}/ providers/{namespace}/locations/westus/operationresults/{operationId}&amp;api-version={api-version}

The _endpoint_ can be determined by the hostname of the URI in the _referrer_ header.

After this maximum time, clients will give up and treat the operation as timed out.

| Clients | Resource Provider |
| --- | --- |
| DELETE /…/resourcegroups/rg1 |   |
|   | 202 AcceptedLocation: /…/resourcegroups/rg1/operationresults/id1Retry-After: 60 |
| Waits 60 seconds |   |
| GET /…/resourcegroups/rg1/ operationresults/id1  |   |
|   | HTTP/1.1 202 AcceptedLocation: /…/resourcegroups/rg1/operationresults/id1 Retry-After: 10 |
| Waits 10 seconds |   |
| GET /…/resourcegroups/rg1/ operationresults/id1 |     |
|   | 204 NOCONTENT |



### Operation Resource format (returned by Azure-AsyncOperation header)

    {
    "id": "/subscriptions/id/locations/westus/operationsStatus/sameguid",
    "name": "sameguid",
    "status" : "RP defined values | Succeeded | Failed | Canceled",
    "startTime": "<DateLiteral per ISO8601>",
    "endTime": "<DateLiteral per ISO8601>",
    "percentComplete": <double between 0 and 100>
    "properties": {
        /\* The resource provider can choose the values here, but it should only be
           returned on a successful operation (status being "Succeeded"). \*/
    },
    "error" : {
        /\* This is the OData v4 format, used by the RPC and will go into the
         v2.2 Azure REST API guidelines \*/
        "code": "BadArgument",
        "message": "The provided database &#39;foo&#39; has an invalid username."
    }

    }

**The operation resource should be used for Azure-AsyncOperation header**. Location header should have different behavior described above.

The status values are similar to provisioningState – the transient / intermediate values can be service specific; however, the terminal values can be one of (1) Succeeded, (2) Failed or (3) Canceled. All other values imply that the operation is still running / being applied.

When reading the operation resource entity, the status code should always be 200. The response payload indicates if the async operation is still running or has completed (successfully or with a failure).

If the response status code is a 4xx or 5xx value, it indicates a failure in reading the _status_ but \*not\* in the underlying operation.

| Element name | Description |
| --- | --- |
| id | **Optional.** (but recommended)It should match what is used to GET the operation result. |
| name | **Optional.** (but recommended)It must match the last segment of the &quot;id&quot; field, and will typically be a GUID / system generated value. |
| status | **Required.** … |
| properties | **Optional** Like the properites envelope for resources, the resource provider can choose the values here. However, it should only be set if the status is Succeeded. |
| error | **Required if status == failed or status == canceled.** This is the OData v4 error format, used by the RPC and will go into the v2.2 Azure REST API guidelines.  The full set of optional properties (e.g. inner errors / details) can be found in the &quot;Error Response&quot; section. |
| error.code | **Required if status == failed or status == canceled.**  If status == failed, provide an invariant error code used for error troubleshooting, aggregation, and analysis. |
| error.message | **Required if status == failed.**   **Localized.**  If status == failed, provide an actionable error message indicating what error occurred, and what the user can do to address the issue. |
| startTime | **Optional.**  DateLiteral using ISO8601, per 1API guidelines. |
| endTime | **Optional.**  DateLiteral using ISO8601, per 1API guidelines. |
| percentComplete | **Optional.**  Double between 0 and 100. |

## Retrying REST Calls

The recommended pattern for REST clients is to retry calls that:

1. Return 408 indicating a request timeout;
2. Return a 5xx status code indicating a server failure (e.g. 500 InternalServerError; 503 Service Unavailable);
3. Experience a socket exception (e.g. DNS resolution failures; network drop; no listening socket).

The retry interval, strategy (e.g. exponential/linear) and max timeout should be defined by the _server_ and not the client. That allows various server workloads to advertise different retry policies.

## Designing Resources

The Azure Resource Provider contract and template language have special semantics around &quot;registered&quot; Azure resources – we call these **tracked resources**.

If these objects are addressable by URIs but not "registered", we call these **proxy only** resources to differentiate them. Resource providers also have the important option of structuring their JSON payloads, but not giving these objects uris. This pattern is referred to below as JSON-only resources. ** **

**Background REST philosophy**

1. Azure API guideline compliant and OData compliant where it makes sense.
2. APIs must be callable from any client implementation, language or framework.
3. Making things simple and regular for machine processing often makes things easier for humans to understand, even when it increases verbosity.
4. When we choose between understandable URLs and understandable templates, we should make the templates human understandable and the URLs machine consumable.
5. Everything that is possible from a template should be possible through imperative APIs, but not necessarily as easily and may require special client code (orchestration is an obvious example).

**Objects should**** be Tracked resources if:**

1. They are billable entities, including freemium models
2. Need to be orchestrated by the template execution engine
3. Related to above, they have dependencies on other resources

**Objects should be top-level resources if: **

1. They should be resources as per above
2. Their lifetime is independent of other resources (only dependent on the containing resource group)
3. If the objects have an independent lifetime but are not important to the model, they should only be top-level resources if no other design can be made to work.

**Objects should be nested resources if:**

1. They meet the guidelines for Azure resources above (billable, orchestration supported, taggable)
2. Their lifetime is dependent on a containing resource

**Objects should be proxy only resources if:**

1. They don&#39;t need to be Azure resources for one of the reasons above
2. if the objects/properties are required for the parent resource to be created, then they should \*not\* be Azure resources
3. It is important that they be simple to create in context of a containing resource.
4. The lifecycle of the resources are managed outside ARM (e.g. agent based discovery).
5. They are very common and would incur a performance overhead on the system (for example by cluttering the indices and GET resources calls)

**Objects should be JSON-only resources if:**

1. They do not need to be addressed independently by HTTP verbs
2. Logically should be managed with their container

**Comparison of Tracked Resources and proxy only Resources**

| ​ **Feature** | ​ **Tracked Resources** | ​ **Proxy only Resources** |
| --- | --- | --- |
| ​Understood by template processor | ​Yes | ​ Yes |
| Can be top-level resource | Yes | Only if global/single region |
| Defined JSON format to payload | ​Yes -- must comply with general Azure resource format (id, type, name, tags, properties, location etc.) | ​Yes -- must comply with general Azure resource format (id, type, name, properties, etc.) but no tags or location |
| Defined URL format | ​Yes -- must use providers/{namespace}/{typename} URL | ​Yes -- must use providers/{namespace}/{typename} URL |
| ​Tagging and Indexing supported | ​Yes | ​No |
| ​Billing supported     | ​Yes | ​No |
| ​Have their own URLs | ​Yes | ​Yes |
| ​​Can be PUT (created) with the parent in a single call | ​No - $batch/deep insert not available | ​​Yes, see deep insert recommendation |
| ​Supports RBAC | ​Yes -- based on URL     | ​ Yes -- based on URL |
| ​Actions are advertised and supported by RBAC experience (/reboot for example) | ​Yes | ​Optional |
| ​Supports targeted imperative GET | ​Yes | ​ Yes |
| ​Supports targeted imperative PUT, PATCH | ​Yes | ​ Yes |
| ​Supports targeted DELETE | ​Yes | ​Yes |
| ​DELETEd when parent is | ​Yes, governed by deletionPolicy in Manfiest | ​RP must implement cascading delete and/or validation |
| Independent lifetime from parent | ​DELETEd when parent is, but otherwise independent | ​ RP must implement cascading delete and/or validation, but otherwise independent |
| ​Supported by orchestration service         | ​Yes | ​ Yes |
| ​Can take dependencies (DependsOn, [reference] on other resources     | ​Yes     | ​Yes |
| ​Can be the target of dependencies from other resources | ​Yes | ​Yes |
| ​In template can take values from variables | ​Yes | ​Yes |
| ​In template can take values from other resources | ​Yes | ​Yes |
| ​Can be independently included in external templates | ​Yes | ​Yes |
| ​Can be versioned independently from parent     | ​Yes | ​Yes |

## Enumerating SKUs for an existing resource

In many cases, it is desirable for users to resize an existing resource.  However, only a certain subset of sizes available from a given resource provider may be applicable to a given resource – e.g. an A1 machine may be updatable to other A series VMs, but may not be convertible to D series.  This API exposes the valid SKUs for an existing resource.

### Request

| Method | Request URI |
| --- | --- |
| GET | https://<endpoint>/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}/skus?api-version={api-version} |

**Arguments**

| Argument | Description |
| --- | --- |
| subscriptionId | The subscriptionId for the Azure user. |
| resourceGroupName | The resource group name uniquely identifies the resource group within the user subscriptionId. |
| resourceType | The type of the resource – the resource providers declare the resource types they support at the time of registering with Azure. |
| resourceName | The name of the resource. |
| api-version | Specifies the version of the protocol used to make this request. Format must match YYYY-MM-DD[-preview|-alpha|-beta|-rc|-privatepreview]. |

**Request Headers**

Only headers common to all requests.

**Request Body**

Empty

### Response

The response includes an HTTP status code, a set of response headers, and a response body.

**Status Code**

The resource provider should return 200 (OK) to indicate that the operation completed successfully.

If the resource does not exist, 404 (NotFound) should be returned. For other errors (e.g. internal errors) use the appropriate HTTP error code.  If no skus are valid, return 200 + an empty value array.

**Response Headers**

Headers common to all responses.

**Response Body**

    {
    "value": [
        {
            "resourceType": "type for sku"
            "sku": {
                "name": "sku name",
                "tier": "sku tier"
            },

            "capacity": {
                "minimum": min,
                "maximum": max,
                "default": default,
                "scaleType": "automatic|manual|none"
            }
        },

        {
            "resourceType": "type for sku"
            "sku": {
                "name": "sku name",
                "tier": "sku tier"
            },

            "capacity": {
                "minimum": min,
                "maximum": max,
                "default": default,
                "scaleType": "automatic|manual|none"

            }
        }
    ]
    }

For a detailed explanation of each field in the response body, please refer to the request body description in the PUT resource section. The only GET specific properties are "name", "type" and "id"

| Field | Description |
| --- | --- |
| resourceType | Required, stringThe resource type that this object applies to. For example, for a database it'd be: Microsoft.SQL/servers/databases.   |
| sku | Required, objectThe exact set of keys that define this sku. This matches the fields on the respective resource. |
| sku.name | Required, stringThe name of the SKU. This is typically a letter + number code, such as A0 or P3 |
| sku.tier | Required, stringThe tier of this particular SKU. Typically one of: <ul> <li>Free</li> <li>Basic</li> <li>Standard</li> <li>Premium</li></ul>|
| capacity | Optional, objectIf the SKU supports scale out/in then the capacity object must be included. If scale out/in is not possible for the resource this may be omitted. |
| capacity.scaleType | Required, enumOne of: <ul><li>None – meaning the capacity is not adjustable in any way (e.g. it is fixed)</li> <li>Manual – the user must manually scale out/in</li> <li>Automatic – the user is permitted to scale this SKU in and out</li></ul>|
| capacity.minimum | Required if scaleType != none, integerThe lowest permitted capacity for this resource. Typically 0 or 1. |
| capacity.maximum | Required if scaleType != none, integerThe highest permitted capacity for this resource. This may vary per SKU, or it may be the same. |
| capacity.default | Required if scaleType != none, integerThe default capacity.  Generally, if the user omits setting the capacity, the RP would use this value. |

## Enumerating SKUs for a new resource

For new resources, SKUs are enumerated via ARM's metadata store.  This allows users to enumerate SKUs based on location, api-version, feature flags, and offerId filters.  The manifest schema used to express this data is available [here](http://sharepoint/sites/AzureUX/Sparta/Shared%20Documents/Specs/arm-sku-api.docx?web=1) **.**
