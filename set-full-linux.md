---

copyright:
  years: 2022

lastupdated: "2022-05-20"

keywords: full linux, set full linux

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
{: #set-full-linux}

Full Linux subscription provides stock images for RHEL, SLES, SAP, and non-SAP applications. 
{: shortdesc}

Power Systems Virtual Server provides three versions of the operating system (OS) stock images. You can also utilize full Linux subscription to obtain Power patches or updates hosted on IBM satellite server within IBM Cloud environement. Charges are applicable to use the keys against the IBM satelite server to receive the patches. 

## Setting up full Linux subscription
{: #set-full-linux}

To set up full Linux subscription for your account, complete the following steps.

1. [Cloud connection configuration](/docs/power-iaas?topic=full-linux-subscription#configure-cloud-connection)
2. [Proxy creation and configuration](/docs/power-iaas?topic=full-linux-subscription#configure-cloud-connection)
3. Power Virtual Machine (PVM) creation and configuration
      a.	RHEL
      b.	SLES subscription-mana
4. Proxy configuration
5. Virtual server cloudinit script (RHEL and SLES)


### Configure a Cloud connection
{: #configure-cloud-connection}

-	Ensure that you set up a cloud connection between a private network that will be attached to the Cloud connection and the private server. 
-	Each environment will need its own cloud connection.
- You will need the details of this private network for further configuration.

For more information on creating a Cloud connection, see [Managing Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Creating and configuring a proxy
{: #create-proxy}

Create and configure a proxy setup by following the instructions in [Configuring an HTTP proxy](/docs/satellite?topic=satellite-config-http-proxy&mhsrc=ibmsearch_a&mhq=proxy). This proxy will be set up in an virtual private cloud (VPC) environement. 

1. Once the proxy has been deployed, log into VPC and select [security groups](/docs/vpc?topic=vpc-using-security-groups). 
2. Select the security group attached to your proxy and add 443, 8443, 80, and 3128. Ensure that the IP being asked is the subnet CIDR of your private network powervs vm. The subnet CIDR can be found in the IBM cloud site by going to the region zone, then selecting subnets, finding the subnet you will be using, and copying the CIDR.
3. A proxy can also be established within the Classic infrastructure.
4. Once the proxy is spawned, log in and locate the subnet cidr.
  
   a. To log in, go to terminal and run the following command
        `	ssh root@”public IP of proxy`

   b. Run `route -n`, the subnet of your proxy is listed below the private gateway. Example subnet: 10.240.65.0, 10.209.155.192.

   c. To get the CIDR, run `ip route`. Example CIDR: 10.240.65.0/24, 10.209.155.192/26.

   d. Note the CIDR as you will need it in step 3 to establish connections from the VM to the proxy.

### Creating and configuring a Power virtual machine
{: #create-proxy}

1.	Create a PVM instance via PowerVS UI, CLI, or API with the following requirements:
      
    a.	SSH key

    b.	Public network

    c.	Private network from Step 1

2.	For RHEL:

    a. Log into your vm in a teminal instance with the external IP using the command:
            `ssh root@”External IP”`.

    b. You must set up a proxy connection.

      - Sudo su root, if not root already
  
      -	ip route add “subnet of proxy(CIDR)” via “private powervs vm gateway
          
        - the CIDR subnet is the value found in the end of step 1
        - the private vm gateway can be found in the IBM cloud site and selecting your powervs vm

    If your VM is restarted, these IP routes will be removed and will need to be added again
    {: note}

3. For SLES:

    a. Using a command line (terminal), SSH to your SLES PVM instance using the PVM’s external IP address.

      -	ssh root@<external IP address> i.e., ssh root@1.2.3.4

    b. Add network route to connect the PVM to the proxy configured in Step 2.

      - ip route add “CIDR subnet of proxy” via “private gateway of PVM”
  
        -	The CIDR subnet of the proxy is the value found at the end of Step 2.
        -	The private gateway of PVM can be found in the server details of the PVM
                  i.e, ip route add 1.5.3.9/24 via 5.9.7.1
    
    If your VM is restarted, these IP routes will be removed and will need to be added again.
    {: note}
