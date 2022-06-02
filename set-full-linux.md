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

Full Linux&reg; subscription provides stock images for RHEL, SLES, SAP, and non-SAP applications. 
{: shortdesc}

Power Systems Virtual Server provides three versions of the operating system (OS) stock images. You can also use full Linux&reg; subscription to obtain Power fixes or updates that are hosted on the IBM satellite server within IBM Cloud environment. Charges are applicable to use the keys against the IBM satellite server to receive the fixes. 

## Setting up full Linux&reg; subscription
{: #set-full-Linux}

To set up full Linux&reg; subscription for your account, complete the following steps.

1. [Configuring a Cloud connection](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)
2. [Creating a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy)
3. [Creating and configuring a Power virtual machine (PVM)](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm)

    a.	RHEL

    b.	SLES
4. [Configuring a Proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-proxy)
5. [Virtual server cloud-init script (RHEL and SLES)](/docs/power-iaas?topic=power-iaas-set-full-Linux#virtual-server)


### Configuring a Cloud connection
{: #configure-cloud-connection}

Create a Cloud connection with the following parameters:

-	Ensure that you set up a cloud connection between a private network that is attached to the Cloud connection and the private server. 
-	Each region zone needs its own cloud connection.
- You need the details of this private network for further configuration.

For more information on creating a Cloud connection, see [Managing Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Creating a proxy
{: #create-proxy}

Create a proxy setup by completing the following steps. This proxy is set up in a virtual private cloud (VPC) environment. 

1. Once you deploy the proxy, log in to VPC and select [security groups](/docs/vpc?topic=vpc-using-security-groups). 
2. Navigate to security groups by going to [IBM Cloud](https://cloud.ibm.com){: external} > VPC Infrastructure > Networks > Security groups. Select the security group that is attached to your proxy and add these port numbers: 443, 8443, 80, and 3128. Ensure that the IP being asked is the subnet CIDR of your private network PowerVS VM. To view the subnet CIDR in the IBM Cloud website go to the region zone. Go to subnets and find the subnet that you will be using, and copy the CIDR.
3. Once the proxy is created, log in and locate the subnet CIDR.
  
   a. To log in, open command-line interface(CLI) and run the `ssh root@<public IP of proxy>` command.

   b. Run `route -n`, the subnet of your proxy is listed after the private gateway. Example subnets are: 10.240.65.0, 10.209.155.192.

   c. To get the CIDR, run the `ip route` command. Example CIDRs are: 10.240.65.0/24, 10.209.155.192/26.

   d. You can note the CIDR number as you need it in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm) to establish connections from the VM to the proxy.

### Creating and configuring a Power virtual machine (PVM)
{: #create-power-vm}

1.	Create a PVM instance via PowerVS UI, CLI, or API with the following requirements.
      
    a.	SSH key

    b.	Public network

    c.	Private network created in [step 1](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)

2.	In the CLI, SSH to your RHEL or SLES PVM instance by using the PVM’s external IP address.

      -	`ssh root@<external IP address>`  Example: ssh root@1.2.3.4

3.  Add a network route to connect the PVM to the proxy configured in [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).

      - Run the `ip route` command and add CIDR subnet of proxy via private gateway of PVM.
  
        -	The CIDR subnet of the proxy is the value that is found at the end of [step 2](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy).
        -	You can view the private gateway of PVM in the server details of the PVM.

          Run `ip route` command and add 1.5.3.9/24 via 5.9.7.1
    
    If your VM is restarted, these IP routes are removed and they need to be added again.
    {: note}

### Configuring a Proxy
{: #configure-proxy}

Set up a proxy configuration, by completing the following steps:

1. Log in to your proxy server, by using the `ssh root@<public IP of proxy>` command.
2. Ensure that another IP route is created within the proxy. This IP route allows the IPs that are within the range of the created private IP gateway for your VM to this proxy gateway.

    - Run the `ip route` command and add CIDR of private network in Step 1 via gateway of proxy.
      
      - You can view the private VM gateway in the [IBM Cloud](https://cloud.ibm.com){: external} website. Select the PowerVS VM that you have created in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm), and go to the attached private network. The CIDR is listed as the last variable.
      - Run the `route -n` command to view the gateway of the proxy.

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

### Virtual server cloud-init script (RHEL and SLES)
{: #virtual-server}

You can customize your RHEL and SLES VMs by running the cloud-init script.

1. Log in to your RHEL or SLES VM, by using the `ssh root@<External IP”>` command.
2. A readme file is generated in the `/usr/share/powervs-fls-readme.md` directory. The readme file contains information from this documentation. However, it also provides some variables that are needed to run the cloud-init script.
3. The cloud-init script is located in `/usr/local/bin/`.
  
   a. Run the script as _root_. You can switch the user to _root_ by using the `sudo su root` command.

   b. For	RHEL, run the following command:

    `. /usr/local/bin/rhel-cloud-init.sh -a Activation_Key -u Capsule_server_url -p Proxy_IP_and_port -o Org -t Deployment type`
        
      -a = activation key

      -u = the url of the RHEL capsule server you are registering against

      -p = ”private_ip_of_powervs_vm”:3128

      -o = organization associated with activation key

      -t = deployment type of this vm(RHEL, RHEL-SAP, RHEL-SAP-NETWEAVER)

4. For SLES, run the following command: 
   
    `. /usr/local/bin/sles-cloud-init.sh -s <RMT_SERVER>`
      
    -s = the url of the SLES RMT server you are registering against
