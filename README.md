# Azure Resource Manager Resoure Provider Contract (RPC)

This document covers the API contract that must be implemented by each Azure Resource Provider in order to onboard to the Azure management API surface (as well as RBAC, tags, and templates).

The intended audience of this document is any service who wants to onboard to Azure as a resource provider. The document is covered into five major sections. The first section covers the request and respose details common to all APIs. It includes information around the headers, client timeout, throttling, response size limitations etc. The second section covers the details of APIs around subscription lifecycle management for a particular resource provider. The next section covers the create, update, delete and read APIs that needs to be implemented for the resources exposed by the provider. The fourth section covers APIs or resources which will not be managed by Azure Resource Manager (ARM) but will be proxied directly to the resource provider. The last section covers details on various things like asynchronous operations, tracing requests, guidance on designing resources and so on.

## Table of Contents

1. [Common API Details] (Common API Details.md) <br/>
2. [Subscription Lifecycle API Reference] (Subscription Lifecycle API Reference.md) <br/>
3. [Resource API Reference] (Resource API Reference.md)
4. [Proxy API Reference] (Proxy API Reference.md)
5. [Addendum] (Addendum.md)
