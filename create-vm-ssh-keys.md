---

copyright:
  years: 2019

lastupdated: "2019-08-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# How to create a new VM with SSH keys for root login
{: #create-vm}

You can set up one or more SSH keys for root login when you create new virtual machines (VM) on an IBM Cloud instance. The keys are loaded into the root's **authorized_keys** file. SSH keys allow you to securely log in to a VM. You must use the available operating system options to create SSH keys. To generate SSH keys on a Linux&reg; or Mac OS system, for example, you can use the standard `ssh-keygen` tool.

## Setting up an SSH key to be used in a VM create operation
{: #ssh-setup}

In this example, the user created a public key on a Linux-based IBM Cloud compute instance by using the `ssh-keygen` tool:

```bash
cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey

```

To use an SSH key with a `VM create` operation, you must first add the public key to the cloud instance by using the [`ibmcloud pi key-create`](https://test.cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-key-create) command. To add the `ssh-keygen`-generated public key, enter the following command (replacing the public key value with your own):

**Important**: You must enclose the `--key` value in quotations.

```bash
ibmcloud pi key-create testkey --key "ssh-rsa AAAAB3NzaC
1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey"
SSHKey created: testkey
```

To confirm that the key was successfully added, use the [ibmcloud compute sshkeys list](https://test.cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-keys) command.

```bash
ibmcloud compute sshkeys list
Name      Key                                          CreationDate
testkey   ssh-rsa AAAAB3NzaC1y...UIzYr3u+79n9 testkey  2019-07-26T18:21:56.030Z
```

## Creating a VM instance with a configured SSH key
{: #create-ssh-key}
Now that you've added the key to the cloud instance, you can create a new VM with the key by using the following command:

```bash
ibmcloud pi instance-create keytest-vm --image AIX-7200-03-03 --processor-type shared --processors 0.5 --memory 5 --networks "ibmcloud" --keyname testkey
```

The preceding `VM create` operation resulted in a new AIX VM with an IP address of _172.16.7.16_. You can now SSH to the AIX VM from a connected system, which is configured with the private key for `testkey`. In the following example, the connecting system is an IBM Cloud compute instance with direct connectivity to the Power cloud instance network.

  ```
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
  #
  ```
  {: screen}

On this AIX VM, you can find the `testkey` value in the **authorized_keys** file.

```shell
cat .ssh/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtuQnQOc2k4zaGzE7b3xUMCjUy++s/9O9HE4fXSm7UNKoTY39zjQ8mhOwaA3HEo12tOdzdFDYHHWNOYufCcFFk61CAL6HyQGGClib1nFc1xUcgTI9Dee8zzaAsN8mIIr1CgbRELhvOsTv23U4QddpfjkcVoKfF0BAtxgauvooQdPZBoxa2rsD+BvcWnjglkYWG2aBbuzFvSl1fLMihjfej8w1lxbcsYEcJg2X96NJPLmLsEJ+XwoXfVuv0X4z8IoBzZ8UbyTlrDv73EAH34GViYfZFbrIaNnwnz/f/tuOKcINihH72YP+oZn9JeiHQ+hKpMqJAmOK2UIzYr3u+79n9 testkey
```
