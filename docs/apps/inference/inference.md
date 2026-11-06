---
title: Inference Endpoints
description: Lifecycle Management of Inference Endpoints
tags:
  - inference endpoints
  - machine learning inference
  - deploy ML models
  - inference API
  - inference deployment
  - model endpoints
  - inference configuration
  - ML model serving
  - real-time predictions
  - inference lifecycle management
---


**Inference** is the process of using a trained AI/ML model to generate predictions from new data. It is central to machine learning workflows, enabling real time or batch decision making for use cases such as image classification, anomaly detection, or customer behavior prediction.

The platform provides an **Inference Endpoint Configuration** screen to deploy and manage models at scale. From a single interface, users can select a LLM from the provided list of LLMs, launch an Inference Endpoint and use it programmatically using OpenAI compatible APIs. 

This streamlines model operationalization, ensuring consistency, scalability, and secure access for ML engineers and data scientists managing production or development environments.

---


## Create Inference Endpoints

To create an inference endpoint, login into the self service portal. The page provides options to create and manage inference endpoints, which are predefined configurations designed to simplify and accelerate the deployment of machine learning models as APIs. 

![Hierarchy](img/inferences_homepage.png)

---

## New Inference Endpoint

To create a new Inference Endpoint,

- Select **Inference Endpoints** from the menu on the left of the console
- Click on **Inference Endpoints**
- Select a suitable inference service profile that suits your requirements

![Hierarchy](img/service-prof-list.png)

Once the profile is selected, provide the required details. A monthly estimate will be displayed.

- Provide a name for the Inference with an optional description
- Select the desired **Workspace** from the dropdown list
- Based on the configuration fields defined in the selected service profile and its associated template, users must provide the required details
- Click on **Deploy** to launch the service

![Hierarchy](img/inferences_inputs.png)

Depending on the size of the selected LLM, it can take a few minutes for the inference and associated software components to be deployed and ready for use.  

!!! info
    Users can deploy multiple inferences on an instance. The only constraint is whether the underlying instance has the resources required for all the inference.

- The instance initially displays a status of ***In Progress***. Upon successful deployment, the status updates to ***Success***

![Hierarchy](img/inferences_success.png)


---

## View Inference Endpoint 

Clicking on the Inference Endpoints menu will list of all the inference endpoints the user has access to. Note that inference endpoints may span different workspaces and different instances. To view details about a specific inference endpoint, users just need to click on the name of the inference.

![Inference in Browser](img/inf_views.png)


---

## Use & Access Inference Endpoint

Clicking on a specific Inference Endpoint will display access information of the endpoint to the end user. You will be presented with the following information: 

### Ready to use cURL Command 

An illustrative example is shown below 

```
curl -X POST https://gemma-3-27b-it-0ea8s.inference.democloud.com/v1/completions \
	-H "Content-Type: application/json" \
	-H "Authorization: Bearer <API Key>" \
	-d '{
	"model": "google/gemma-3-27b-it",
	"prompt": "What is the full form of LLM?",
	"max_tokens": "300"
	}'
```

### Access Token 

Users need to use this as the bearer token when they access the Inference endpoint programmatically. 

![Use Inference Endpoint](img/inf_access.png)

--- 

## Delete Inference Endpoint

To delete a Inference, users should click on the ellipses on the far right of the selected Inference and select delete.

![inference in Browser](img/delete_inferences.png)

!!! info
    Once deletion has been initiated, it cannot be stopped or reversed. Users can create a new Inference if required.

---
