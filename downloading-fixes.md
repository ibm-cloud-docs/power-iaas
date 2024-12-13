---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-03"

keywords: suma, fixes, updates, PTF, TL, SNDPTFORD, fix central, network intsall server

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Downloading fixes and updates
{: #downloading-fixes-updates}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

You must use the AIX [Service Update Management Assistant (SUMA)](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/install/serv_update_mgt.html){: external} or the IBM i `Send PTF Order (SNDPTFORD)` command to download fixes and updates from the IBM Fix Central website.
{: shortdesc}

If you'd like to download fixes and updates, you must complete one of the following actions:
- Put your virtual machine (VM) on the public network. You can add a public network [during](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) or [after](/docs/power-iaas?topic=power-iaas-modifying-instance#adding-removing-network) the provisioning stage. Depending on your VM, see the [SUMA tasks and the command-line](#suma-tasks-cli) section for information on the **suma** command or the [SNDPTFORD command](#sndptford-command).
- Set up another VM as an AIX [NIM server](/docs/power-iaas?topic=power-iaas-provisioning-nim) or an IBM i [Network installation Server](#ibmi-network-server).
- Set up another public-facing VM with an [HTTP/HTTPS proxy](#configuring-aix-proxy).

## Ordering fixes and updates for AIX VMs
{: #downloading-fixes-aix}

Learn more about ordering fixes and updates for AIX VMs by using SUMA.

### Understanding SUMA
{: #understanding-suma}
{: help}
{: support}

SUMA sets up an automated interface to download fixes and updates from a fix distribution website to your system. You can configure SUMA to periodically check the availability of specific new fixes and technology levels. With SUMA, you don't have to manually retrieve maintenance updates.

When you configure SUMA in an AIX logical partition (LPAR) or as the NIM master, SUMA establishes a connection to the fix distribution website and downloads the available service update.

To verify that SUMA can get through to the IBM fix servers, run the following command (from the AIX system where you want to download the fixes):

```code
/usr/esa/bin/verifyConnectivity -tw
```
If the tests fail, work with your network security team to determine why you are unable to access the servers.

You can access the SUMA configuration by running the [suma command](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/s_commands/suma.html){: external} or by using the `SMIT suma` fast path. When you create a SUMA policy, you must specify one of the following request types that specifies the type of download:
- **PTF**: Specifies a request to download a program temporary fix (PTF), such as U813941. Only certain PTFs can be downloaded as an individual file set. This limitation applies to PTFs that contain either the *bos.rte.install* or *bos.alt_disk_install.rte* file sets as well as those that are released in between Service Packs (SP). Otherwise, you must download the technology level (TL) or SP.
- **TL**: Specifies a request to download a specific TL (such as 7200-02).
- **SP**: Specifies a request to download a specific SP (such as 7200-02-00).
- **Latest**: Specifies a request to download the latest fixes. This value returns the latest SP or TL as specified in the **FilterML** attribute.

### Configuring SUMA to use the proxy settings
{: #configuring-aix-proxy}

Before you run the `suma` command to download any updates, ensure that the AIX LPAR is authenticated to access the internet and that your LPAR knows in which data centers it is running.

To make the LPAR aware in which data centers it is running, run the following command:

```text
#echo “COUNTRY_CODE = **” >> /var/suma/data/config.suma
```
{: codeblock}

```text
#export SUMA_COUNTRY_CODE=**
```
{: codeblock}

Where ** is the country code of your DC based on the following table:

| POD Location| Country | Country code |
|----------|---------|---------|
| Sao Paulo | Brazil | BR|
| Washington & Dallas | USA |	US |
| Toronto & Montreal | Canada | CA |
| London	| UK	| GB |
| Frankfurt |	Germany |	 DE |
| Madrid	| Spain	| ES |
| Sydney	| Australia |	 AU |
| Tokyo & Osaka |	Japan | JP |
| Chennai | India | IN |
{: caption="POD location with their respective country code" caption-side="top"}

To verify that the LPAR is connected to the internet, enter the following command:
```code
suma -x -a Action=Preview -a RqType=LatestCopy
```

The `suma` command allows you to preview only the download operation. When you run this command, files are not downloaded. If the LPAR is not authenticated to access the internet, the command returns an error message. For information on troubleshooting SUMA error messages, see [Troubleshooting SUMA error messages](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/install/serv_update_mgt.html#serv_update_mgt__section_troubleshoot_suma){: external}.

Complete the following steps to configure SUMA to use the proxy settings:

1. Ensure that the *bos.ecc_client.rte* file set is installed on the AIX LPAR by running the following command:

    ```code
    lslpp -h bos.ecc_client.rte
    ```

2. Determine whether the `config_conn_path` command is available in the `bos.ecc_client.rte` file set by running the following command:

    ```code
    lslpp -w /usr/ecc/bin/config_conn_path
    ```

3. Configure your proxy settings by completing the following steps:
   1. Run the `smit srv_conn` command.
   2. Select **Create/Change Service Configuration** and press **Enter**.
   3. Select **Create/Change Primary Service Configuration** and press **Enter**.
   4. Set the following fields in the SMIT interface:

    Configuring proxy settings:

    ```screen
    Type or select values in entry fields.
    Press Enter AFTER making all desired changes.
                                                               [Entry Fields]
      Connection type                                          [HTTP_Proxy]
      Test service configuration                              [Yes]

      If type is DIRECT_INTERNET, no entry required.

      If type is HTTP_PROXY,
            IP address                                        [xx.xx.xx.xx]
            Port number                                       [5026]
            Authentication user ID                            []
            Authentication password requested interactively.
    ```

    Where, *xx.xx.xx.xx* is the IP address of the proxy and *5026* is the port number that is used to connect to the proxy settings. When you press **Enter**, a test connection determines whether the AIX LPAR is authenticated to access the internet by using the proxy settings. The common values for proxy port number are *3138* or *8080*.

4. Run the `smit suma_config_base` command to access the SUMA base configuration SMIT interface. Verify the fields that are shown in the **Base Configuration** screen capture.

For the **Fixserver protocol** field, *https* is the only option. For the **Download protocol** field, *http* is the default option. You can change the default option to *https* for a secure connection. If you set the **Download protocol** to *https*, the downloads are slower but more secure because *HTTP* provides multi-threaded performance and *HTTPS* provides single-threaded performance.
{: important}

Base SMIT configuration:

```screen
                     Base Configuration

Type or select values in entry fields.
Press Enter AFTER making all desired changes.
                                                              [Entry Fields]
Screen output verbosity                                   [Info/Warnings/Errors]  +
Logfile output verbosity                                  [Verbose]               +
Notification email verbosity                              [Info/Warnings/Errors]  +
Remove superseded filesets on Clean?                      Yes                    +
Remove duplicate base levels on Clean?                     Yes                    +
Remove conflicting updates on Clean?                       Yes                    +
Fixserver protocol                                        https                   +
Download protocol                                         http                    +
Maximum log file size (MB)                                [1]                       #
Download timeout (seconds)                                [180]                     #
```

### SUMA tasks and the command line
{: #suma-tasks-cli}

The `suma` command can be used to perform various operations on a SUMA task or policy. An **RqType** parameter specifies the type of download that is being requested, such as a TL, SP, or Latest. You can use several flag options with the `suma` command to complete the following tasks:

- Create
- Edit
- List
- Schedule
- Unschedule
- Delete

To create and save a SUMA task by using the command line, enter the following command:

```screen
suma -w -a DisplayName=‘ AIX72TL2SP2‘ -a FilterML=‘7200-00‘
```

The command returns a task ID after the successful creation of a SUMA task:

```text
Task ID 10 created.
```

To create and schedule a task that downloads the latest fixes and adds a policy label through the **DisplayName** field (useful when you are listing policies through SMIT), enter the following command:

```screen
suma -s "30 2 15 * *" -a RqType=Latest   \
    -a DisplayName="Latest fixes - 15th Monthly"
```

## Using the Electronic Service Agent (ESA) to download fixes and updates for IBM i VMs
{: #downloading-fixes-ibmi}
{: help}
{: support}

Learn how to configure a [Universal Connection to IBM services](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzaji/rzaji_setup.htm){: external}. If you don't want to assign a public IP to an IBM i VM, you can use a multi-hop connection (proxy server) to download fixes and updates. You can also use the `SNDPTFORD` command and a network installation server to do the same.

### The SNDPTFORD command
{: #sndptford-command}

You can use the `SNDPTFORD` command to order and receive IBM-supplied fixes (or PTFs) for the IBM i environment and IBM-supplied applications. You can use this command over the electronic customer support configuration that uses TCP/IP connectivity through *Universal Connection*. You can use the `SNDPTFORD` command to order the following types of fixes and related information:

- Separate or accompanying cover letters
- Individual fixes
- Multiple fixes
- Cumulative PTF packages
- PTF groups
- PTF summaries
- Cross-reference summary lists
- Preventive service planning tips

For example, the following command sends a request for PTF numbers SI12345 and SI12346:

```text
SNDPTFORD PTFID((SI12345) (SI12346))
```

For more information, see [Send PTF Order (SNDPTFORD)](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/cl/sndptford.htm){: external} and [Ordering fixes by using the Send PTF Order command](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzam8/rzam8fixobtainsndptford.htm){: external}. If you can't put your IBM i VM on the network, set up a network install server as instructed in the next section.

### Setting up an IBM i network install server
{: #ibmi-network-server}

Before you can install or upgrade an IBM i system through the network, you must [set up a network installation server](/docs/power-iaas?topic=power-iaas-preparing-install-server). The network installation server contains images of the IBM i operating system, its internal code as well as licensed programs and PTFs.
