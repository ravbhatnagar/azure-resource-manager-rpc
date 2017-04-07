# Common API Details
- [Proxy Request Header Modifications] (#proxy-request-header-modifications) </br>
- [Client Request Headers] (#client-request-headers) </br>
- [Request Query Parameters] (#request-query-parameters) </br>
- [Case Insensitivity for Requests] (#case-insensitivity-for-requests) </br>
- [Client Request Timeout] (#client-request-timeout) </br>
- [Request Throttling] (#request-throttling) </br>
- [Common API Response Details] (#common-api-response-details) </br>

## Proxy Request Header Modifications ##

The resource provider proxy will preserve all the client requests headers, with the exception of modifications per the details below. The headers below are reserved and cannot be set by clients.


| Header                                       | Description |  1st or 3rd Party |
| :------------------------------------------- | :----------------| :---------------------|
| referer | Always added. Set to the full URI that the client connected to (which will be different than the RP URI, since it will have the public hostname instead of the RP hostname).This value can be used in generating FQDN for Location headers or other requests since RPs should not reference their endpoint name. |  1st and 3rd party |
| authorization | Always removed/changed. The authorization used by the client to the proxy will be different than the authorization used to communicate from the proxy to the resource provider. | 1st and 3rd party |
| x-ms-correlation-request-id | Always added. Specifies the tracing correlation Id for the request; the resource provider \*must\* log this so that end-to-end requests can be correlated across Azure. | 1st and 3rd party | 
| x-ms-client-ip-address | Always added . Set to the client IP address used in the request; this is required since the resource provider will not have access to the client IP. | 1st and 3rd party |
| x-ms-client-principal-name | Always added. Set to the principal name / UPN of the client JWT making the request. | 1st party only |
| x-ms-client-principal-id | Added when available. Set to the principal Id of the client JWT making the request. Service principal will not have the principal Id. | 1st party only |
| x-ms-client-tenant-id | Always added. Set to the tenant ID of the client JWT making the request. | 1st party only |
| x-ms-client-audience | Always added. Set to the audience of the client JWT making the request. | 1st party only |
| x-ms-client-issuer | Always added. Set to the issuer of the client JWT making the request. | 1st party only |
| x-ms-client-object-id | Always added. Set to the object Id of the client JWT making the request. Not all users have object Id. For CSP (reseller) scenarios for example, object Id is not available. | 1st party only |
| x-ms-client-app-id | Always added. Set to the app Id of the client JWT making the request. | 1st party only |
| x-ms-client-app-id-acr | Always added. Set to the app Id acr claim of the client JWT making the request. This is the application authentication context class reference claim which indicates how the client was authenticated. | 1st party only |
| x-ms-client-authorization-source | Always added. Specifies the authorization source of the token. It&#39;s value can be NotSpecified, Legacy, RoleBased, Bypassed, Direct and Management. | 1st party only |
| x-ms-client-identity-provider | Always added. Set to the identity provider of the client JWT. |1st party only |
| x-ms-client-wids | Always added. Set to the wids of the client JWT. These identify the admins of the tenant which issued the JWT. | 1st party only |
| x-ms-client-authentication-methods | Always added. Set to the authentication method references of client JWT. | 1st party only|

## Client Request Headers ##

Any non-reserved headers provided by the client will pass as-is to the resource provider. All requests to resource providers may include the following standard headers and \*must\* be supported:

| Header | Description |
| --- | --- |
| Content-Type | Set to application/json. This header is not sent in requests that don&#39;t have any content, such as all GET calls. |
| Accept-Language | Specifies the preferred language for the response; all RPs should use this header when generating error messages or client facing text. |
| x-ms-client-request-id | Caller-specified value identifying the request, in the form of a GUID with no decoration such as curly braces (e.g. client-request-id: 9C4D50EE-2D56-4CD3-8152-34347DC9F2B0). If the caller provides this header – the resource provider \*must\* log this with their traces to facilitate tracing a single request.If specified, this will be included in response information as a way to map the request if "x-ms-return-client-request-id"; is specified as "true". |
| x-ms-return-client-request-id | Optional. True or false and indicates if a client-request-id should be included in the response. Default is false. |

## Request Query Parameters ##

ARM will proxy request parameters (e.g. $filter; $expand; $skipToken; etc.) as-is to the Resource Providers. It will not delete, modify or add any query parameters before relaying the request.

## Case Insensitivity for Requests ##

When satisfying incoming requests, it is assumed that the following values are stored / indexed / compared in a case \*insensitive\* way:

- Resource group name
- Resource name
- Other names of entities in the URL, even if they are not resources.

## Client Request Timeout ##

Requests proxied to the resource provider are made with a client timeout of 60 seconds. If request take more than 60 seconds please consider using asynchronous request/response pattern.

The resource provider must respond within that time interval or the client will receive a 504 (timeout) error code and will not see the response from the RP.

## Request Throttling ##

ARM provides subscription level throttling. More details on these limits can be found [here] (https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/#overview)

## Common API Response Details ###

<div id='res-headers-id'/>
### Response Headers ###

All responses from resource providers should include the following headers:

| Header | Description |
| --- | --- |
| Content-Type | Set to application/json. This header is not required in responses that don&#39;t have any content. |
| Date | The date that the request was processed, in RFC 1123 format. |
| x-ms-request-id | A unique identifier for the current operation, service generated.All the resource providers \*must\* return this value in the response headers to facilitate debugging. |

All long running operations response details are described below.

### Error Response Content ###

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

### Max Response Size ###

In all the calls that ARM makes to the resource provider, the maximum size of a response that ARM will accept from the resource providers is 4 MB.

Any response greater than 4 MB in size will be dropped by ARM, and **500 Internal Server Error** will be returned to the client.  In general, APIs exposed by the resource provider should be designed to transmit relatively little data in keeping with the management nature of the API.

### Transfer-Encoding ###

Chucked transfer encoding is supported and can be used for larger payloads.

### Redirecting the Client ###

The Resource Provider may return a 307 response code to the customer if they want to expose a direct URL / host (with no proxy) to the user. As an example – when downloading a large file, the RP may return a 307 to a URL on storage to download that file.

The Azure Resource Manager will \*not\* follow any redirects and will instead proxy them directly back to the client.
