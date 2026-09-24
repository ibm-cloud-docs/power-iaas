---

copyright:
  years: 2023, 2026

lastupdated: "2026-09-23"

keywords: getting help and support, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, help and support, support ticket, faq, create new case

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting help and support for {{site.data.keyword.powerSys_notm}}
{: #getting-help-and-support-pvs}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

If you experience an issue or have questions about {{site.data.keyword.powerSys_notm}}, IBM Support is available to help. You can open a support case directly, or use the following self-service resources if you prefer a self-service approach.
{: shortdesc}

* Ask a question in the [AI assistant](/docs/overview?topic=overview-ask-ai-assistant){: external}, available from the console or the {{site.data.keyword.cloud_notm}} CLI.
* Review the [FAQs for Power Virtual Server](/docs/power-iaas?topic=power-iaas-powervs-faqs).
* Review the [troubleshooting documentation](/docs/power-iaas?group=troubleshooting) to resolve common issues.
* Check the status of the {{site.data.keyword.Bluemix_notm}} platform and resources on the [Status page](/status){: external}.
* Review [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud){: external} to see whether other users have experienced the same problem. When you post a question, tag it with `ibm-cloud` so that IBM development teams can find it.
* Review [Getting support](https://cloud.ibm.com/docs/support){: external} for an overview of support options.
* Review the [IBM Power Virtual Server Support Reference Guide](https://www.ibm.com/support/pages/node/6953473){: external} for detailed guidance on opening and managing support cases.

Use the following table to identify which support process applies to your situation.

| Issue type                              | Deployment                         | Process to follow                                                                                                                             |
| --------------------------------------- | ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Infrastructure                          | IBM data center or client location | [Opening {{site.data.keyword.powerSys_notm}} infrastructure cases](#support-case-IBM-cloud)                                                   |
| Operating system (AIX, Linux, or IBM i) | IBM data center                    | [Opening operating system–related cases for IBM data centers](#support-case-IBM-offprem)                                                      |
| Operating system (AIX, Linux, or IBM i) | Client location                    | [Opening operating system–related cases for {{site.data.keyword.powerSys_notm}} Private Cloud in a client location](#support-case-IBM-onprem) |
{: caption="Support processes by issue type and deployment" caption-side="bottom"}

## Support plans
{: #support-plans}

You can choose a Basic, Advanced, or Premium support plan to customize your {{site.data.keyword.cloud_notm}} support experience. The support plan that you select determines the severity level that you can assign to support cases and your level of access to the tools in the Support Center. For more information, see [Basic, Advanced, and Premium support plans](https://cloud.ibm.com/docs/support?topic=support-support-plans){: external}.

If you have a Lite or Free support plan, you can open cases only for non-technical issues, such as account management, billing and usage, and access management. To open technical support cases for {{site.data.keyword.powerSys_notm}}, you must have a Basic, Advanced, or Premium support plan.
{: note}



## Providing support case details
{: #support-case-details}

To help the support team investigate your case and provide a timely resolution, include detailed information and steps to reproduce the issue, if applicable. Review the following types of information and include the details that are applicable to your {{site.data.keyword.powerSys_notm}} environment.




- Provide your data center information, including the data center name, region, and zone.

- Provide your {{site.data.keyword.powerSys_notm}} workspace and instance details by running the following commands. Before you run these commands, ensure that you have the {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.powerSys_notm}} CLI plug-in installed and that you are logged in to your account. For more information, see [Installing the IBM {{site.data.keyword.powerSys_notm}} CLI plug-in](/docs/power-iaas?topic=power-iaas-power-iaas-cli-byb).

   - Run `ibmcloud pi workspace list` and note your workspace ID.
   - Run `ibmcloud pi instance list` and note the VSI name and ID.
   - Run `ibmcloud pi instance get INSTANCE_ID` for full details of the affected instance.

- (Optional) Provide a network diagram with your specific setup.
- (Optional) For network connectivity issues, provide the following details:
   * Source and destination IP addresses.
   * Network Security Group details.
   - A route report from {{site.data.keyword.powerSys_notm}}.
- Provide the operating system name, version, and patch level.

## Opening {{site.data.keyword.powerSys_notm}} infrastructure cases
{: #support-case-IBM-cloud}

To open a {{site.data.keyword.powerSys_notm}} infrastructure case, log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com){: external}, click the **Help** icon (![Help icon](../icons/help.svg "Help icon")) in the menu bar, select **Support center**, and click **Create case**. To complete the case, include the information described in the [Providing support case details](#support-case-details) section.

The categories and options that are available depend on your support plan. For detailed guidance on selecting the correct category, topic, and subtopic for {{site.data.keyword.powerSys_notm}} cases, see the [IBM Power Virtual Server Support Reference Guide](https://www.ibm.com/support/pages/node/6953473){: external}.






## Opening operating system (AIX, Linux, or IBM i)–related cases for IBM data centers
{: #support-case-IBM-offprem}

[{{site.data.keyword.off-prem}}]{: tag-blue}

If you experience an AIX, Linux, or IBM i operating system issue in IBM data centers, contact operating system support through the IBM Support portal by completing the following steps:

To log in to the IBM Support portal, you need an IBMid. If you do not have one, [create an IBMid](https://www.ibm.com/account/us-en/signup/register.html){: external} before you begin.
{: note}



1. Log in to the [IBM Support](https://www.ibm.com/mysupport/s/?language=en_US){: external} portal with your IBMid.

2. Click **Open a case**. The **Open a case** page is displayed.

3. In the **General** section, select **Product support** from the **Type of support** list.

4. In the **Case title** field, enter a title that summarizes the operating system issue.

5. In the **Product information** section, select the product details that apply to your operating system:

   **For AIX or IBM i**:
   1. Select **IBM** from the **Product manufacturer** list.
   2. In the **Product** field, search for and select **AIX on PowerVS** or **IBM i on PowerVS**.
   3. Select the appropriate version from the **Product version** list.

   **For Linux**:
   1. From the **Product manufacturer** list, select the manufacturer that matches your Linux distribution:
      - Select **Red Hat** for Red Hat Enterprise Linux (RHEL).
      - Select **SUSE** for SUSE Linux Enterprise Server (SLES).
   2. In the **Product** field, search for and select the product that matches your environment.

6. In the **Severity and account information** section, select the appropriate severity level based on the business impact of the issue.

7. In the **Case description** section, provide a detailed description of the issue, select your preferred language for case communications, and optionally select **Enhanced** or **Basic** email notifications.

9. In the **Attachments and team members** section, provide a contact number in the **Case contact number** field.

10. (Optional) In the **Client reference number** field, provide a client reference number.

11. (Optional) In the **Case template** section, select **Save this case as a template for future use** and enter a template title.

12. Click **Submit case**.

## Opening operating system (AIX, Linux, or IBM i)–related cases for {{site.data.keyword.powerSys_notm}} Private Cloud in a client location
{: #support-case-IBM-onprem}

[{{site.data.keyword.on-prem}}]{: tag-red}

If you experience an AIX, Linux, or IBM i operating system issue in {{site.data.keyword.powerSys_notm}} Private Cloud, contact operating system support through the IBM Support portal by completing the following steps:

To log in to the IBM Support portal, you need an IBMid. If you do not have one, [create an IBMid](https://www.ibm.com/account/us-en/signup/register.html){: external} before you begin.
{: note}

1. Log in to the [IBM Support](https://www.ibm.com/mysupport/s/?language=en_US){: external} portal with your IBMid.

2. Click **Open a case**. The **Open a case** page is displayed.

3. In the **General** section, select **Product support** from the **Type of support** list.

4. In the **Case title** field, enter a title that summarizes the operating system issue.

5. In the **Product information** section, select the product details that apply to your operating system:

   **For AIX or IBM i**:
   1. Select **IBM** from the **Product manufacturer** list.
   2. In the **Product** field, search for and select **AIX on PowerVS** or **IBM i on PowerVS**.
   3. Select the appropriate version from the **Product version** list.

   **For Linux**:
   1. From the **Product manufacturer** list, select the manufacturer that matches your Linux distribution:
      - Select **Red Hat** for Red Hat Enterprise Linux (RHEL).
      - Select **SUSE** for SUSE Linux Enterprise Server (SLES).
   2. In the **Product** field, search for and select the product that matches your environment.
   3. In the **Machine serial number** field, enter your serial number.
   4. Select the appropriate version from the **Product version** list.
   5. For Red Hat Enterprise Linux, select the appropriate option from the **Service type** list.

6. In the **Severity and account information** section, select the appropriate severity level based on the business impact of the issue.

7. In the **Case description** section, provide a detailed description of the issue.

8. (Optional) In the **Case description** section, select your preferred language for case communications.

9. In the **Attachments and team members** section, provide a contact number in the **Case contact number** field.

10. (Optional) In the **Client reference number** field, provide a client reference number.

11. (Optional) In the **Case template** section, select **Save this case as a template for future use** and enter a template title.

12. Click **Submit case**.
