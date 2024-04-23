
# Boost Software Quality: Local Development with Azion CLI

## Introduction

[Azion CLI](https://www.azion.com/en/documentation/products/azion-cli/overview/) is an efficient tool for setting up local testing environments for edge functions. You can easily run your application locally by executing the `azion dev` command, kickstarting the local development process. This capability boosts software quality by testing and examining edge functions before integrating them into the live product, preventing errors, and unexpected behaviors.

## Key Benefits of Local Development with Azion CLI

-   *Error prevention*: test new features or modifications before they go live, reducing the risk of introducing bugs to the production system.
-   *Improved debugging*: debug code more effectively and quickly in a controlled environment as you can check logs in real time. 
-   *Performance optimization*: test the application's behavior under different loads or unique user scenarios.
-   *Security enhancements*: identify and rectify security vulnerabilities before the application goes live.
-   *Cost-effective*: prevent high resource-consuming post-production fixes, saving time and money by addressing potential problems before deployment.

---

## Prerequisites for Using Azion CLI

-   Azion CLI installed.
-   Node.js ≥ 18.
-   Access to the command line.

---

## Behind The Scenes: How Azion CLI local dev Works

### Dataflow

1.  Through Azion CLI, the user runs the `azion dev [flags]` command.
2.  Azion CLI invokes [Vulcan](https://github.com/aziontech/vulcan), which manages build and local development.
3.  Vulcan initializes a server and this server instantiates the runtime. This runtime supports a list of [Web APIs](https://www.azion.com/en/documentation/devtools/runtime-apis/javascript) and emulates the actual [Azion Edge Runtime](https://www.azion.com/en/documentation/devtools/runtime/overview/).

### Responsibilities

**Azion CLI**: serves as the primary point of interaction between the user and the system. It manages the entire application deployment process, ensuring a smooth and efficient workflow.

**Vulcan**: the engine that drives project initialization, building, and adaptation. It intelligently tailors the project based on the selected template, ensuring that the application is optimally configured for its intended use. For local development, Vulcan:

- Initiates a server.
- Instantiates the Edge Runtime.
- Handles changes in the source code, implementing hot reload.

---

## The Science Behind Edge Functions

Azion Edge Functions are used to enhance edge applications or to boost security in an edge firewall. Both run on Azion Edge Runtime, reduce latency, and help to implement a distributed approach. OK, but what's the difference between them?

The difference is how the functions are structured, let's dive deeper into that.

### Edge Application Functions

First, edge functions for edge applications work based on a fetch event. They're initialized with an `addEventListener` function, passing fetch as the event type, and an event. For example:

```js
 addEventListener('fetch',event=>{

   event.respondWith(handleRequest(event.request));

  });

```

Second, it’s necessary to define the behavior of the handleRequest function. This function has `event.request` as the signature. This data can be used later on to implement the necessary logic, such as:

- Manipulate cookies.
- Implement a behavior based on the HTTP request method (POST, GET, PUT, DELETE).
- Access request metadata.

>It's mandatory to return a response object with fetch.

The `handleRequest` function can be defined as:

```js
 consthtml=`<!DOCTYPE html>

 <body>

  <h1>Hello World</h1>

  <p>This markup was generated by Azion - Edge Functions.</p>

 </body>`

 asyncfunctionhandleRequest(request){

  returnnewResponse(html,{

   headers:{

    "content-type":"text/html;charset=UTF-8",

   },

  })

 }

```

In this example, the response will be the HTML content, declared previously by the const html. The headers can be manipulated and, in the example, the content type is set.

Complete Example:

```js
 consthtml=`<!DOCTYPE html>

 <body>

  <h1>Hello World</h1>

  <p>This markup was generated by Azion - Edge Functions.</p>

 </body>`

 asyncfunctionhandleRequest(request){

  returnnewResponse(html,{

   headers:{

    "content-type":"text/html;charset=UTF-8",

   },

  })

 }

 addEventListener('fetch',event=>{

   event.respondWith(handleRequest(event.request));

  });

```

[Learn more about edge functions for edge applications](https://www.azion.com/en/documentation/products/guides/edge-functions/first-steps/).

### Edge Firewall Functions

Edge functions for Edge Firewall operate based on a firewall event. They are initialized using the `addEventListener` function, passing `'firewall'` as the event type, and an event. For example:

```js 
 addEventListener('firewall',event=>{

   event.deny();

 });

```

In this instance, the system sends a denial in response to the firewall event that has been triggered. There could be other event reactions like `event.continue()`, and `event.drop()` depending on the specific circumstances or logic desired.

It's necessary to define the potential behaviors for different event reactions within the firewall event listener. The exact response depends on the condition met. For example:

-   Detect threat levels.
-   Block or rights list IP addresses.
-   Implement behaviors based on traffic patterns.

An example where the `event.deny` function is defined and used:

```js
 // Define a list of blocked IP addresses

 constblockedIPs=["192.0.2.0","203.0.113.0","198.51.100.0"]

 addEventListener('firewall',event=>{

   letip=event.request.clientIP;

   if(blockedIPs.includes(ip)){

     event.deny();

   }else{

     event.continue();

   }

 });

```

In this example, the firewall event listener checks the IP address that triggered the event against the list of blocked IPs. If the IP is on the list, the event is denied. If the IP isn't on the list, the event will continue processing. It showcases how you might use the `event.deny()`, `event.continue()`, and `event.drop()` in real application scenarios. You can also implement `event.respondWith(<Response>)`.

> Since it's not possible to execute any other method after the exectuion of an finishing event, it's recommended to use a return right after the event so it's clear nothing more will be executed.

[Learn more about edge functions for edge firewall](https://www.azion.com/en/documentation/products/secure/edge-firewall/edge-functions/).

---

## Getting Started: Testing Edge Applications Functions

To kick off a local testing environment:

1.  Open the terminal, create a new directory, and access it.
2.  In the command line, initiate an application through azion init
3.  Name your application or accept the suggestion.
4.  Select JavaScript as the template.

> You can start the application based on the template you want. For this example, JavaScript is used.

5.  Start the local development by answering yes to the interaction.
6.  Install the dependencies.
7.  After a build process, Azion will return the port to access the application.
8.  Send requests to the server and check the behavior.

>note: you can always terminate the terminal process and run `azion dev` to run the application locally. The changes applied to the function are rebuilt using *hot reload*.

The `azion dev` command starts up a local environment where you can test and monitor the functionality and efficiency of your edge function.

Azion edge functions run on Azion [Edge Runtime](https://www.azion.com/en/documentation/devtools/runtime/overview/) and have compatibility with Web APIs and Azion APIs.  

-   [Edge Functions First steps](https://www.azion.com/en/documentation/products/guides/edge-functions/first-steps/).
-   [Web APIs](https://www.azion.com/en/documentation/devtools/runtime-apis/javascript/).
-   [Complete list of Azion Edge Runtime Web APIs suppor](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/supported-types/)t.

### Testing Firewall Functions

If you've implemented firewall functions within your system, you'll need to consider special testing conditions.

To do so, you must run the `azion dev` command with the flag `--firewall`. It informs the system you're testing an edge firewall function.

-   [Edge function for Edge Firewall](https://www.azion.com/en/documentation/products/secure/edge-firewall/edge-functions/).
-   [Network List API](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/network-list/).
-   [Metadata API](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/metadata/).

---

## Conclusion


Using local testing environments improves the product development process and the software quality. Leveraging tools like Azion CLI makes it easier to build reliable, efficient, secure, and high-performing software solutions. By testing edge functions with the command `azion dev`, and optionally adding a `--firewall` flag when necessary, developers can navigate potential pitfalls before pushing their code into production.

---

Keywords

Azion CLI

Local development

Local testing environments

Software quality

Debugging

Performance optimization

Edge functions

Azion Edge Runtime

Security enhancements

Vulcan

JavaScript

Node.js

Event listener

Edge Applications

Edge Firewall

Firewall functions

Hot reload

Web APIs

Azion APIs

Fetch event

Firewall event
