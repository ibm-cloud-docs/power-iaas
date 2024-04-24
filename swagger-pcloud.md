---

copyright:
  years: 2019, 2022, 2023, 2024

lastupdated: "2024-04-15"

keywords: power systems api

subcollection: power-iaas

content-type: api-docs

title: Power Virtual Server API

---

{{site.data.keyword.attribute-definition-list}}



# API documentation
{: #introduction}

You can use the IBM&reg; Power Systems&trade; Virtual Server to easily deploy and configure virtual servers that are running AIX, IBM i, or Linux (RHEL and SLES) workloads.

## Endpoint URL
{: #endpoint}

The {{site.data.keyword.powerSys_notm}} service uses regional endpoints over a public network. To target your region, replace `{region}` with the prefix that represents the geographic area where your service instance is located. Currently, the `us-east`, `us-south`, `eu-de`, `lon`, `tor`, `syd`, and `tok` regions are supported.

```text
https://{region}.power-iaas.cloud.ibm.com
```

The {{site.data.keyword.powerSys_notm}} service uses regional endpoints over a private network. To target your region, replace `{region}` with the prefix that represents the geographic area where your service instance is located. Currently, the `us-east`, `us-south`, `eu-de`, `eu-gb`, `ca-tor`, `au-syd`, `jp-tok`, `jp-osa`, `br-sao`, and `ca-mon` regions are supported.

```text
https://private.{region}.power-iaas.cloud.ibm.com
```

## Authentication
{: #authentication}

To work with the {{site.data.keyword.powerSys_notm}} API, you must include your {{site.data.keyword.cloud_notm}} IAM access token and the {{site.data.keyword.powerSys_notm}} instance ID, also known as your **Cloud Resource Name** (CRN), in every request. The first part of your CRN contains your **Tenant ID** and the second part contains your **Cloud Instance ID**. The following example shows a typical CRN:

```text
crn:v1:staging:public:power-iaas:us-east:a/abcdefghijklmnopqrstuvwxyzabcdef:121d5ee5-b87d-4a0e-86b8-aaff422135478::

Tenant ID {tenant_id} = abcdefghijklmnopqrstuvwxyzabcdef
Cloud Instance ID {cloud_instance_id} = 121d5ee5-b87d-4a0e-86b8-aaff422135478
```

You can retrieve an access token by first creating an API key, and then exchanging your API key for a {{site.data.keyword.cloud_notm}} IAM token. For more information, see [Retrieving an access token programmatically](/docs/services/key-protect?topic=key-protect-retrieve-access-token) and [Retrieving your instance ID](/docs/services/key-protect?topic=key-protect-retrieve-instance-ID).

## Example
{: #example}
{: #curl}
{: right}

API endpoint

```text
https://{region}.power-iaas.cloud.ibm.com
```
Replace `{region}` with the prefix that represents the geographic area where your {{site.data.keyword.powerSys_notm}} service instance resides.

To retrieve your access token:

```text
ibmcloud iam oauth-tokens
```


To retrieve your instance ID:

```text
ibmcloud resource service-instance {instance_name} --id
```

Replace `{instance_name}` with the unique alias that you assigned to your {{site.data.keyword.powerSys_notm}} instance.

## Error handling
{: #error-handling}

This API uses standard HTTP response codes to indicate whether a method completed successfully. A `200` response indicates success. A `400` type response indicates a failure, and a `500` type response indicates an internal system error.

| HTTP Error Code | Description           | Recovery                                                                                                         |
|-----------------|-----------------------|------------------------------------------------------------------------------------------------------------------|
| `200`           | Success               | The request was successful.                                                                                      |
| `400`           | Bad Request           | The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all of the required parameters in your request. |
| `401`           | Unauthorized          | You are not authorized to make this request. Log in to the IBM Cloud website and try again. If this error persists, contact the account owner to check your permissions. |
| `403`           | Forbidden             | The supplied authentication is not authorized to access this resource.                                           |
| `404`           | Not Found             | The requested resource could not be found.                                                                       |
| `408`           | Request Timeout       | The connection to the server timed out. Wait a few minutes, then try again.                                      |
| `409`           | Conflict              | The entity is already in the requested state.                                                                    |
| `500`           | Internal Server Error | Power Virtual Server is currently unavailable. Your request could not be processed. Wait a few minutes and try again. |


## Download OpenAPI definition file
{: #api-doc-file}

Download the OpenAPI definition file from [here](https://cloud.ibm.com/media/docs/downloads/power-iaas/swagger-pcloud-la.json){: external}.
