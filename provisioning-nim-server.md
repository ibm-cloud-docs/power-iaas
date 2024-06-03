---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-22"

keywords: troubleshooting, NIM server, support, fixes, updates

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

# Setting up a Network Installation Management (NIM) server
{: #provisioning-nim}

You can provision an AIX virtual machine (VM) and use it as a NIM server for troubleshooting purposes or for downloading fixes and updates.

1. Determine the hostname and IP address of the system by using the following two commands, `hostname` and `ifconfig -a`.

    Determining your hostname and IP address:

    ```screen
    # hostname
    mpb-test-aix
    # ifconfig -a
    en0: flags=1e084863,814c0<UP, BROADCAST, NOTRAILERS, RUNNING, SIMPLEX, MULTICAST, GROUPPRT, 64BIT, CHECKSUM_OFFLOAD (ACTIVE), LARGESEND, CHAIN>
            inet 192.168.2.228 netmask 0xffffff00 broadcast 192.168.2.255
             tcp_sendspace 262144 tcp_recvspace 262144 rfc1323 1
    enl: flags=1e084863, 814c0<UP, BROADCAST, NOTRAILERS, RUNNING, SIMPLEX, MULTICAST, GROUPRT, 64BIT, CHECKSUM_OFFLOAD (ACTIVE), LARGESEND, CHAIN>
            inet6 fe80::205f: dfff:fe3e:dc56/64
             tcp_sendspace 262144 tcp_recvspace 262144 rfc1323 1
    sit0: flags=8100041<UP, RUNNING, LINKO>
            inet6 ::/96
    lo0: flags=e08084b, c0<UP, BROADCAST, LOOPBACK, RUNNING, SIMPLEX, MULTICAST, GROUPRT, 64 BIT, LARGESEND, CHAIN>
            inet 127.0.0.1 netmask 0xff000000 broadcast 127.255.255.255
            inet6 ::1%1/128
             tcp_sendspace 131072 tcp_recvspace 131072 rfc1323 1
    #
    ```

2. Using the information from the previous step, add an entry for your hostname and IP address into `/etc/hosts`. For example, `echo "192.168.0.15 aix-7100-05-04" >> /etc/hosts`.

3. Confirm that a valid `bos.vendor.profile` exists by copying the `/usr/lpp/bosinst/bos.vendor.profile` into the `installp/ppc` directory of the source repository.
    For example, `cp /usr/lpp/bosinst/bos.vendor.profile  /usr/sys/inst.images/installp/ppc/.`

4. Run the following command, `nim_master_setup -a device=/usr/sys/inst.images -a mk_resource=no`.

    Creating a NIM master:

    ```screen
    # echo "192.168.2.228 mpb-test-aix" >> /etc/hosts
    # nim_master_setup -a device=/usr/sys/inst.images -a mk_resource=no

    ####### NIM master setup #######
    During script execution, lpp_source and spot resource creation times may vary.
    To view the install log at any time during nim_master_setup, run the command: tail -f /var/adm/ras/nim.setup in a separate screen.
    Creating image.data file...
    ```

5. Once completed, the NIM master file set has been installed and the basic resource objects created. The administrator is now able to add more NIM clients and define resources.

    NIM master installation summary:

    ```screen
    +----------------------------------------+
                 Summaries
    +----------------------------------------+
    Installation Summary
    --------------------
    Name                    Level           Part            Event           Result
    bos.sysmgt.nim.master   7.2.3.17        USR             APPLY           SUCCESS
    ```

For more information, see [Setting up NIM to boot into maintenance mode](https://www.ibm.com/support/pages/setting-nim-boot-maintenance-mode){: external}. If you are unfamiliar with this process, create a [new support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Additional information
{: #add-info-nim}

 - [Migrating Clients using NIM on PowerVS](https://www.ibm.com/support/pages/node/7033798)(: external).
