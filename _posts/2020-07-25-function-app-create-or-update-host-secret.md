---
layout: post
title: Function App - List, Create or Update, Delete Api Keys
description: This post explains how to list, create, update or delete Function App host secrets (aka Api Keys).
tags: appservice armapi powershell
---

In previous [post](/2020/07/24/function-app-create-or-update-host-secret-error) I was complaining how I received a BadRequest error when trying to create or update host secret in Function App using ARM Api. But how I'm actually doing this?

One way is to use Postman and call ARM Api. I'm calling ARM Api using PowerShell Invoke-WebRequest cmdlet in my scripts and then using this in CI/CD to create/update/get/delete api keys on Function Apps in my Azure Tenant.

Actually I'm and following instructions in the docs:
- List: [https://docs.microsoft.com/en-us/rest/api/appservice/webapps/listfunctionsecrets](https://docs.microsoft.com/en-us/rest/api/appservice/webapps/listfunctionsecrets)
- Create/Update: [https://docs.microsoft.com/en-us/rest/api/appservice/webapps/createorupdatehostsecret#request-body](https://docs.microsoft.com/en-us/rest/api/appservice/webapps/createorupdatehostsecret#request-body). 
- Delete: [https://docs.microsoft.com/en-us/rest/api/appservice/webapps/deletehostsecret](https://docs.microsoft.com/en-us/rest/api/appservice/webapps/deletehostsecret)

And here's is a part of my code. Also I'm describing [here](/2020/07/24/function-app-create-or-update-host-secret-error) why I'm building JSON body (variable $body) in this way for Create/Update request.

{% gist 1c186db495d66df9dbddd017b4bf2c1c %}

I'm using 'GetToken' function to acquire current session authentication token. Code for the function is [here](/2020/07/26/gettoken-function).

Thanks for reading!