---

copyright:
  years: 2022, 2023

lastupdated: "2023-06-12"

keywords: full Linux, set full Linux, proxy

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Full Linux&reg; subscription for {{site.data.keyword.powerSys_notm}} on cloud
{: #set-full-Linux}

[Off-premises]{: tag-blue}

The full Linux&reg; subscription feature enables Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise Server (SLES) support through IBM.
{: shortdesc}

The full Linux subscription also provides, via activation keys, access to OS interim fixes and updates for Power servers hosted on an IBM satellite server within the IBM Cloud environment. Extra charges apply when setting up a Full Linux subscription account.

To register for the full Linux subscription, you must select one of the stock operating system (OS) images provided by IBM. IBM provides RHEL and SLES stock OS images for SAP and non-SAP applications. To know more about the SLES versions that are supported, see [What versions of AIX, IBM i, and Linux are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).


The full Linux subscription feature OS filename starts with the Red Hat or Suse distribution name, `RHEL...` or `SLES...`.

If you plan to use your own license, select the OS image suffixed with `-BYOL`. On the VM Provisioning page, these images are listed under the **Client supplied subscription** section.
{: note}

## Setting up full Linux subscription
{: #setup-full-Linux}

To set up full Linux subscription for your account, complete the following steps:

1. [Configuring a Cloud connection](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-cloud-connection)
2. [Creating a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-proxy)
3. [Creating and configuring a Power virtual machine (PVM)](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm)

    a.	RHEL

    b.	SLES
4. [Configuring a proxy](/docs/power-iaas?topic=power-iaas-set-full-Linux#configure-proxy)
5. [Customizing the VMs by using the cloud-init script (RHEL and SLES)](/docs/power-iaas?topic=power-iaas-set-full-Linux#virtual-server)


### Step 1: Configuring a Cloud connection
{: #configure-cloud-connection}

Ensure that the following requirements are met when you create a Cloud connection. Create a Cloud connection with the following parameters:

-	Ensure that you set up a Cloud connection between the {{site.data.keyword.powerSysFull}} instance and the IBM Cloud Classic infrastructure by using a private network.
-	The {{site.data.keyword.powerSys_notm}} in each region and zone must have its own cloud connection.
- You have the details of this private network for further configuration.

For more information about creating a Cloud connection, see [Managing Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Step 2: Creating a proxy
{: #create-proxy}

Create a proxy setup by completing the following steps. This proxy is set up in a virtual private cloud (VPC) environment.

1. Deploy a proxy instance based on your requirement. For more information, see [Enabling proxy protocol](/docs/vpc?topic=vpc-advanced-traffic-management#proxy-protocol-enablement).

2. Open the Security groups for the VPC by navigating to IBM Cloud dashboard > VPC Infrastructure > Networks > Security groups. For more information about security groups, see [security groups](/docs/vpc?topic=vpc-using-security-groups).

3. Select the security group that is attached to your proxy and add these port numbers: 443, 8443, 80, and 3128. Ensure that the IP address that you are asked to specify is the subnet Classless Inter-Domain Routing (CIDR) of your private network for the {{site.data.keyword.powerSys_notm}} instance. To view the subnet CIDR in the IBM Cloud dashboard, go to the zone, click **Subnets**, identify the subnet that you will be using, and copy the CIDR.

4. After the proxy is created, log in to the proxy instance and locate the subnet CIDR by completing the following steps:

   a. Open the command-line interface (CLI) and run the `ssh root@<public IP of proxy>` command.

   b. Run the `route -n` command to identify the subnets. The subnet of your proxy instance is listed after the private gateway in the command output. Example subnets are: 10.240.65.0, 10.209.155.192.

   c. To get the CIDR, run the `ip route` command. Example CIDRs are: 10.240.65.0/24, 10.209.155.192/26.

   d. Note the CIDR number as you need it, as described in [step 3](/docs/power-iaas?topic=power-iaas-set-full-Linux#create-power-vm) to establish connections from the VM to the proxy.

### Step 3: Creating and configuring a Power virtual machine (PVM)
{: #create-power-vm}

1.	Create a {{site.data.keyword.powerSys_notm}} instance (also known as PVM instance) by using Power Virtual instance GUI, CLI, or API with the following requirements.

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

    If your VM is restarted, these IP routes are removed and so must be added again.
    {: note}

### Step 4: Configuring a proxy instance
{: #configure-proxy}

Set up a proxy configuration, by completing the following steps:

1. Log in to your proxy instance by running the `ssh root@<public IP of proxy>` command.
2. Ensure that another IP route is created within the proxy instance. This IP route allows the IP addresses that are within the range of the private IP gateway that you created for your VM. The IP addresses are used to connect your VM to the proxy gateway.

    - Run the `ip route` command and add the CIDR number of that private network that you derived in [Step 1](#configure-cloud-connection) via the gateway of proxy.

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

   b. Use the configuration provided in the following example for your reference. Values represented in the example configuration denote the following:
      - acl localnet src 192.168.0.0/16: the IP ranges of the IBM private network that the proxy will accept.
      - acl ibmprivate dst 161.26.0.0/16 and acl ibmprivate dst 166.8.0.0/14: the IP ranges of the IBM networks this proxy will be going to, this is the location of the RHEL satellite servers and SLES RMT servers.
      - acl SSL_ports port 443 8443 : Ports used for communication with RHEL satellite servers and SLES RMT servers.
      - http_port 3128: the port that will be listening for squid. This will be used as the communication port from your {{site.data.keyword.powerSys_notm}} VM to the squid proxy.

      ```text
      # Recommended minimum configuration:
      #

      # Example rule allowing access from your local networks.
      # Adapt to list your (internal) IP networks from where browsing
      # should be allowed
      acl localnet src 10.0.0.0/8     # RFC1918 possible internal network
      acl localnet src 172.16.0.0/12  # RFC1918 possible internal network
      acl localnet src 192.168.0.0/16 # RFC1918 possible internal network
      acl localnet src fc00::/7       # RFC 4193 local private network range
      acl localnet src fe80::/10      # RFC 4291 link-local (directly plugged) machines
      acl localnet src all
      acl ibmprivate dst 161.26.0.0/16
      acl ibmprivate dst 166.8.0.0/14
      acl FTP_ports port 21 20 1025-65535
      acl SSL_ports port 443 8443
      acl Safe_ports port 80          # http
      acl Safe_ports port 21          # ftp
      acl Safe_ports port 443         # https
      acl Safe_ports port 22
      acl Safe_ports port 8443
      acl Safe_ports port 70          # gopher
      acl Safe_ports port 210         # wais
      acl Safe_ports port 1025-65535  # unregistered ports
      acl Safe_ports port 280         # http-mgmt
      acl Safe_ports port 488         # gss-http
      acl Safe_ports port 591         # filemaker
      acl Safe_ports port 777         # multiling http
      acl CONNECT method CONNECT

      #
      # Recommended minimum Access Permission configuration:
      #
      # Deny requests to certain unsafe ports
      http_access deny !Safe_ports

      # Deny CONNECT to other than secure SSL ports
      http_access deny CONNECT !SSL_ports

      # Only allow cachemgr access from localhost
      http_access allow localhost manager
      http_access deny manager

      # We strongly recommend the following be uncommented to protect innocent
      # web applications running on the proxy server who think the only
      # one who can access services on "localhost" is a local user
      #http_access deny to_localhost

      # INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS
      ## Example rule allowing access from your local networks.

      # Adapt localnet in the ACL section to list your (internal) IP networks
      # from where browsing should be allowed
      http_access allow localnet
      http_access allow localhost

      # And finally deny all other access to this proxy
      # http_access deny all

      # Squid normally listens to port 3128
      #http_port 10.220.54.36:3128
      http_port 3128

      # Uncomment and adjust the following to add a disk cache directory.
      #cache_dir ufs /var/spool/squid 100 16 256

      # Leave coredumps in the first cache dir
      coredump_dir /var/spool/squid

      #
      # Add any of your own refresh_pattern entries above these.
      #
      refresh_pattern ^ftp:           1440    20%     10080
      refresh_pattern ^gopher:        1440    0%      1440
      refresh_pattern -i (/cgi-bin/|\?) 0     0%      0
      refresh_pattern .                 0     20%     4320
      ```
   c. Save the squid config file and start squid by using the `sudo systemctl start squid` command.

   d. You can stop squid by using the `sudo systemctl stop squid` command.

   e. You can restart squid by using the `sudo systemctl restart squid` command.


### Step 5: Customizing the VMs by using the cloud-init script (RHEL and SLES)
{: #virtual-server}

You can customize your RHEL and SLES VMs by running the cloud-init script.

1. Log in to your RHEL or SLES VM, by using the `ssh root@<External IP”>` command.
2. A readme file is generated in the `/usr/share/powervs-fls/powervs-fls-readme.md` location. For relevant information about variables that are required to run the cloud-init script, see the readme file.
3. Run the cloud-init script that is located in the `/usr/local/bin/` location. Run the script as _root_. You can switch the user to _root_ by using the `sudo su root` command.

   a. For	RHEL, run the following command:

    `. /usr/local/bin/rhel-cloud-init.sh -a Activation_Key -u Capsule_server_url -p Proxy_IP_and_port -o Org -t Deployment type`

     For information about the cloud-init script options and values, refer to the readme file that is generated in step 2 (`/usr/share/powervs-fls/powervs-fls-readme.md` location).

      -a = activation key

      -u = the URL of the RHEL capsule server you are registering against

      -p = "private_ip_of_powervs_vm":3128

      -o = organization associated with the activation key

      -t = deployment type of this VM (RHEL, RHEL-SAP, RHEL-SAP-NETWEAVER)

    b. For SLES, run the following command:

      `. /usr/local/bin/sles-cloud-init.sh -s RMT_Server_address -p private_ip_of_proxy_vm:3128`

      -s = the URL of the SLES Repository Mirroring Tool (RMT) server that you are using for registration

      -p = "private_ip_of_powervs_vm":3128

      If the system is already registered, you need to de-register the system before registering again by running the following two commands:
      `SUSEConnect --de-register`

      `SUSEConnect –cleanup`

      If the registration fails and the following note appears in the logs:

      `Could not register with SLES RMT servers, Please verify connection to the proxy server. If proxy is verified, it may be an issue with SLES RMT servers undergoing maintenance. If so, please try executing the command again within a few minutes`

      Then it could be a network issue and you should attempt to register again at a later time.

<!-- ## Passing user-defined scripts
{: #cloud-init-fls}

When you select a Full Linux Subscription (FLS) boot image while provisioning a {{site.data.keyword.powerSys_notm}} instance, you get the option to pass in user data during first boot runtime.

In the user data you can pass the custom content that allows you to customize the startup configuration for the specific instance.

The user data that you pass should follow the following conditions:
-  It should be uncompressed.
-  It should start with `#cloud-config`.
-  It should not exceed 63 Kb in size. -->
<!-- Q2 -->
