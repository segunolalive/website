---
layout: layouts/post.njk
title: RESTful API Design — PUT vs PATCH
metaTitle: RESTful API Design — PUT vs PATCH
metaDesc: ' When designing API endpoints, there’s always the need to specify what http method to use for CRUD (Create, Read/Retrieve, Update, Delete) operations. In this article, Segun explains the nuances of HTTP PUT and PATCH methods.'
socialImage: images/1-k3ztvzacfgysrw_0z_wgmg.jpeg
date: 2018-03-13T09:59:34.840Z
tags:
  - http
---
When designing API endpoints, there’s always the need to specify what http method to use for CRUD (Create, Read/Retrieve, Update, Delete) operations. Commonly, this is nailed down as:

* Create — **POST**
* Read/Retrieve — **GET**
* Update — **PUT/PATCH**
* Delete — **DELETE**

Given the mapping above, I won’t be surprised if you think PUT and PATCH do the same thing and are simply aliases but you couldn’t be further from the truth. It’s true that both methods update the resource at a location, but they do so differently. Note that I said “… update resource at a **LOCATION**". Why?

![solar-powered prefab Swedish homes. Source: \[https://inhabitat.com\](https://inhabitat.com)](https://cdn-images-1.medium.com/max/2000/1*K3ZtvzAcfGYsrw_0z_WGmg.jpeg)*solar-powered prefab Swedish homes. Source: <https://inhabitat.com>*

Everything on the internet is considered a resource, has a location **(URL)** and a corresponding identifier **(URI)**. We’ll be silent about the latter 🙂.

Let’s imagine the internet was a street, the houses on this street were prefabricated *(that’s a thing in the architectural world now)* and the house addresses were URLs. Also, let’s assume the street was divided into numbered plots with a house per plot such that house-1 was on plot-1 and so on. Remember, the houses are prefabricated so they just get dropped at their location. No onsite building required.

When you make a PUT request to https://internet-street.com/plot-1 with a prefabricated house, you’re saying “Please **PUT** this house in the location marked as **plot-1**”. That instruction searches through our street for the specified location and **replaces** the content at that location. If nothing is found at the location, it’ll simply **PUT** the resource at the location. In this case, a full prefabricated house. Thus, a **PUT** request always contains a full resource. This is necessary because, a necessary quality of PUT requests is idempotence — the quality of producing the same result even if the same request is made multiple times.

If our intent is to update the house at a location, for example, say we want to add a new window, we’d make a PUT request with a full *prefab* house that’s identical to the former only with the number of windows changed. That seems like an awful waste of bandwidth and it is. Here’s what the house and PUT request payload would look like.

```js
// House on plot 1
{
  address: 'plot 1',
  owner: 'segun',
  type: 'duplex',
  color: 'green',
  rooms: '5',
  kitchens: '1',
  windows: 20
}
```

```js
// PUT request payload to update windows of House on plot 1
{
  address: 'plot 1',
  owner: 'segun',
  type: 'duplex',
  color: 'green',
  rooms: '5',
  kitchens: '1',
  windows: 21
}
```

We could simply choose to send the data we need and have our server code update resources appropriately, but then, we’d loose the idempotence and its benefits such as reliable caching of responses on the network and reliable updates of resources from retries when the original request fails. PUT requests are particularly useful for major updates. So, how do we make minor updates to our resources (houses) whilst being good citizens of the web. Meet PATCH, the after-thought of REST architecture.

**EDIT**: *Responses to PUT requests are not cacheable. If a PUT request finds a response in a cache infrastructure, that response (cache entry) should be treated as stale.*

> Several applications extending the Hypertext Transfer Protocol (HTTP)  require a feature to do partial resource modification. The existing
>  HTTP PUT method only allows a complete replacement of a document.
>  This proposal adds a new HTTP method, PATCH, to modify an existing
>  HTTP resource.
> – [RFC 5789](https://tools.ietf.org/html/rfc5789)

A **PATCH** request on the other hand, is used to make changes to part of the resource at a location. That is, it **PATCHES** the resource — changing its properties. It is used to make minor updates to resources and it’s not required to be idempotent.

If we continue with our example above, we could easily add a new window to the house on plot 1 without having to ship a whole new house. All we have to do is ship the window and PATCH up the old house with a new window. Below is an example of the payload we’d have to send.

```js
// House on plot 1 (same as above)
{
  address: 'plot 1',
  owner: 'segun',
  type: 'duplex',
  color: 'green',
  rooms: '5',
  kitchens: '1',
  windows: 20
}
```

```js
// Patch request payload to update windows on the House
{
  windows: 21
}
```

Since PATCH is not idempotent, failed requests are not automatically re-attempted on the network. Also, if a PATCH request is made to a non-existent url e.g attempting to replace the front door of a non-existent building, it should simply fail without creating a new resource unlike PUT, which would create a new one using the payload. Come to think of it, it’ll be odd having a lone door at a house address 😄.

That about sums up the differences and use cases of both HTTP methods.

Special thanks to [Kayode Adeniyi](https://twitter.com/codekayy) and [Bolaji](https://twitter.com/Bolaji___) for editing this piece.