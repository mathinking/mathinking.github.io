---
layout: single
title: "When MATLAB Production Server met Thunder Client for VS Code"
excerpt: "My new preferred way to do my MATLAB API testing for production code"
date:  2021-07-28 12:00:00 +0100
categories: [blog, en]
tags: [matlab, production]
classes: wide
toc: false
toc_label: In this post
toc_sticky: false

header: 
  teaser: /assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/server.jpg
  overlay_color: "#000"
  overlay_filter: "0.3"
  overlay_image: /assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/server.jpg
  caption: "Photo credit: [Taylor Vick](https://unsplash.com/@tvick?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
---

[Postman](https://www.postman.com/) has been my preferred choice for quite some time when testing any MATLAB code that I am bringing to production or showcasing others how to leverage the RESTful API for MATLAB Production Server. However, I must say that I am a huge [cURL](https://curl.se/) fan. It is almost always available on test machines and is easy to use in scripts. Besides, I have great esteem for [Daniel Stenberg](https://daniel.haxx.se/), the man behind cURL. 

Recently, I started to play with [Thunder Client](https://www.thunderclient.io/), a lightweight Rest API Client Extension for Visual Studio Code. This Extension facilitates the creation of REST API calls while staying at VS Code. Here's a short post to share my impressions.

# Install Thunder Client

Click your _Extensions_ button at VS Code or simply click `Ctrl + Shift + X`. Install the extension and restart VS Code: 

![Thunder Client - REST API Client Extension for VS Code](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-install.jpg)

# Start your Production Server

One simple way, scalable and aligned with cloud development best practices, is to deploy your MATLAB code via MATLAB Production Server. [MATLAB Production Server](https://www.mathworks.com/products/matlab-production-server.html) is an application server that operationalizes your MATLAB models or algorithms as APIs, so they get integrated with your enterprise IT/OT systems.

Once your algorithm has been developed and fully tested, you may package it as a CTF file using [MATLAB Compiler SDK](https://www.mathworks.com/products/matlab-compiler-sdk.html) and deploy it to your production system without having to recode the algorithm in a different language or create custom infrastructure. Deployed packages can be accessed by client applications written in Java®, .NET, Python®, C and C++ using client-specific libraries or through a HTTP/HTTPS endpoint using the RESTful API.

[Production Server Compiler App](https://www.mathworks.com/help/compiler_sdk/mps_dev_test/productionservercompiler.html) in MATLAB Compiler SDK facilitates the testing and packaging of algorithms. Once opened, you can add the desired files to _Production Server Compiler App_:

![Adding files to be deployed](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/production-server-compiler-app.jpg) 

# Test your MATLAB functions from VS Code
_Production Server Compiler App_ simplifies testing your MATLAB functions right from your desktop before moving them to your staging or production system. 

![Testing Client](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/production-server-compiler-app-testing.jpg)

You can then start a local application server to test your _to-be-deployed_ MATLAB functions:

![Start local Production Server](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/production-server-compiler-app-testing-start.jpg)

Back in VS Code, you can now create a new request using Thunder Client:

![New request Thunder Client](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-new-request.jpg)

It's relatively straightforward from here to create a [POST request](https://www.mathworks.com/help/compiler_sdk/mps_restfuljson/postsynchronousrequest.html), specify the URL and configure the HTTP request payload using JSON (_click image below to enlarge_):

[![HTTP Request to Production Server from Thunder Client](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-mps.jpg)](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-mps.jpg)

The key elements in building the payload, in this case, the Body of the HTTP POST Request, are: 

* `nargout`: the number of outputs that the client application is requesting from the deployed MATLAB function
* `rhs`: _Right Hand Side_ of the deployed MATLAB function, that is, the input arguments to the deployed MATLAB function, specified as an array of comma-separated values
* `outputFormat`: Specify whether the MATLAB output in the response should be returned using large or small JSON notation, and whether `NaN` and `Inf` should be represented as a JSON string or object

The response from the server (`lhs` -- _left hand side_--) is a JSON array where each element corresponds to an output of the deployed MATLAB function.

[MATLAB data types can be represented in JSON format](https://www.mathworks.com/help/mps/restfuljson/json-representation-of-matlab-data-types.html) to interchange data accross programming languages. 

The example below is yet another dummy example to show how to set up the POST request and interpret MATLAB Production Server's output. 

Given the MATLAB function:

![Add matrix example](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/addmatrix.jpg)

we can build the following input JSON payload, requesting two outputs from the server (sum and cumulative sum). 
```
{
    "nargout": 2, 
    "rhs": 
    [
        {
            "mwdata":[62,31,52,10,27,39],
            "mwsize": [2,3],
            "mwtype": "uint8"
        },
        {
            "mwdata":[46,18,7,3,13,11],
            "mwsize": [2,3],
            "mwtype": "uint8"
        }
    ],
    "outputFormat":
    {
        "mode":"large",
        "nanInfFormat":"string"
    }
}
```
We use again Thunder Client to complete the HTTP Request to MATLAB Production Server (_click image below to enlarge_):

[![HTTP Request to Production Server from Thunder Client](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-mps2.jpg)](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-mps2.jpg)

Note that the inputs sent to and outputs given by MATLAB should be interpreted in column-major format.

From here, you may obtain a code snippet to bring to your code or script:

![Thunder Client code snippet](/assets/images/2021/when-matlab-production-server-met-thunder-client-vs-code/thunder-client-snippet.jpg)


# My take

It's clear that Postman is indeed a complete tool with many exciting features. However, it has become more of an API development application and has lost some of its original lightweight API testing core. 

If you are looking for something lightweight to do your API testing that even integrates with VS Code, Thunder Client might be an option to explore! :zap: