---

copyright:
  years: 2023

lastupdated: "2023-03-28"

keywords: creating ssh key, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, video, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Generating and using an SSH key
{: #creating-ssh-key}

In this example, the user created a public key on a Linux-based IBM Cloud compute instance by using the `ssh-keygen` tool:

```text
cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey
```

To use an SSH key with a VM-create operation, you must first add the public key to the {{site.data.keyword.powerSysFull}} instance by using the [`ibmcloud pi key-create`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-key-create) command. To add the generated public key, enter the following command (replacing the example value with your own public key):

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

<!-- Secure Shell (SSH) keys authenticate your access to a server that uses public-key cryptography and challenge-response authentication. By using SSH key pairs, you can authenticate your access to the server without sending your password over the network. You can also use it with automation since it allows for unattended server communication. When generating an SSH key-pair, a private key file and a public key file are created. The private key file must be secured in your workstation and the public key file is copied on to the remote server for authentication and communication.

You can set up one or more SSH keys for root login when you create virtual server instances. The keys are loaded into the root's **authorized_keys** file. SSH keys allow you to securely log in to a virtual server instance.

You can use the `ssh-keygen` tool to generate SSH keys. To generate an SSH key, complete the following steps:

1. Ensure that you have the proper account permissions and device access. Only the account owner, or a user with the Manage Users classic infrastructure permission, can adjust the permissions. For more information, see [Service access roles](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#service-access-roles).

2. Run the `ssh-keygen` command in your private cloud workstation. The following example generates a standard 2048-bit RSA key. The command prompts you for the location to store the key (default is $HOME/.ssh/) as well as a passphrase to secure the SSH key.

     ```text
     root@bck2:/etc# ssh-keygen
     Generating public/private rsa key pair.
     Enter file in which to save the key (/root/.ssh/id_rsa):
     Enter passphrase (empty for no passphrase):
     Enter same passphrase again:
     Your identification has been saved in /root/.ssh/id_rsa.
     Your public key has been saved in /root/.ssh/id_rsa.pub.
     The key fingerprint is:
     SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx root@bck2.example.com
     The key's randomart image is:
     +---[RSA 2048]----+
     |.  oo*%=+o..     |
     |.++.oX+=. .      |
     |..+ooo=. .       |
     |   E.+. .o.      |
     |    +   S..+     |
     |     . +. =      |
     |      o  = o     |
     |      .o+ +      |
     |       +o.       |
     +----[SHA256]-----+
     ```

     The `ssh-keygen` command in the example generates two keys in the ~/.ssh directory:

     ```text
     $ ls ~/.ssh
     id_rsa
     id_rsa.pub
     ```

     The id_rsa.pub file is the SSH public key file.

3. Go to the {{site.data.keyword.powerSys_notm}} private cloud for Power dashboard and click **SSH keys** in the navigation pane.

4. Click **Create SSH key**.

5. Specify a name in the **Key name** field and fill in the contents of your public key file in the **Public key** text box.

6. Click **Add SSH key**.

To add an SSH public key to the {{site.data.keyword.powerSys_notm}} private cloud for Power configuration by using CLI, use the `ibmcloud pi key-create` command.
When you create a virtual server instance, you can connect to the instance over SSH by using the IP address of the instance. For example:

```text
ssh root@172.16.xx.xx
```
## Debugging the connection
{: #debugging-connection}

If the SSH connection to the VM instance is failing, use the **-vvv** option of `ssh` command to determine the reason of the connection failure. Each additional verbose flag in the **-vvv** option increases the verbosity of the ssh client session and generates a large amount of data. Therefore, use a script session to capture the ssh log data so that log data is also sent to the Standard output (STDOUT).

Run the following commands to start an SSH client debug session:

```text
# /usr/bin/script /tmp/ssh.{host}.debug
# /usr/bin/ssh -vvv {hostname/IP_of_ssh_server}
```

After you end the SSH client debug session, close the script session by pressing Ctrl+D or by entering `exit` command.

-->

## Creating an AIX VM instance
{: #create-ssh-key}

You can create an AIX VM instance with a configured SSH key by using the {{site.data.keyword.powerSys_notm}} CLI or the console. When you use an AIX stock image as your boot volume, the root password is not set. You must connect to the AIX VM and set the root password for the system. Without completing this step, SSH login as **root** appears as being *disabled*. If you have public network access to the AIX VM, you can use telnet from a private cloud system and set the root password. For more information, see [IBM AIX V7.2 documentation](https://www.ibm.com/docs/en/aix/7.2){: external}.

### Creating an AIX VM with a configured SSH key using UI
{: #console-add-ssh}

You must [generate a public SSH key](#creating-ssh-key) before you can create an AIX VM with a configured SSH key.

1. Ensure that you have the proper account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions. For more information, see [Service access roles](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#service-access-roles).

2. Click **Virtual server instances** from the left navigation in the {{site.data.keyword.powerSys_notm}} user interface.

3. Click **Create instance**.

4. Under the **Virtual servers** section, select **Add SSH Keys**.

5. Enter a **Key name** and your previously generated **Public key**.

6. Click **Add SSH key** to add the SSH key.

7. Complete the rest of the fields to successfully create a new instance with a configured SSH key.

### Creating an AIX VM with a configured SSH key using CLI
{: #create-vm-cli}

You can create a new VM with the public key with the following command (replacing the options with your own):

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

After you end the SSH client debug session, close the script session by pressing **Ctrl+D** or by entering **exit** command.

## Additional support information
{: #extra-info-aix-vm}

Refer to the following support pages for additional information for different use cases:

- [Debugging sshd without impacting existing sshd sessions](https://www.ibm.com/support/pages/node/631957){: external}
- [Using IPSec rules to filter network traffic](https://www.ibm.com/support/pages/node/6590907){: external}
- [Downloading and installing or upgrading OpenSSL and OpenSSH](https://www.ibm.com/support/pages/node/720655){: external}
