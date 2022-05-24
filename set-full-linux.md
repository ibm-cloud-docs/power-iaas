---

copyright:
  years: 2022

lastupdated: "2022-05-23"

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

# Full Linux subscription for Power Systems Virtual Servers
{: #set-full-Linux}

Full Linux&reg; subscription provides stock images for RHEL, SLES, SAP, and non-SAP applications. 
{: shortdesc}

Power Systems Virtual Server provides three versions of the operating system (OS) stock images. You can also use full Linux&reg; subscription to obtain Power fixes or updates that are hosted on IBM satellite server within IBM Cloud environment. Charges are applicable to use the keys against the IBM satellite server to receive the fixes. 

## Setting up full Linux subscription
{: #set-full-Linux}

To set up full Linux&reg; subscription for your account, complete the following steps.

1. [Configure a Cloud connection](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)
2. [Creating and configuring a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy)
3. [Creating and configuring a Power virtual machine (PVM)](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm)

    a.	RHEL

    b.	SLES subscription-mana
4. [Proxy configuration](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm)
5. Virtual server cloudinit script (RHEL and SLES)


### Configure a Cloud connection
{: #configure-cloud-connection}

-	Ensure that you set up a cloud connection between a private network that is attached to the Cloud connection and the private server. 
-	Each environment needs its own cloud connection.
- You need the details of this private network for further configuration.

For more information on creating a Cloud connection, see [Managing Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Creating and configuring a proxy
{: #create-proxy}

Create and configure a proxy setup by following the instructions in [Configuring an HTTP proxy](/docs/satellite?topic=satellite-config-http-proxy&mhsrc=ibmsearch_a&mhq=proxy). This proxy is set up in a virtual private cloud (VPC) environment. 

1. Once you deploy the proxy, log in to VPC and select [security groups](/docs/vpc?topic=vpc-using-security-groups). 
2. Select the security group that is attached to your proxy and add 443, 8443, 80, and 3128. Ensure that the IP being asked is the subnet CIDR of your private network PowerVS VM. You can view the subnet CIDR in the IBM cloud site by going to the region zone, then selecting subnets, finding the subnet that you will be using, and copying the CIDR.
3. A proxy can also be established within the Classic infrastructure.
4. Once the proxy is created, log in and locate the subnet CIDR.
  
   a. To log in, go to terminal and run the `ssh root@<public IP of proxy>` command.

   b. Run `route -n`, the subnet of your proxy is listed after the private gateway. Example subnets are: 10.240.65.0, 10.209.155.192.

   c. To get the CIDR, run the `ip route` command. Example CIDR's are: 10.240.65.0/24, 10.209.155.192/26.

   d. You can note the CIDR number as you will need it in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm) to establish connections from the VM to the proxy.

### Creating and configuring a Power virtual machine (PVM)
{: #create-power-vm}

1.	Create a PVM instance via PowerVS UI, CLI, or API with the following requirements.
      
    a.	SSH key

    b.	Public network

    c.	Private network created in [step 1](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)

2.	For RHEL:

    a. Log in to your VM in a terminal instance with the external IP by using the `ssh root@<External IP>` command.

    b. You must set up a proxy connection.

      - Run the `Sudo su root` command.
  
      -	Run `ip route` command and add a subnet of proxy (CIDR) via private PowerVS VM gateway.
          
          - The CIDR subnet is the value that you have noted at the end of [step 1](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection).
          - You can view the private VM gateway in the [IBM Cloud](https://cloud.ibm.com){: external} website by selecting your PowerVS VM.

    If your VM is restarted, these IP routes are removed and they need to be added again.
    {: note}

3. For SLES:

    a. In the command-line interface (terminal), SSH to your SLES PVM instance by using the PVM’s external IP address.

      -	`ssh root@<external IP address>`  Example: ssh root@1.2.3.4

    b. Add a network route to connect the PVM to the proxy configured in [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).

      - Run the `ip route` command and add CIDR subnet of proxy via private gateway of PVM.
  
        -	The CIDR subnet of the proxy is the value found at the end of [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).
        -	You can view the private gateway of PVM in the server details of the PVM.

          Run `ip route` command and add 1.5.3.9/24 via 5.9.7.1
    
    If your VM is restarted, these IP routes are removed and they need to be added again.
    {: note}

### Proxy configuration
{: #configure-proxy}

Set up a proxy configuration, by completing the following steps:

1. Log in to your proxy server, by using the `ssh root@<public IP of proxy>` command.
2. Ensure that another IP route is created within the proxy. This IP route allows the IP’s within the range of the private IP gateway that you have created for your VM to this proxy gateway.

    - Run the `ip route` command and add a private PowerVS VM gateway ranges(CIDR) via gateway of proxy.
      
      - You can view the private VM gateway in the [IBM Cloud](https://cloud.ibm.com){: external} website. Select the PowerVS VM that you have created in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm), and go to the attached private network. The CIDR is listed as the last variable.
      - Run the `route -n` command, to view the gateway of the proxy.

3. A connection is now established with the proxy and the PowerVS VM. You can ping the connection both ways. 
    - From within the proxy you can ping the private IP of the PowerVS VM, by using the `ping <private IP of powervs vm>` command.
    - From within the PowerVS VM you can ping the private IP of the proxy, by using the `ping <private IP of proxy>` command.

4. A squid must be installed on the VM. 
5. Set up squid by completing the following steps:
   
   a. Run these commands as _root_.	This installs the base of squid: 
      - `sudo yum update -y`
      - `sudo yum install epel-release`
      - `sudo yum install squid`
  
   b. `squid config` file is stored in the location `/etc/squid/squid.conf`.
   c. Use the configuration provided in the [Example File](Add the example file that is provided in the doc as a downloadable file) for your reference.