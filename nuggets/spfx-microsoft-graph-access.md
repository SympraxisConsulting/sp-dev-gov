---
title: SharePoint Framework and accessing the Microsoft Graph
audience: Developer, Administrator, Architect
product-major: SharePoint Online
product-minor: NA
glossary-links: SPFx
---

# SharePoint Framework and accessing the Microsoft Graph
 
## Summary
Using the Microsoft Graph is a great way to surface data from Office 365 into a SharePoint framework solution. To access the Microsoft Graph it is preferred to use the `MSGraphClient` client object, which simplifies the authentication.

_**Note**: Currently the `MSGraphClient` object is in preview, and is not available for general availability._

_**Note**: It is not recommended to use the old `GraphHttpClient` object which never made it out of preview and has been deprectated as of SPFx v1.4.1._
 
## Main Content
One of the challenges of accessing the Microsoft Graph while in a SharePoint context has been to handle the authentication against the Microsoft Graph. By using the `MSGraphClient` client object authentication is handled for you, so all you have to concentrate on is reading and writing data.

When accessing the Microsoft Graph using the `MSGraphClient` client object you have to specify what resources you want to consume from the Microsoft Graph in the **webApiPermissionRequests** section of the _package-solution.json_ file under the _config_ folder of your solution. 

Typical resource requests are:

* User.ReadBasic.All
* Group.ReadWrite.All

_See [Microsoft Graph permissions reference](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) for a full list of all available permission scopes._

When installing a SharePoint Framework solution with resource requests, a tenant administrator has to grant access to those resources in order for it to start working in your solution. Permission requests for your SharePoint Framework solution are managed in the [SharePoint Administration Portal](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-aadhttpclient#manage-permission-requests).

## Security
When a call is executed towards the Microsoft Graph, the least amount of access right of the end-user and the requested resource scopes will take effect.

This means that if the requested resource scopes grants higher access rights than the end-user actually has, then the rights of the end-user takes precedence. A user will not be able to write to a file he/she has read-only access to even though the scope is be `Files.ReadWrite`. On the other hand if the end-user has write access to a file, then the scope `Files.Read` will take precedence.

## Pros
Surfacing data from other workloads in Office 365 via the SharePoint Framework is a powerful way to create solutions combining data from multiple data sources. Instead of creating back-end services to handle data access, you can easily create data-driven solution directly in your SharePoint Framework solutions.

## Cons
When a tenant administrator grants access to a resource in the Microsoft Graph for one SharePoint Framework solution, that resource is also available to **all other scripts**, including third party libraries you might be loading from a CDN without them being explicitly granted.

This means that if one web part is granted access to read and write to a users Planner tasks, then any other web part installed in your tenant or script running on your page can also read and write to the users Planner tasks, even though only requested read rights was requested for the solution.

Due to the way resource scopes are made available to SharePoint Framework solutions, it is important for an administrator to check what resources SharePoint Framework solutions requires, especially if coming from non-trusted third parties.

## Get Started
* [Use the MSGraphClient to connect to Microsoft Graph](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-msgraph
)
* [Consume the Microsoft Graph in the SharePoint Framework - Tutorial](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-aad-tutorial)