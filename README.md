# How to Deploy WebSocket Application To Azure Container Registry Repository
- version: 1.0.0
- Last update: Jan 2025
- Environment: Docker and Azure CLI
- Prerequisite: [Access to Azure](#prerequisite)

## <a id="intro"></a>Introduction

This project shows a step-by-step guide to public a container application to Microsoft [Azure Container Registry](https://azure.microsoft.com/en-us/products/container-registry) repository. I am reusing the [WebSocket API](https://developers.lseg.com/en/api-catalog/real-time-opnsrc/websocket-api) [MRN Python examples application](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN) (RTO with Version 2 Authentication) as an example Docker image application. However, the concept and main logic can be applied to any technologies that support containerization. 

**Note**: 
- My Azure Account is based on my Visual Studio Enterprise Subscription service which is may be different from your Azure account type.
- The Azure Portal website UI/UX are subjected to change.

## <a id="intro_azure"></a>Introduction to Azure Container Registry

[Azure Container Registry](https://azure.microsoft.com/en-us/products/container-registry) is Microsoft own container hosing platform (the same as [Docker](https://www.docker.com/)'s [dockerhub](https://hub.docker.com/)). The repository handles private Docker/[OCI - Open Container Initiative](https://opencontainers.org/) images and artifacts with a fully managed, geo-replicated instance of OCI distribution. Developers can build, store and manage containers/artifacts to connect to across Azure services such as [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/products/kubernetes-service), [Azure App Service](https://azure.microsoft.com/en-us/products/app-service) and much more. 

The service also lets Developers/DepOps streamline building, testing, pushing, and deploying images with Tasks. The example is developers can targeting a container registry from a continuous integration and continuous delivery (CI/CD) tool such as [Azure Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/ecosystems/containers/acr-template) or [Jenkin](https://jenkins.io/).

![figure-1](images/image1_azure_container.png "Azure Container Registry Service")

This project shows the first step which is how to set up an image registry, upload an application image to Azure and how to pull it to a local environment. 

## <a id="prerequisite"></a>Prerequisite

This project requires the following software and account on your machine.

1. RTO Access credentials (Version 2 - Service ID) with MRN data permission.
2. [Microsoft Azure](https://azure.microsoft.com/en-us/get-started/azure-portal) account.
3. [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) application.
4. [Docker desktop](https://www.docker.com/products/docker-desktop/) application.
5. Internet connection.

Please contact your LSEG representative to help you to access the RTO account and MRN service.

## <a id="dev_detail"></a>Project Development Detail

Please check [Azure_devdetail.md](./Azure_devdetail.md) document.

##  <a id="next_steps"></a>Next Steps

That brings me to the end of this project. This project shows only step-by-step guide for the basic tasks such as set up Azure Container Registry repository, push your local application image to Azure, and pull an image back to your machine. There are more tasks that help you improve container lifecycle management like the following:

- Use the development pipelines to automate container building, testing, pushing and deploying when developers commit code to Git repository
- Scale your container registry to serve developers across regions
- Connect to other Azure services like [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/products/kubernetes-service) or [Azure App Service](https://azure.microsoft.com/en-in/products/app-service) or [Azure Container Apps](https://azure.microsoft.com/en-us/products/container-apps), and much more.

You can find more information on the following Azure resources pages 

- [Automate container image builds and maintenance with Azure Container Registry tasks]((https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview))
- [Azure Container Registry documentation](https://learn.microsoft.com/en-us/azure/container-registry/)
- [List of Azure Container Services](https://azure.microsoft.com/en-us/products/category/containers)

Please note that your application image does not limit to the [WebSocket API](https://developers.lseg.com/en/api-catalog/real-time-opnsrc/websocket-api)/[Real-Time APIs](https://developers.lseg.com/en/use-cases-catalog/real-time)  or Machine Readable News data, any applications that support containerization can be utilized Azure Container Registry service.

## <a id="reference"></a>Reference

For further details, please check out the following resources:

- [Real-Time WebSocket API page](https://developers.lseg.com/en/api-catalog/real-time-opnsrc/websocket-api) on the [LSEG Developer Community](https://developers.lseg.com/) website.
- [WebSocket API Quickstart page](https://developers.lseg.com/en/api-catalog/real-time-opnsrc/websocket-api/quick-start).
- [MRN Data Models Implementation Guide](https://developers.lseg.com/en/api-catalog/real-time-opnsrc/rt-sdk-java/documentation#mrn-data-models-implementation-guide) document.
- [MRN WebSocket Python example application](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN)
- [Introduction to Machine Readable News with WebSocket API](https://developers.lseg.com/en/article-catalog/article/introduction-machine-readable-news-elektron-websocket-api-refinitiv) article.
- [Machine Readable News (MRN) & N2_UBMS Comparison and Migration Guide](https://developers.lseg.com/en/article-catalog/article/machine-readable-news-mrn-n2_ubms-comparison-and-migration-guide) article.
- [Azure Container Registry page](https://azure.microsoft.com/en-us/products/container-registry)
- [Azure Container Registry documentation](https://learn.microsoft.com/en-us/azure/container-registry/)
- [Introduction to Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-intro)
- [Quickstart: Create an Azure container registry using the Azure portal](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-get-started-portal?tabs=azure-cli)
- [What is Azure Container Registry?](https://dev.to/makendrang/what-is-azure-container-registry-1f02) blog post.
- [How to install the Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
- [Automate container image builds and maintenance with Azure Container Registry tasks](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview).
- [Azure Container Registry documentation](https://learn.microsoft.com/en-us/azure/container-registry/).
- [List of Azure Container Services](https://azure.microsoft.com/en-us/products/category/containers).

For any question related to this article or the LSEG APIs, please use the Developer Community [Q&A Forum](https://community.developers.refinitiv.com/).
