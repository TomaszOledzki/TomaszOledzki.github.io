---
layout: post
title: BadRequest when Create Or Update Host Secret (aka Api Key) for Function App
description: This post explains how to handle BabRequest error when create or update Function App host secrets (aka Api Keys).
tags: appservice armapi powershell
---

When creating or updating host secret (aka ApiKey) for Function App using ARM Api, have you ever received a error message "Properties object is not present in the request body."? Well I did.

Here's full error response body I was receiving:
{% highlight json %}
{
    "Code": "BadRequest",
    "Message": "Properties object is not present in the request body.",
    "Target": null,
    "Details": [
        {
            "Message": "Properties object is not present in the request body."
        },
        {
            "Code": "BadRequest"
        },
        {
            "ErrorEntity": {
                "ExtendedCode": "51006",
                "MessageTemplate": "{0} object is not present in the request body.",
                "Parameters": [
                    "Properties"
                ],
                "Code": "BadRequest",
                "Message": "Properties object is not present in the request body."
            }
        }
    ],
    "Innererror": null
}
{% endhighlight %}


Message states, I'm sending incorrect body. So what I'm sending in the body? Just a simple JSON:
{% highlight json %}
{
  "Name": "ApiKey",
  "Value": "<my-secret-api-key>"
}
{% endhighlight %}


Let's see in the docs: [https://docs.microsoft.com/en-us/rest/api/appservice/webapps/createorupdatehostsecret#request-body](https://docs.microsoft.com/en-us/rest/api/appservice/webapps/createorupdatehostsecret#request-body).

According to thee docs, I should send just two parameters in the body "name" and "value":
<table>
    <thead>
    <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
        <tr>
            <td>name</td>
            <td>string</td>
            <td>Key name</td>
        </tr>
        <tr>
            <td>value</td>
            <td>string</td>
            <td>Key value</td>
        </tr>
    </tbody>
</table>

Looks easy. But ARM Api keeps telling me something is missing. Not so easy, though. How should correct JSON look like then?

Correct JSON should look like so:

{% highlight json %}
{
  "Properties": {
    "Name": "ApiKey",
    "Value": "<my-secret-api-key>"
  }
}
{% endhighlight %}

Thats it! Simple, isn't it?

Bonus: [how to create Function App Host Secret using PowerShell](/2020/07/25/function-app-create-or-update-host-secret).

Thanks for reading!
