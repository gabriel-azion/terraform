---
layout: page-documentation-md
title: Azion Preview Deployment
description: Azion Preview Deployment makes it possible for you to preview the behavior of your edge functions before they go to production.
meta_tags: edge, javascript
namespace: documentation_products_edge_functions_runtime_preview_deployment
permalink: /documentation/products/edge-application/edge-functions/runtime-api/preview-deployment/
permalink_pt-br: /documentacao/produtos/edge-application/edge-functions/runtime-api/preview-deployment/
---

# Azion Preview Deployment

**Azion Preview Deployment** makes it possible for you to preview the behavior of your edge functions before they go to production. New possibilities are unlocked when using the Preview, such as:

- Test different flows based on the http method provided.
- See the outcome of an HTML page.
- Return data in JSON.

---

## How does Azion Preview Deployment work?

Azion Preview Deployment depends on an auxiliar function inside your source code. This function is called `PreviewProvider`, and it's responsible for debugging and simulating a request, returning the outcome to be rendered. The `PreviewProvider` function is represented as:

```javascript
    function PreviewProvider<PreviewProvider>(args){
        var request ={
            body:{},
            headers{},
            method: "GET",
            redirect: ""
        }
        return handleRequest(request)
    }
```

>**Note**: without the `PreviewProvider` function, it isn't possible to visualize the preview.

Now, with your simulated request running, you're able to set different behaviors to your function, based on all properties available inside the request variable, such as:

```javascript
    async function handleRequest(request){
        switch (request.Method){
            case 'GET':
             return new Response(html,{
                headers:{
                    "content-type":"text/html:charset=UTF-8",
                }
             })
        }
    }
```

In this code snippet, it's defined that if a `GET` request is called, it returns the `HTML` var, containing the html to be output, and set its content type as required to perform this action.

### API Builder

It's also possible to build APIs and have the outcome based on the request method. For example:

- You can have an object in `JSON` as response, if the request is a `POST`, by altering the `content-type` header and returning the object using the `JSON.stringify()` function.

- In case the request is a `GET`, and you wish to return an HTML page, the `content-type` should be set as `text/html:charset=UTF-8`. The response is going to be presented already rendered on the preview.

Example:

```javascript
    async function handleRequest(request){
        switch (request.Method){
            case 'POST':
             return new Response(objectList,{
                headers:{
                    "content-type":"application/json",
                }
             })
            case 'GET':
             return new Response(html,{
                headers:{
                    "content-type":"text/html:charset=UTF-8",
                }
            })
        }
    }
```

The output is shown right next to the code editor. It's possible to open it on a different tab as well, clicking on the **open** button.

---

## Preview Provider and ChatGPT

The ChatGPT integration helps you to boost your productivity and, alongside the Preview Deployment, enables more analytical implementations, making it possible to test and see new ideas on the fly. Take a look at [Edge Functions Chat GPT integration]({% tl documentation_products_edge_functions_runtime_ai_integration %}).

---

## Implementation

Here are some implementations of the Preview Deployment tool:

| Implementation | Description |
| --- | --- |
| [How to build an API with Edge Functions and ChatGPT]() | See how to build an API and have its responses returned in JSON, with the help of ChatGPT |

---

## Related documentation

- [Edge Functions Code Editor]({% tl documentation_products_edge_functions_runtime_code_editor %})
- [Edge Functions ChatGPT integration]({% tl documentation_products_edge_functions_runtime_ai_integration %})
- [Edge Functions - JavaScript Runtime APIs]({% tl documentation_products_edge_functions_runtime_apis_javascript %})
- [Edge Functions]({% tl documentation_products_edge_functions %})
- [Edge Functions on Edge Firewall]({% tl documentation_products_edge_functions_firewall %})

---

Didn’t find what you were looking for? [Open a support ticket](https://tickets.azion.com/).
