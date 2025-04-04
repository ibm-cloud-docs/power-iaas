---

copyright:
  years: 2024
lastupdated: "2025-03-28"

---

{{site.data.keyword.attribute-definition-list}}

# Installing the IBM {{site.data.keyword.powerSys_notm}} CLI plug-in
{: #power-iaas-cli-byb}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}

---



To install, update, or view the IBM {{site.data.keyword.powerSys_notm}} CLI plug-in, complete the following steps:

1. Install the [{{site.data.keyword.cloud}} CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started){: external}.

2. Install or update the `power-iaas` plug-in.

    **To install:**

    ```bash
    ibmcloud plugin install power-iaas
    ```

    **To update:**

    ```bash
    ibmcloud plugin update
    ```

    **To view your installed plug-ins and versions:**

    ```bash
    ibmcloud plugin list
    ```

3. Log in to the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/login){: external}.

    The power-iaas command-line plug-in uses the region that `ibmcloud login` targets to determine the IBM {{site.data.keyword.powerSys_notm}} endpoint. For example, to use the IBM {{site.data.keyword.powerSys_notm}} endpoint `https://cloud.ibm.com` you must use the `ibmcloud login -a https://cloud.ibm.com` command to target the `us-east` region. If you have a federated account, use the following command:

    ```bash
    ibmcloud login -a https://cloud.ibm.com -sso
    ```

4. Run one of the following commands to list all the services under your account:

   * For IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}}, run the `ibmcloud pi ws ls` command.
     The **Cloud Resource Name** (CRN) under **ID** contains your **Tenant ID** and **Cloud Instance ID**. The following example shows a typical CRN:

    ```screen
    crn:v1:staging:public:power-iaas:us-east:a/abcdefghijklmnopqrstuvwxyzabcdef:121d5ee5-b87d-4a0e-86b8-aaff422135478::
    ```

   * For {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}, run the `ibmcloud pi ws ls -p` command.

5. Target your service by entering `ibmcloud pi ws tg <CRN>` command:
   * Following is an example of the output for IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}}:

    ```bash
    ibmcloud pi ws tg crn:v1:staging:public:power-iaas:us-east:a/abcdefghijklmnopqrstuvwxyzabcdef:121d5ee5-b87d-4a0e-86b8-aaff422135478::
    ```

   * Following is an example of the output for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}:

    ```bash
    ibmcloud pi ws tg crn:v1:staging:public:power-iaas:satloc_dal_clp3foc20dd82387pe83:a/c7e6bd2517ad44eabbd61fcc25cf68d5:dc815dc0-e0ba-4576-b286-a3aeedaa9e60::
    ```

The IBM {{site.data.keyword.powerSys_notm}} CLI plug-in requires a valid IAM token authorization before each use. Use the `ibmcloud login` command to renew authorization if your token expires.
{: note}
