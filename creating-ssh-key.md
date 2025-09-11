---

copyright:
  years: 2024

lastupdated: "2025-09-11"

keywords: creating ssh key, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, video, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Generating and using an SSH key
{: #creating-ssh-key}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---



You can set up one or more Secure Shell (SSH) keys for root login when you create a new virtual machine (VM). The keys are loaded into the **authorized_keys** file in the root directory. By using SSH keys, you can securely log in to a VM. You must use the available operating system options to create SSH keys. To generate SSH keys on a Linux&reg; or Mac OS system, for example, you can use the standard `ssh-keygen` tool.
{: shortdesc}







In this example, the user created a public key on a Linux-based IBM Cloud compute instance by using the `ssh-keygen` tool:

```text
cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey
```





To use an SSH key with a VM-create operation, you must first add the public key to the {{site.data.keyword.powerSysFull}} instance by using the [`ibmcloud pi ssh-key create KEY_NAME --key KEY`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-create) command.


To add the generated public key and to set its scope by using the `visibility` attribute, enter the following command (replacing the example value with your own public key) :


```text
ibmcloud pi ssh-key create testkey --key "ssh-rsa AAAAB3NzaC
1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey" --visibility "account"
SSHKey created: testkey
```

To confirm that the key was successfully added, use the [`ibmcloud pi ssh list`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-ssh-key-list) command:

```text
ibmcloud pi ssh list
Name      Key                                          Visibility CreationDate
testkey   ssh-rsa AAAAB3NzaC1y...UIzYr3u+79n9 testkey  account    2019-07-26T18:21:56.030Z
```









## Setting the scope of an SSH key in a {{site.data.keyword.powerSys_notm}} workspace
{: #scope-ssh}

In a {{site.data.keyword.powerSys_notm}} workspace, when you create the SSH key, you can set the scope of an SSH key as `Workspace` or `Account`. When you set the scope of an SSH key as `Workspace`, the SSH key is available only in the workspace where it is created and not available in other workspaces. When you set the scope of an SSH key as `Account`, the SSH key is available in all the workspaces under the account. However, you can delete the SSH key only from the workspace in which it is created. Therefore, the security and privacy of the SSH key is improved.
{: shortdesc}



Complete the following steps to create and set the scope of an SSH key:

1. Open a workspace to add an SSH key from the {{site.data.keyword.powerSys_notm}} user interface.
2. Click **SSH keys** under **Compute**. The list of SSH keys that are associated with the workspace are displayed on the "SSH key" page.
3. Click **Create SSH Key**. The "New SSH key" page appears.
4. Enter a unique name in the **Key name** field.
5. Select one of the following options from the **Access setting** section to set the scope of the SSH key:
   - **Workspace**: The SSH key is visible only in the workspace in which it is created.
   - **Account**: The SSH key is visible to all the workspaces in the account. However, you can delete the SSH key only from the workspace in which it is created.
6. Enter a description about the SSH key in the **Description** field.
7. Enter the SSH key in the **Public key** field.
8. Click **Add SSH key**.

The SSH key is created and listed in the data table on the "SSH key" page. The **Access setting** column in the data table displays the scope of the SSH key as `Workspace` or `Account`.








## Creating an AIX VM instance
{: #create-ssh-key}

You can create an AIX VM instance with a configured SSH key by using the {{site.data.keyword.powerSys_notm}} CLI or the console. When you use an AIX stock image as your boot volume, the root password is not set. You must connect to the AIX VM and set the root password for the system. Without completing this step, SSH login as **root** appears as disabled. If you have public network access to the AIX VM, you can use telnet from a private cloud system and set the root password. For more information, see [IBM AIX V7.2 documentation](https://www.ibm.com/docs/en/aix/7.2){: external}.

### Creating an AIX VM with a configured SSH key using UI
{: #console-add-ssh}

You must [generate a public SSH key](#creating-ssh-key) before you can create an AIX VM with a configured SSH key.

1. Ensure that you have the necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions. For more information, see [Service access roles](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#service-access-roles).

2. Click **Virtual server instances** from the left navigation in the {{site.data.keyword.powerSys_notm}} user interface.

3. Click **Create instance**.

4. Under the **Virtual servers** section, select **Add SSH Keys**.

5. Enter a **Key name** and your previously generated **Public key**.

6. Click **Add SSH key** to add the SSH key.

7. Complete the rest of the fields to successfully create a new instance with a configured SSH key.

### Creating an AIX VM with a configured SSH key using CLI
{: #create-vm-cli}

You can create a new VM with the public key with the following command by replacing the options with your own:

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
{: #debug-connection}

If the SSH connection to the VM instance is failing, use the `-vvv` option of **ssh** command to determine the reason of the connection failure. Each additional verbose flag in the `-vvv` option increases the verbosity of the ssh client session and generates a large amount of data. Therefore, use a script session to capture the ssh log data so that log data is also sent to the **Standard output (STDOUT)**.

Run the following commands to start an SSH client debug session:
```text
# /usr/bin/script /tmp/ssh.{host}.debug
# /usr/bin/ssh -vvv {hostname/IP_of_ssh_server}
```

After you end the SSH client debug session, close the script session by pressing **Ctrl+D** or by entering the **exit** command.

## Additional support information
{: #extra-info-aix-vm}

Refer to the following support pages for additional information for different use cases:

- [Debugging sshd without impacting existing sshd sessions](https://www.ibm.com/support/pages/node/631957){: external}
- [Using IPsec rules to filter network traffic](https://www.ibm.com/support/pages/node/6590907){: external}
- [Downloading and installing or upgrading OpenSSL and OpenSSH](https://www.ibm.com/support/pages/node/720655){: external}
