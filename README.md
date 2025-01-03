# How to Deploy WebSocket Application To Azure Container Registry Repository

## Overview

This project shows a step-by-step guide to public a container application to Microsoft [Azure Container Registry](https://azure.microsoft.com/en-us/products/container-registry) repository. I am reusing the [MRN WebSocket Python example application](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN) (RTO with Version 2 Authentication) as an example application. However, the concept and main logic can be applied to any technologies that support containerization. 

## Introduction to Azure Container Registry

[Azure Container Registry](https://azure.microsoft.com/en-us/products/container-registry) is Microsoft own container hosing platform (the same as [Docker](https://www.docker.com/)'s [dockerhub](https://hub.docker.com/)). The repository handles private Docker/[OCI - Open Container Initiative](https://opencontainers.org/) images and artifacts with a fully managed, geo-replicated instance of OCI distribution. Developers can build, store and manage containers/artifacts to connect to across Azure services such as [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/products/kubernetes-service), [Azure App Service](https://azure.microsoft.com/en-us/products/app-service) and much more. 

The service also lets Developers/DepOps streamline building, testing, pushing, and deploying images with Tasks. The example is developers can targeting a container registry from a continuous integration and continuous delivery (CI/CD) tool such as [Azure Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/ecosystems/containers/acr-template) or [Jenkin](https://jenkins.io/).

![figure-1](images/image1_azure_container.png "Azure Container Registry Service")

This project shows the first step which is how to set up a registry, upload an application image and then how to pull it to a local environment. 

## Prerequisite  

This project requires the following software and account on your machine.

1. RTO Access credentials (Version 2 - Service ID) with MRN data permission.
2. [Microsoft Azure](https://azure.microsoft.com/en-us/get-started/azure-portal) account.
3. [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) application.
4. [Docker desktop](https://www.docker.com/products/docker-desktop/).
5. Internet connection.

Please contact your LSEG representative to help you to access the RTO account and MRN service.

## Application Container Preparation

Developers need the following files from the [WebSocket API Machine Readable News Example with Python](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN) project to create an application image with Docker.

1. [mrn_console_rto_v2.py](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN/blob/master/mrn_console_rto_v2.py) Python application file.
2. [requirements.txt](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN/blob/master/requirements.txt) Python dependencies configurations file.

### Docker Image Preparation

Next, create a file name ```Dockerfile``` as a blueprint for our image.

```Docker
#Build stage
ARG PYTHON_VERSION=3.11
ARG VARIANT=slim-bookworm
FROM python:${PYTHON_VERSION}-slim-bookworm AS builder 

LABEL maintainer="LSEG Developer Relations"

#Copy requirements.txt
COPY requirements.txt .

# install dependencies to the local user directory (eg. /root/.local)
RUN pip install --trusted-host pypi.python.org --trusted-host files.pythonhosted.org --trusted-host pypi.org --no-cache-dir --user -r requirements.txt

# Run stage
FROM python:${PYTHON_VERSION}-alpine3.20
WORKDIR /app

# Update PATH environment variable + set Python buffer to make Docker print every message instantly.
ENV PATH=/root/.local:$PATH \
    PYTHONUNBUFFERED=1

# copy only the dependencies installation from the 1st stage image
COPY --from=builder /root/.local /root/.local
COPY mrn_console_rto_v2.py .

#Run Python
ENTRYPOINT ["python", "mrn_console_rto_v2.py"]
```

Please note that if you are not in the controlled network environment (like our beloved ZScaler), you can replace the ```RUN pip instal ....``` line with the following Docker instruction instead.

```Docker
# install dependencies to the local user directory (eg. /root/.local)
RUN pip install --no-cache-dir --user -r requirements.txt
```
### Docker Image Testing

To test our newly created Dockerfile, developers can build a test image on their local machine with the ```docker build``` command. 

```bash
docker build -t rto_v2_ws_mrn_python .
```

Then verify if the build is succeed with the ```docker images``` command.

![figure-2](images/image2_mrn_image_local.png "Docker build local succeed")

You can check on [RTO Version 2 Authentication console Docker example](https://github.com/LSEG-API-Samples/Example.WebSocketAPI.Python.MRN/tree/master?tab=readme-ov-file#rto-version-2-authentication-console-example) section of the MRN example project to see how to run an application locally to test your RTO account and MRN subscription.

![figure-3](images/image3_mrn_run_local.png "Docker run local succeed")

That is all for the example image.

## Azure Container Registry Preparation

[tbd]

## Reference

- [Azure Container Registry page](https://azure.microsoft.com/en-us/products/container-registry)
- [Azure Container Registry documentation](https://learn.microsoft.com/en-us/azure/container-registry/)
- [Introduction to Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-intro)
- [Quickstart: Create an Azure container registry using the Azure portal](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-get-started-portal?tabs=azure-cli)
- [What is Azure Container Registry?](https://dev.to/makendrang/what-is-azure-container-registry-1f02) blog post.
- [How to install the Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
