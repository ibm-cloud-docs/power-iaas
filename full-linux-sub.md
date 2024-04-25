---

copyright:
  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: Full Linux Subscription, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Full Linux&reg; subscription for IBM {{site.data.keyword.powerSys_notm}} Private Cloud
{: #full-linux-sub}

[Private Cloud]{: tag-red}

The full Linux&reg; subscription feature enables Red Hat Enterprise Linux (RHEL) support through IBM.
{: shortdesc}

The full Linux subscription uses activation keys to provide access to interim fixes and updates for the operating system for {{site.data.keyword.powerSysFull}}. The {{site.data.keyword.powerSys_notm}} is hosted on an IBM satellite server within the IBM Cloud environment. Extra charges apply for setting up a Full Linux subscription account.

To register for the full Linux subscription, you must select one of the stock operating system (OS) images that are provided by IBM. IBM currently provides RHEL stock OS images for SAP and non-SAP applications.

To know more about the SLES versions that are supported, see [What versions of AIX, IBM i, and Linux are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).

The OS file name for the full Linux subscription feature starts with RHEL. For SAP applications, ensure that you are using an IBM stock OS image for SAP. These stock images are certified for using SAP applications. Bring your own images feature is not supported. To learn more about SAP applications with {{site.data.keyword.powerSys_notm}}, see these [Must-Reads](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external} before you start deployment.
{: note}

## Setting up full Linux subscription
{: #setup-fls}

Complete the following steps to set up full Linux subscription for your account:

* [Configuring a data plane network](/docs/power-iaas?topic=power-iaas-full-linux-sub#config-dpn)
* [Creating a proxy](/docs/power-iaas?topic=power-iaas-full-linux-sub#create-proxy-private)
* [Install squid base](/docs/power-iaas?topic=power-iaas-full-linux-sub#squid-base)
* [Completing the setup](/docs/power-iaas?topic=power-iaas-full-linux-sub#complete-setup)

### Configuring a data plane network
{: #config-dpn}

The pod is configured with a control plane network and data plane network when onboarded. The full Linux subscription setup is done through the data plane network. The data plane network connects the pod with your data center infrastructure. The data plane network and the control plane network do not interact with each other. Hence, for completing the full Linux subscription, use the data plane network on the pod. Set up connectivity between your data center and IBM Cloud either by using a site-to-site VPN for virtual private cloud (VPC) or by using IBM Cloud Direct Link 2.0.

### Creating a proxy
{: #create-proxy-private}

A proxy setup is set up in a virtual private cloud (VPC) on IBM Cloud with a Virtual Switch Interface (VSI). Connect this VPC on IBM Cloud to the control plane network through IBM Cloud Direct Link 2.0 Connect or VPN connection.

The CentOS image is recommended for the proxy VSI.
{: note}

To create a proxy setup, complete the following steps:

1. Open the Security groups for the VPC by navigation to IBM Cloud dashboard > VPC Infrastructure > Networks > Security groups. For more information about security groups, see [About security groups](/docs/vpc?topic=vpc-using-security-groups){: external}.

2. In the default Security group that is attached to your proxy, add 443, 8443, 80 and 3128 ports.

3. On the VSI, enable a floating IP temporarily. In the proxy instance, start an secure shell (SSH) connection by using this temporary IP address in the `ssh` command.

```text

ssh root@<external IP address>
```
{: codeblock}

Example: ssh root@1.2.3.4

### Install squid base
{: #squid-base}

In the VSI, install squid by using the following commands:
1. `sudo yum update -y`
2. `sudo yum install epel-release`
3. `sudo yum install squid`

You must have root authority to run these commands. After the installation completes, the `squid config` file is stored in the `/etc/squid/squid.conf` location.

Configure the squid by using the following commands:
1. `acl localnet "<CIDR of a subnet that you will deploy in the pod>"`
      For example: `10.140.129.217/29`
2. `acl ibmprivate dst 161.26.0.0/16`
3. `acl ibmprivate dst 166.8.0.0/14`

Also, look at the other entries and make necessary changes according to your environment.

Save the `squid config` file and restart the squid service by using the following commands:
1. `sudo systemctl enable squid`
2. `sudo systemctl stop squid` (optional)
3. `sudo systemctl start squid`

### Completing the setup
{: #complete-setup}

To complete the setup process, follow these steps:
1. Deploy a network in the pod.
2. Connect the network externally by using a ticketing process with Border Gateway Protocol (BGP).
3. Deploy the LPAR (RHEL) for completing the full Linux subscription.
4. Connect to the LPAR by using one of the following methods:
   * From the console on the browser.
   * By using the `SSH` command from your data network.
5. Test the internal private address of the VSI on the VPC by using the `ping` command. For example, `ping 10.240.0.4`
6. To register your LPAR with the RHEL subscription on the satellite server, open the `powervs-fls-readme.md` file that is stored in the path `/usr/share/powervs-fls` and use the following command in the file
    `/usr/local/bin/rhel-cloud-init.sh`
7. One of the parameters for the command represents the proxy IP. Set this proxy IP to the internal private IP of your proxy VSI. For example, `10.240.0.4`. Set the port to 3128.

To check whether the setup is complete and the subscription is successful, check the log files, `/var/log/powervs-fls.log` and `powervs-fls-dev.log`. When the setup is completed successfully, you can use the commands, such as `yum update -y`, `yum search <package>`, `yum install <package>`.

## Passing user-defined scripts
{: #cloud-init-fls-private-cloud}

When you select a Full Linux Subscription (FLS) boot image while provisioning a {{site.data.keyword.powerSys_notm}} instance, you get the option to pass in user data during first boot runtime.

In the user data  you can pass the custom content that allows you to customize the operating system for the specific instance.

The user data that you pass should follow the following conditions:
-  It should be uncompressed.
-  It should start with `#cloud-config`.
-  It should not exceed 63 Kb in size.
