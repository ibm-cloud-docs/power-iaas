---

copyright:
  years: 2024

lastupdated: "2024-06-05"

keywords: setting up terraform, {{site.data.keyword.powerSys_notm}} as a service, private cloud, howto, terminology, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Terraform for {{site.data.keyword.powerSys_notm}}
{: #setting-up-terraform}

Terraform on IBM Cloud enables predictable and consistent provisioning of IBM Cloud services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the IBM Cloud CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.powerSysFull}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on IBM Cloud solution? Try out [IBM Cloud Schematics](/docs/schematics?topic=schematics-getting-started). With Schematics, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the IBM Cloud Provider plug-in. Schematics also provides pre-defined Terraform templates that you can easily install from the IBM Cloud catalog.
{: tip}

## Installing Terraform and configuring resources for {{site.data.keyword.powerSys_notm}}
{: #installing-terraform}

Before you can create an authorization by using Terraform, make sure that you have completed the following prerequisites:

- Make sure that you have the [required access](/docs/power-iaas?topic=power-iaas-managing-resources-and-users) to create and work with the {{site.data.keyword.powerSys_notm}} resources.
- Install the Terraform CLI and configure the IBM Cloud Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the IBM Cloud APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

1. Create a {{site.data.keyword.powerSys_notm}} instance by using the `ibm_resource_instance` resource argument in your `main.tf` file. The {{site.data.keyword.powerSys_notm}} instance in the following example is named `test_instance` and the resource is `ibm_pi_instance`.

   ```text
   resource "ibm_pi_instance" "test-instance" {
       pi_memory             = "4"
       pi_processors         = "2"
       pi_instance_name      = "test-vm"
       pi_proc_type          = "shared"
       pi_image_id           = "${data.ibm_pi_image.powerimages.id}"
       pi_key_pair_name      = ibm_pi_key.key.key_id
       pi_sys_type           = "s922"
       pi_cloud_instance_id  = "51e1879c-bcbe-4ee1-a008-49cdba0eaf60"
       pi_pin_policy         = "none"
       pi_health_status      = "WARNING"
       pi_network {
         network_id = data.ibm_pi_public_network.dsnetwork.id
       }
   }
   ```
   {: codeblock}

2. #After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```text
   # terraform init
   ```
   {: codeblock}

3. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.powerSys_notm}} instances:

   ```text
   # terraform plan
   ```
   {: codeblock}

4. Create the {{site.data.keyword.powerSys_notm}} instances in IBM Cloud.

   ```text
   # terraform apply
   ```
   {: codeblock}

5. From the [IBM Cloud resource list](https://cloud.ibm.com/resources){: external}, select the {{site.data.keyword.powerSys_notm}} instance that you created and note the instance ID.

## What's next?
{: #what-next}

Now that you have successfully created your {{site.data.keyword.powerSys_notm}} instance with Terraform on IBM Cloud, you can visit the [Power Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/pi_capture){: external} to perform additional tasks using Terraform.
