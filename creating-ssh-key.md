---

copyright:
  years: 2023

lastupdated: "2023-03-28"

keywords: creating ssh key, power private cloud as a service, ppcaas, before you begin, terminology, video, how-to

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Generating and using an SSH key
{: #creating-ssh-key}

Secure Shell (SSH) keys authenticate your access to a server that uses public-key cryptography and challenge-response authentication. By using SSH key pairs, you can authenticate your access to the server without sending your password over the network. You can also use it with automation since it allows for unattended server communication. When generating an SSH key-pair, a private key file and a public key file are created. The private key file must be secured in your workstation and the public key file is copied on to the remote server for authentication and communication.

You can set up one or more SSH keys for root login when you create virtual server instances. The keys are loaded into the root's **authorized_keys** file. SSH keys allow you to securely log in to a virtual server instance.

You can use the `ssh-keygen` tool to generate SSH keys. To generate an SSH key, complete the following steps:

1. Ensure that you have the proper account permissions and device access. Only the account owner, or a user with the `Manager` service access role, can generate SSH keys. For more information, see [Service access roles](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#service-access-roles).
2. Run the `ssh-keygen` command in your on-premises workstation. The following example generates a standard 2048-bit RSA key. The command prompts you for the location to store the key (default is $HOME/.ssh/) as well as a passphrase to secure the SSH key.

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

3. Go to the Stratos for Power dashboard and click **SSH keys** in the navigation pane.
4. Click **Create SSH key**.
5. Specify a name in the **Key name** field and fill in the contents of your public key file in the **Public key** text box.
6. Click **Add SSH key**.

To add an SSH public key to the Stratos for Power configuration by using CLI, use the `ibmcloud pi key-create` command. 
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