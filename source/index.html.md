---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Multiverse API!



# Authentication

> To authorize, use this `x-api-key` header:



```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "x-api-key: <API_KEY>"
```

> Make sure to replace `API_KEY` with your API key.

Multiverse uses API keys to allow access to the API. You can register a new Multiverse API key at our [developer portal](http://example.com/developers).

Multiverse expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-api-key: API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>


# Projects


## Project Object

> PROJECT OBJECT

```json
{
  "project_id":"blahblah",
  "name":"products listing project",
  "description": "My first project",
  "created_at":123456,
  "updated_at":23456
}
```

### Attributes

Attribute | Description
--------- | -----------
project_id | Unique identifier for the project
name | Project name
description | A short explainer about the project
created_at | Time at which the project was created (Measured in seconds since the Unix epoch)
updated_at | The last time the project was updated (Measured in seconds since the Unix epoch). When creating a project, updated_at is the same as created_at



## Create a project

```shell
curl -X POST "https://<GLOBAL_DOMAIN>/projects"
-d description="My First Project!"
-d name="Project name"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "name":"products listing project",
  "description": "My first project",
  "created_at":123456,
  "updated_at":23456
}
```

### Parameters

`POST https://<GLOBAL_DOMAIN>/projects`

Parameter | Description
--------- | -----------
description (optional) | A short explainer about the project.
name (optional) | Project name


## Retreive a single project

```shell
curl -X GET "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "name":"products listing project",
  "description": "My first project",
  "created_at":123456,
  "updated_at":123456
}
```

Retreives the details of a single project. Supply the unique ID of the project as a URL parameter and we'll return the corresponding Project information

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID returned from your previous request for creating a project



## Update a project

```shell
curl -X PUT "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>"
-d description="My First updated Project!"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "name":"products listing project",
  "description": "My First updated Project!",
  "created_at":123456,
  "updated_at":134567
}
```

Update an existing project. You can change its name and/or description.

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID returned from your previous request for creating a project

### Body Parameters

Parameter | Description
--------- | -----------
description (optional) | A short explainer about the project.
name (optional) | Project name



# Pages


## Page Object

> PAGE OBJECT

```json
{
  "project_id":"a1s2d3",
  "page_id":"f5g6h8",
  "url": "https://example.com/product-page",
  "description":"My first page!",
  "assets":["https://assets.example.com/image1.jpg","https://assets.example.com/image2.gif","https://assets.example.com/image3.png"],
  "experiments":[{"<Experiment_object>"},{"<Experiment_object>"}],
  "created_at":123456,
  "updated_at":23456
}
```

### Attributes

Attribute | Description
--------- | -----------
project_id | Unique identifier for the project where the page is created under
page_id | Unique indentifier of the page you like to optimize
url | The address of the page to optimize
description | A short explainer on the page (e.g., product_page>Women , homepage)
assets | A list of URLs of assets found on the page
experiments | A list of Experiment objects that were already created for this page
created_at | Time at which the page was created (Measured in seconds since the Unix epoch)
updated_at | The last time the page was updated (Measured in seconds since the Unix epoch). When creating a page, updated_at is the same as created_at



## Create a page

```shell
curl -X POST "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages"
-d page_url="https://mysite.com/my-page"
-d description="page description"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "page_id":"a1s2d3",
  "url":"https://mysite.com/my-page",
  "description": "My first page!",
  "assets":["https://assets.mysite.com/image1.jpg","https://assets.mysite.com/image2.gif"],
  "created_at":123456,
  "updated_at":23456
}
```

### Parameters

`POST https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages`

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project

### Body Parameters

Parameter | Description
--------- | -----------
page_url (required) | The address of the page to optimize
description (optional) | A short explainer of the page 


## Retreive a single page

```shell
curl -X GET "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "page_id":"<PAGE_ID>",
  "url": "https://example.com/product-page",
  "description":"My first page!",
  "assets":["https://assets.example.com/image1.jpg","https://assets.example.com/image2.gif","https://assets.example.com/image3.png"],
  "experiments":[{"<Experiment_object>"},{"<Experiment_object>"}],
  "created_at":123456,
  "updated_at":23456
}
```

Retreives the details of a single page. It also includes assets_urls and already created experiments. When an experiment is created, its asset URL is removed from assets_urls list. Supply the unique ID of the project as a URL parameter and we'll return the corresponding Project information

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page returned from the previous call for creating a page



## Update a page

```shell
curl -X PUT "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>"
-d description="My First updated Page!"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "name":"products listing project",
  "description": "My First updated Project!",
  "assets":["https://assets.example.com/image1.jpg","https://assets.example.com/image2.gif","https://assets.example.com/image3.png"],
  "experiments":[{"<Experiment_object>"},{"<Experiment_object>"}],
  "created_at":123456,
  "updated_at":134567
}
```

Update an existing page. You can change its name and/or description.

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page returned from the previous call for creating a page

### Body Parameters

Parameter | Description
--------- | -----------
description (optional) | A short explainer about the project.
url (optional) | The page address to refresh

# Experiments 

## Experiment Object

> EXPERIMENT OBJECT

```json
{
  "project_id":"a1s2d3",
  "page_id":"f5g6h8",
  "experiment_id":"j6k7l89",
  "url": "https://assets.mysite.com/image1.jpg",
  "weight": 1,
  "is_live":true,
  "is_original":true,
  "created_at":123456,
  "updated_at":23456
}
```

### Attributes

Attribute | Description
--------- | -----------
project_id | Unique identifier for the project where the page is created under
page_id | Unique indentifier of the page you like to optimize
experiment_id | Unique indentifier of the asset to do the A/B testing on. This original asset acts as the 'control group' of the experiment.
url | The URL of the asset (as it appears on the page)
weight | Control the importance of an experiment or variation
is_live | whether the experiment is currently live on the page
created_at | Time at which the experiment was created (Measured in seconds since the Unix epoch)
updated_at | The last time the experiment was updated (Measured in seconds since the Unix epoch). When creating an experiment, updated_at is the same as created_at

## Create an experiment

```shell
curl -X POST "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>"
-d url="https://assets.mysite.com/image1.jpg"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "page_id":"a1s2d3",
  "experiment_id":"j6k7l89",
  "url":"https://assets.mysite.com/image1.jpg",
  "is_live":true,
  "is_original":true,
  "created_at":123456,
  "updated_at":23456
}
```

### Parameters

`POST https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>`

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page (where the asset is currently on)

### Body Parameters

Parameter | Description
--------- | -----------
url (required) | The asset URL. This should be the same as the URL currently live in the page
is_live | Boolean parameter. Whether to activate this experiment. Default:true
weight | Number. Assign weight to an asset to control the frequency of its requests


## Retreive a single experiment

```shell
curl -X GET "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "page_id":"<PAGE_ID>",
  "experiment_id":"<EXPERIMENT_ID>",
  "url": "https://assets.mysite.com/image1.jpg",
  "weight":20,
  "is_live":true,
  "is_original":true,
  "created_at":123456,
  "updated_at":23456
}
```

Retreives the details of a single experiment. 

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page (where the asset is currently on)
EXPERIMENT_ID | The unique ID of the experiment returned from the previous call for creating an experiment



## Update an experiment

```shell
curl -X PUT "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>"
-d url="https://assets.mysite.com/image1-new.jpg"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "page_id":"<PAGE_ID>",
  "experiment_id":"<EXPERIMENT_ID>",
  "url": "https://assets.mysite.com/image1-new.jpg",
  "weight":20,
  "is_live":true,
  "is_original":true,
  "created_at":123456,
  "updated_at":23456
}
```

Update an existing experiment. Available fields for update are url, is_live and weight.

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page (where the asset is currently on)
EXPERIMENT_ID | The unique ID of the experiment returned from the previous call for creating an experiment

### Body Parameters
Required to specify at least one of the following parameters

Parameter | Description
--------- | -----------
url (optional) | The page address to refresh
is_live (optional) | Boolean parameter. Whether to activate this experiment. Default:true
weight (optional) | Number. Assign weight to an asset to control the frequency of its requests


# Variations 

## Variation Object

> VARIATION OBJECT

```json
{
  "project_id":"a1s2d3",
  "page_id":"f5g6h8",
  "experiment_id":"j6k7l89",
  "variation_id":"lop90oi",
  "url": "https://assets.mysite.com/image2.jpg",
  "weight": 1,
  "is_live":true,
  "is_original":false,
  "created_at":123456,
  "updated_at":23456
}
```

### Attributes

Attribute | Description
--------- | -----------
project_id | Unique identifier for the project where the page is created under
page_id | Unique indentifier of the page you like to optimize
experiment_id | Unique indentifier of the original asset. The variation is added as one of the options for the specific experiment
variation_id | Unique identifier of the asset 
url | The URL of the asset you'd like to add as a variation
weight | Control the frequency of this variation to be requested for a specific experiment. Higher number = higher chances for selecting this asset as an alternative to the original.
is_live | whether the experiment is currently live on the page
is_original | Always set to false because it's not the original asset
created_at | Time at which the experiment was created (Measured in seconds since the Unix epoch)
updated_at | The last time the experiment was updated (Measured in seconds since the Unix epoch). When creating a variation, updated_at is the same as created_at

## Create a variation

```shell
curl -X POST "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>/variations"
-d url="https://assets.mysite.com/image2.jpg"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"blahblah",
  "page_id":"a1s2d3",
  "experiment_id":"j6k7l89",
  "variation_id":"lop90oi",
  "url":"https://assets.mysite.com/image2.jpg",
  "is_live":true,
  "is_original":false,
  "created_at":123456,
  "updated_at":23456
}
```

### Parameters

`POST https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>/variations`

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | Unique ID of the project
PAGE_ID | Unique ID of the page
EXPERIMENT_ID | Unique ID of the experiment (the control group for the variation)

### Body Parameters

Parameter | Description
--------- | -----------
url (required) | The asset URL for the new variation
is_live | Boolean parameter. Whether to activate this variation. Default:true
weight | Number. Assign weight to an asset to control the frequency of its requests


## Retreive a single variation

```shell
curl -X GET "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>/variations/<VARIATION_ID>"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "page_id":"<PAGE_ID>",
  "experiment_id":"<EXPERIMENT_ID>",
  "variation_id":"lop90oi",
  "url": "https://assets.mysite.com/image2.jpg",
  "weight":20,
  "is_live":true,
  "is_original":false,
  "created_at":123456,
  "updated_at":23456
}
```

Retreives the details of a single variation. 

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page (where the asset is currently on)
EXPERIMENT_ID | The unique ID of the experiment returned from the previous call for creating an experiment
VARIATION_ID | The unique ID for the alternative asset



## Update a variation

```shell
curl -X PUT "https://<GLOBAL_DOMAIN>/projects/<PROJECT_ID>/pages/<PAGE_ID>/experiments/<EXPERIMENT_ID>/variations/<VARIATION_ID>"
-d url="https://assets.mysite.com/image2-new.jpg"
-H "x-api-key: API_KEY"
-H "Content-Type: application/json"
```

> Response

```json
{
  "project_id":"<PROJECT_ID>",
  "page_id":"<PAGE_ID>",
  "experiment_id":"<EXPERIMENT_ID>",
  "variation_id":"<VARIATION_ID>",
  "url": "https://assets.mysite.com/image2-new.jpg",
  "weight":20,
  "is_live":true,
  "is_original":false,
  "created_at":123456,
  "updated_at":23456
}
```

Update an existing variation. Available fields for update are url, is_live and weight.

### URL parameters

Parameter | Description
--------- | -----------
PROJECT_ID | The unique ID of the project
PAGE_ID | The unique ID of the page
EXPERIMENT_ID | The unique ID of the experiment
VARIATION_ID | The unique ID for the alternative asset

### Body Parameters
Required to specify at least one of the following parameters

Parameter | Description
--------- | -----------
url (optional) | The page address to refresh
is_live (optional) | Boolean parameter. Whether to activate this experiment. Default:true
weight (optional) | Number. Assign weight to an asset to control the frequency of its requests
