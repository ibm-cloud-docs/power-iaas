---

copyright:
  years: 2022

lastupdated: "2022-05-30"

keywords: full Linux, set full Linux, proxy

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Full Linux&reg; subscription for Power Systems Virtual Servers
{: #set-full-Linux}

Full Linux&reg; subscription provides Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES) stock images that can be used for SAP and non-SAP applications. 
{: shortdesc}

Power Systems Virtual Server provides three versions of stock images for each operating system (OS). You can also use the full Linux&reg; subscription feature to get OS interim fixes and updates for Power servers that are hosted on the IBM satellite server within the IBM Cloud environment. Extra charges apply if you use the activation keys in the IBM Cloud Satellite to receive the interim fixes.

## Setting up full Linux&reg; subscription
{: #set-full-Linux}

To set up full Linux&reg; subscription for your account, complete the following steps:

1. [Configuring a Cloud connection](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)
2. [Creating a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy)
3. [Creating and configuring a Power virtual machine (PVM)](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm)

    a.	RHEL

    b.	SLES
4. [Configuring a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-proxy)
5. [Customizing the VMs by using the cloud-init script (RHEL and SLES)](/docs/power-iaas?topic=power-iaas-set-full-Linux#virtual-server)


### Step 1: Configuring a Cloud connection
{: #configure-cloud-connection}

Ensure that the following requirements are met when you create a Cloud connection: Create a Cloud connection with the following parameters:

-	Ensure that you set up a Cloud connection between the Power Systems Virtual Server instance and the IBM Cloud Classic infrastructure by using a private network. 
-	The Power Systems Virtual Servers in each region and zone must have its own cloud connection.
- You have the details of this private network for further configuration.

For more information about creating a Cloud connection, see [Managing Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Step 2: Creating a proxy
{: #create-proxy}

Create a proxy setup by completing the following steps. This proxy is set up in a virtual private cloud (VPC) environment. 

1. Deploy a proxy instance based on your requirement. For more information, see [Enabling proxy protocol](/docs/vpc?topic=vpc-advanced-traffic-management#proxy-protocol-enablement).

2. Open the Security groups for the VPC by navigation to IBM Cloud dashboard > VPC Infrastructure > Networks > Security groups. For more information about security groups, see [security groups](/docs/vpc?topic=vpc-using-security-groups). 

3. Select the security group that is attached to your proxy and add these port numbers: 443, 8443, 80, and 3128. Ensure that the IP address that you are asked to specify is the subnet CIDR of your private network for the Power Systems Virtual Server instance. To view the subnet CIDR in the IBM Cloud dashboard, go to the zone, click **Subnets**, identify the subnet that you will be using, and copy the CIDR.

4. After the proxy is created, log in to the proxy instance and locate the subnet CIDR by completing the following steps:
  
   a. Open the command-line interface (CLI) and run the `ssh root@<public IP of proxy>` command.

   b. Run the `route -n` command to identify the subnets. The subnet of your proxy instance is listed after the private gateway in the command output. Example subnets are: 10.240.65.0, 10.209.155.192.

   c. To get the CIDR, run the `ip route` command. Example CIDRs are: 10.240.65.0/24, 10.209.155.192/26.

   d. Note the CIDR number as you need it, as described in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm) to establish connections from the VM to the proxy.

### Step 3: Creating and configuring a Power virtual machine (PVM)
{: #create-power-vm}

1.	Create a Power Systems Virtual Server instance (also known as PVM instance) by using Power Systems Virtual instance GUI, CLI, or API with the following requirements.
      
    a.	SSH key

    b.	Public network

    c.	Private network that you created in [step 1](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)

2.	In the proxy instance CLI, start an SSH connection to your RHEL or SLES PVM instance by using the PVM’s external IP address in the following command:

      	`ssh root@<external IP address>`  
      
        Example: ssh root@1.2.3.4

3.  Add a network route from the PVM instance to the proxy instance that you configured in [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).

      - Run the `ip route` command and add the CIDR subnet of proxy through the private gateway of PVM.
  
        -	The CIDR subnet of the proxy is the value that you got after performing [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).
        -	You can view the private gateway of PVM in the server details of the PVM.

        Example: Run the `ip route` command and add the CIDR subnet IP address 1.5.3.9/24 through the private gateway IP address 5.9.7.1.
    
    If your VM is restarted, these IP routes are removed and the IP routes must be added again.
    {: note}

### Step 4: Configuring a proxy instance
{: #configure-proxy}

Set up a proxy configuration, by completing the following steps:

1. Log in to your proxy instance by running the `ssh root@<public IP of proxy>` command.
2. Ensure that another IP route is created within the proxy instance. This IP route allows the IP addresses that are within the range of the private IP gateway that you created for your VM. The IP addresses are used to connect your VM to the proxy gateway.

    - Run the `ip route` command and add the CIDR number of that private network that you derived in Step 1 via the gateway of proxy.
      
      - You can view the private VM gateway in the [IBM Cloud](https://cloud.ibm.com){: external} website. Select the PowerVS VM that you created in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm), and go to the attached private network. The CIDR number is listed as the last variable.
      - Run the `route -n` command to view the gateway of the proxy.

3. A connection is now established with the proxy and the PVM. You can ping the connection in both the proxy instance and the PVM instance, as follows:  
    - In the proxy instance, you can ping the private IP of the PVM by using the `ping <private IP of powervs vm>` command.
    - In the PVM instance, you can ping the private IP of the proxy by using the `ping <private IP of proxy>` command.

4. A squid (proxy caching server) must be installed on the VM. 
5. Set up squid by completing the following steps:
   
   a. Install the squid base by running the following commands:
      - `sudo yum update -y`
      - `sudo yum install epel-release`
      - `sudo yum install squid`
  
   You must have root authority to run these commands. After the installation completes, the squid config file is stored in the `/etc/squid/squid.conf` location. 

   b. Use the configuration provided in the [Example File](Add the example file that is provided in the doc as a downloadable file) for your reference.

### Step 5: Customizing the VMs by using the cloud-init script (RHEL and SLES)
{: #virtual-server}

You can customize your RHEL and SLES VMs by running the cloud-init script.

1. Log in to your RHEL or SLES VM, by using the `ssh root@<External IP”>` command.
2. A readme file is generated in the `/usr/share/powervs-fls/powervs-fls-readme.md` location. For relevant information about variables that are required to run the cloud-init script, see the readme file.
3. Run the cloud-init script that is located in the `/usr/local/bin/` location. Run the script as _root_. You can switch the user to _root_ by using the `sudo su root` command.

   a. For	RHEL, run the following command:

    `. /usr/local/bin/rhel-cloud-init.sh -a Activation_Key -u Capsule_server_url -p Proxy_IP_and_port -o Org -t Deployment type`
        
      -a = activation key

      -u = the URL of the RHEL capsule server you are registering against

      -p = "private_ip_of_powervs_vm":3128

      -o = organization associated with the activation key

      -t = deployment type of this VM (RHEL, RHEL-SAP, RHEL-SAP-NETWEAVER)

    b. For SLES, run the following command: 
   
      `. /usr/local/bin/sles-cloud-init.sh -s RMT_Server_address -p private_ip_of_proxy_vm:3128`
      
      -s = the URL of the SLES Repository Mirroring Tool (RMT) server that you are using for registration

      -p = "private_ip_of_powervs_vm":3128
