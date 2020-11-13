# Azure Automatic Video Converter

An automatic video converter using Azure Medias Services (AMS) with Azure Functions & Azure Logic Apps, running in the cloud.


## Overview

Once the solution is all deployed and configure, to get starter you just need to upload a `.mov` file into the `movs` container inside the Azure Blob Storage. It can be done via the Azure portal or the Microsoft Azure Storage Explorer, or Azure CLI. It could easily change to use OneDrive, DropBox, or Google if you prefer.

After a few minutes (it depends on the size of you file), the file will be move to `movarchive` and you will found the converted equivalent in the `mp4s` container.

> ***Note:** This project uses some Azure Functions coming from the [Azure-Sample GitHub repo](https://github.com/Azure-Samples/media-services-v3-dotnet-core-functions-integration). That project ad different objectives but function were repurposed for this converter tool.*

## Deployment

### 1. Create an Azure Media Services account

Create a Media Services account in your subscription if don't have it already ([follow this article](https://docs.microsoft.com/azure/media-services/previous/media-services-portal-create-account?WT.mc_id=dotnet-0000-frbouche)).


### 2. Create a Service Principal

Create a Service Principal and save the password. It will be needed in step #4. To do so, go to the API tab in the account ([follow this article](https://docs.microsoft.com/azure/media-services/media-services-portal-get-started-with-aad?WT.mc_id=dotnet-0000-frbouche#service-principal-authentication)).

or execute this CLI command

```bash
az ams account sp create -a myAmsAccount -g myRG -n mySpName --password mySecret --role Owner
```

### 3. Make sure the AMS streaming endpoint is started

To enable streaming, go to the Azure portal, select the Azure Media Services account which has been created, and start the default streaming endpoint ([follow this article](https://docs.microsoft.com/azure/media-services/previous/media-services-portal-vod-get-started?WT.mc_id=dotnet-0000-frbouche#start-the-streaming-endpoint)).


### 4. Deploy the Azure functions

If not already done : fork the repo, deploy Azure Functions and select the right project (IMPORTANT!).

Note : if you never provided your GitHub account in the Azure portal before, the continuous integration probably will probably fail and you won't see the functions. In that case, you need to setup it manually. Go to your azure functions deployment / Functions app settings / Configure continuous integration. Select GitHub as a source and configure it to use your fork.

<a href="https://portal.azure.com/?WT.mc_id=dotnet-0000-frbouche#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FFBoucher%2FAzure-Automatic-Video-Converter%2Fmaster%2Fdeployment%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>
