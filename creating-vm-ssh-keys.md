---

copyright:
  years: 2019, 2020

lastupdated: "2020-06-10"

keywords: ssh key, AIX virtual machine, configure ssh key, new virtual server, public ssh key

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Creating an AIX virtual machine (VM) with SSH keys for root login
{: #create-vm}

You can set up one or more Secure Shell (SSH) keys for root login when you create new AIX virtual machines (VM). The keys are loaded into the root's **authorized_keys** file. SSH keys allow you to securely log in to a VM. You must use the available operating system options to create SSH keys. To generate SSH keys on a Linux&reg; or Mac OS system, for example, you can use the standard `ssh-keygen` tool.
{: shortdesc}

## Generating an SSH key
{: #ssh-setup}

In this example, the user created a public key on a Linux-based IBM Cloud compute instance by using the `ssh-keygen` tool:

```text
cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey
```

To use an SSH key with a VM-create operation, you must first add the public key to the {{site.data.keyword.powerSys_notm}} instance by using the [`ibmcloud pi key-create`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-key-create) command. To add the generated public key, enter the following command (replacing the example value with your own public key):

```text
ibmcloud pi key-create testkey --key "ssh-rsa AAAAB3NzaC
1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey"
SSHKey created: testkey
```

To confirm that the key was successfully added, use the [`ibmcloud pi keys`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-keys) command:

```text
ibmcloud pi key testkey
Name      Key                                          CreationDate
testkey   ssh-rsa AAAAB3NzaC1y...UIzYr3u+79n9 testkey  2019-07-26T18:21:56.030Z
```

## Creating an AIX VM instance
{: #create-ssh-key}

You can create an AIX VM instance with a configured SSH key by using the {{site.data.keyword.powerSys_notm}} CLI or the console. When you use an AIX stock image as your boot volume, the root password is not set. You must connect to the AIX VM and set the root password for the system. Without completing this step, SSH login as **root** appears as being *disabled*. If you have public network access to the AIX VM, you can use telnet from an on-premises system and set the root password. For more information, see [IBM AIX V7.2 documentation](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/navigation/welcome.html){: new_window}{: external}.

### Using the {{site.data.keyword.powerSys_notm}} user interface to create an AIX VM with a configured SSH key
{: #console-add-ssh}

You must [generate a public SSH key](#ssh-setup) before you can create an AIX VM with a configured SSH key.

1. Ensure that you have the proper account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions. For more information, see [Classic infrastructure permissions](/docs/iam?topic=iam-infrapermission#infrapermission) and [Managing device access](/docs/vsi?topic=virtual-servers-managing-device-access).

2. From the **Resource List**, select your service under **Services** to go to the **Manage** pane.

    ![IBM Cloud Resource List](./images/power-iaas-resource-list.png "IBM Cloud Resource List"){: caption="Figure 3. IBM Cloud Resource List" caption-side="bottom"}

3. Click **New instance**.

4. Under the **Virtual servers** section, select **Add SSH Keys**.

    ![SSH key navigation](./images/console-ssh-new.png "SSH key navigation"){: caption="Figure 5. SSH key navigation" caption-side="bottom"}

5. Enter a **Key name** and your previously generated **Public key**.

6. Click **Add SSH key** to add the SSH key.

7. Complete the rest of the fields to successfully create a new instance with a configured SSH key.

### Using the {{site.data.keyword.powerSys_notm}} CLI to create an AIX VM with a configured SSH key
{: #create-vm-cli}

You can create a new VM with the public key by using the following command (replacing the options with your own):

```text
ibmcloud pi instance-create keytest-vm --image AIX-7200-03-03 --memory 5 --networks "cloud.ibm.com" --processors 1 --processor-type shared --key-name testkey
```

In this example, the `ibmcloud pi instance-create` command created a new AIX VM with an IP address of _172.16.7.16_. You can now SSH to the AIX VM from a connected system, which is configured with the private key for `testkey`.

```text
ssh root@172.16.7.16
Enter passphrase for key '/home/keytest/.ssh/id_rsa':
Last login: Fri Jul 26 16:53:22 CDT 2019 on ssh from 10.150.0.11
*******************************************************************************
*                                                                             *
*                                                                             *
*  Welcome to AIX Version 7.2!                                                *
*                                                                             *
*                                                                             *
*  Please see the README file in /usr/lpp/bos for information pertinent to    *
*  this release of the AIX Operating System.                                  *
*                                                                             *
*                                                                             *
*******************************************************************************
# oslevel -s
7200-03-03-1914
```

You can find the `testkey` value in the **authorized_keys** file:

```text
cat .ssh/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey
```

### Debugging the connection
{: debug-connection}

If the SSH connection to the VM instance is failing, use the `-vvv` option of **ssh** command to determine the reason of the connection failure. Each additional verbose flag in the `-vvv` option increases the verbosity of the ssh client session and generates a large amount of data. Therefore, use a script session to capture the ssh log data so that log data is also sent to the **Standard output (STDOUT)**.

Run the following commands to start an SSH client debug session:
```text
# /usr/bin/script /tmp/ssh.{host}.debug
# /usr/bin/ssh -vvv {hostname/IP_of_ssh_server}
```

After you end the SSH client debug session, close the script session by pressing **Ctrl+D** or by entering **exit** command.
