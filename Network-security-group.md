---

copyright:
  year: 2025

lastupdated: "2025-05-27"

keywords: Network security group, Power virtual server NSG, PowerVS NSGs, network address groups, NAG, NAGs, rules, security rules, memebers, nsg rules evaluation order, NAG precedence, traffic matching

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security groups
{: #nsg}

---




{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

A network security group (NSG) is used to define security rules to allow or deny specific network traffic that is related to resources provisioned in an {{site.data.keyword.powerSysFull}} workspace. You can create NSGs in the Power Virtual Server environment to inspect and filter network traffic between resources in {{site.data.keyword.powerSys_notm}} workspaces.
{: shortdesc}



The existing workspaces can provide NSG support only after the data center in which the workspaces are deployed is enabled with the new metering code. The metering code must be based on Cloud Resource Name (CRN). For more information about the rollout schedule, see [Release notes](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-release-notes#Feb-2025).



Security rules in NSG define which inbound or ingress network traffic is allowed or denied from reaching members. Members are one or more network interfaces (NIC) at the subnet and virtual machine (VM) level. All outbound or egress traffic is automatically allowed.

Using NSGs in your {{site.data.keyword.powerSys_notm}} environment provides the following benefits:

- Enhances security and traffic control to limit unauthorized access to VMs and network resources
- Supports creation of specific security rules based on source, destination, port, and protocols (TCP, UDP, ICMP, and Any)
- Incurs no additional cost for using NSG; included as part of {{site.data.keyword.powerSys_notm}} workspaces
- Does not negatively impact on overall network throughput or network latency for any NSG members

## NSG components
{: #nsg-components}

Review the following topics to understand the components that are part of the NSG implementation:

- [Network address groups](#nag)
- [Members](#members)
- [Rules](#rules)

### Network address groups
{: #nag}

A network address group (NAG) is a collection of one or more external network address ranges, such as Classless Inter-Domain Routing (CIDRs), that are not directly related to provisioned network resources in your {{site.data.keyword.powerSys_notm}} workspace. NAGs are used to categorize external network address ranges, such as those accessible over Transit Gateway or natively by PER, such as [IBM Cloud Private endpoints](https://www.ibm.com/docs/en/cloud-private/3.2.x?topic=cluster-cloud-private-endpoints).

NAGs are used as reference points in NSG rules to simplify NSG implementation by grouping multiple external IP addresses, subnets, or virtual network segments under a single entity (NAG). Instead of listing multiple IP addresses or subnets in an NSG security rule, you can refer to a NAG to apply the same rule to all addresses in that group.

Using NAGs provide the following benefits:

- Simplifies management of NSG rules for external network addresses
- Reduces complexity when you apply security policies across multiple addresses
- Improves scalability, as you can add new IP addresses, subnets, or virtual network segments to an NAG without modifying the NSG rules

### Members
{: #members}

Members are one or more network interfaces that are provisioned in your {{site.data.keyword.powerSys_notm}} workspace. A network interface can be identified by either its Ethernet MAC address or IPv4 address. The same network interface must not be added as a member to two different NSGs, one using the MAC address and the other using the IPv4 address. Doing so can lead to unexpected behavior.

NSGs are a collection of members and security rules. For more information, see [rules](#rules).

An NSG member can only be associated with a single NSG. A provisioned network resource cannot belong to multiple NSGs concurrently.
{: note}

### Rules
{: #rules}

Rules or security rules define the inbound network traffic that is allowed or denied from reaching members of an NSG. By default, all inbound network traffic is denied and does not reach any member of an NSG unless security rules are explicitly defined. To learn more about defining rules to allow inbound traffic, see [Creating a new rule on an NSG](#creating-a-new-rule-on-an-nsg).


All outbound traffic is automatically allowed.
{: note}

## Network traffic rules and precedence in NSG
{: #traffic-rules-prec}

Review the following topics to understand how network traffic and security rules are processed and prioritized when NSG is implemented in a {{site.data.keyword.powerSys_notm}} workspace:

- [Rules evaluation order](#rules-eval-order)
- [NAG precedence in traffic matching](#nag-precedence)

### Rules evaluation order
{: #rules-eval-order}

The order in which a rule identifies inbound network traffic to be allowed or denied depends on the following key factors:
{: shortdesc}

- Deny rules are always evaluated first and take the highest precedence. If a Deny rule matches the traffic, the traffic is immediately blocked and the evaluation stops, regardless of any existing Allow rules.
- The system processes allow rules only after it completes processing deny rules. If no Deny rules are matched, the system proceeds to evaluate the Allow rules.
- If multiple Allow rules overlap, the first matching rule in the list is respected and applied. Overlapping rules do not cause conflicts. For example,
     - **Rule A**: Allow TCP `All`.
     - **Rule B**: Allow TCP `Port 22`.

       **Result**: Either rule might be applied, depending on which rule is matched first.

- Traffic that does not match any Allow rules is denied by default, following the implicit Deny rule.

### NAG precedence in traffic matching
{: #nag-precedence}

Review the following information to understand how inbound network traffic is matched to NAGs:
{: shortdesc}

- Inbound network traffic is matched to the most specific CIDR in any custom NAGs. When Allow or Deny rules for an NAG is evaluated, the source IP address is matched against the most specific CIDR in a custom NAG and not the default NAG (`0.0.0.0/0`).

- If a source IP falls in a more specific NAG, it must have an explicit NSG rule allowing network traffic from that NAG.
- If a more specific CIDR exists in a custom NAG, relying on the default NAG (`0.0.0.0/0`) does not allow inbound traffic.

For example, consider a remote system and a custom NAG with the following configuration:

- Remote system with the IP address `10.55.55.2`.
- Existing custom NAG with the CIDR `10.55.55.0/24`.

To allow traffic from `10.55.55.2`, an NSG rule must explicitly allow traffic from the custom NAG (`10.55.55.0/24`). This traffic does not match against the default NAG (`0.0.0.0/0`).

For more information about working with NAGs, see [Creating and managing NAGs in a workspace](#create-manage-nag).

## Setting up network security groups in a workspace
{: #setting-nsg-ws}

When you provision a workspace in your {{site.data.keyword.powerSys_notm}} environment, a default NSG and NAG are automatically created to allow bidirectional communication between the existing network interfaces in that workspace.
{: shortdesc}

Review the following topics to understand the various aspects of setting up, configuring, and managing NSGs:

- [Enabling or disabling NSG in a workspace](#enable-disable-nsg)
- [Creating and managing NSGs in a workspace](#create-manage-NSG)
- [Creating and managing NAGs in a workspace](#create-manage-nag)
- [Managing rules in an NSG](#create-manage-ib-rules)
- [Adding members to an NSG and managing them](##add-manage-memebers-nsg)

### Enabling or disabling NSG in a workspace
{: #enable-disable-nsg}

You can enable or disable the NSG feature in PER and enhanced CRN-enabled workspaces. However, you cannot enable NSG on previous, manual, VPN, or Cloud Connection workspaces.
{: shortdesc}

To determine whether your {{site.data.keyword.powerSys_notm}} workspace has the prerequisites to support NSGs, run the following IBM Cloud CLI command:

```sh
ibmcloud resource service-instance <WORKSPACE_CRN> -o json
```
{: pre}

Verify that the `resourceCRNs` property is present and its value is set to `true`:

```sh
"extensions": {
            "resourceCRNs": true
        },
```
{: pre}

To enable or disable the NSG feature on an existing workspace, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Click **workspaces** in the left navigation menu.
3. Select the workspace on which you want to enable or disable the NSG feature. The Workspace details pane is displayed.
4. Set the Network security groups feature to **Enabled** or **Disabled**.

When the NSG feature is enabled on a workspace, a default NSG is automatically created containing members of any existing NIC attachments in the workspace with two rules. The first rule allows all bidirectional communication (`Protocol=ALL`) from other members in the “default” NSG. The second rule allows all bidirectional communication (`Protocol=ALL`) with the “default” NAG (`0.0.0.0/0` network CIDR outside of the workspace).




The default rules can be deleted to achieve complete isolation between members in the same NSG, as well as from external addresses. When the default rules are deleted, all inbound traffic is denied by default. To delete these rules, complete the steps that are listed in the [Deleting rules from an existing NSG](#delete-rule-nsg) section.
{: tip}

### Creating and managing NSGs in a workspace
{: #create-manage-NSG}

You can create an NSG in your workspace either with the default configuration without defining any rules or members added to it, or you can create an NSG with inbound rules defined and members added during the NSG creation.
{: shortdesc}

### Creating an NSG with the default configuration
{: #create-nsg-default}

When you create an NSG in your workspace, you are not required to mandatorily define security rules or add members to the NSG. However, after an NSG is created with default settings, you can add rules and members to it later.
{: shortdesc}

By default, all inbound network traffic is denied and does not reach any member of the network security group. To create an NSG with default configuration, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the left navigation menu.
3. Select a workspace in which you want to create the NSG.
4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.
5. Click **Create network security group**. The Create network security group pane is displayed.
6. In the details section, enter a name for the network security group and click **Continue**. To define **Inbound security rules** and add **Members** to the NSG later, click **Continue** > **Finish** > **Create**.

### Creating an NSG with inbound rules and members
{: #create-nsg-custom}

To allow or deny inbound traffic, inbound rules must be explicitly defined. To create and define an NSG with inbound rules and members, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the left navigation menu.

3. Select a workspace in which you want to create the NSG.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Click **Create network security group**. The Create network security group pane is displayed.

6. In the Details section, enter a name for the network security group and click **Continue**.

7. In the Inbound rules (optional) section, click **Create rule**. The Create rule pane is displayed.

8. Select any of the following actions:
     - **Allow**: Use this option to allow network traffic from the specified Remote.
     - **Deny**:  Use this option to create traffic exceptions by overriding the allow rules.

9. Select one of the following protocols based on the type of traffic that you want to control:
      - **Transmission Control Protocol (TCP)**: Ideal for reliable, connection-oriented traffic such as web (HTTP/HTTPS), SSH, RDP, FTP, and databases. This protocol guarantees that all sent packets reach the destination and in the correct order.

      - **User Datagram Protocol (UDP)**: Ideal for real-time communication, fast, and connection-less traffic such as DNS, VoIP, network monitoring, video streaming, and gaming. This protocol does not guarantee delivery, order, or error correction.

      - **Internet Control Message Protocol (ICMP)**: Ideal for network diagnostics such as `ping` and `traceroute`. Unlike TCP or UDP, ICMP does not support data transmission between applications.

      - **Any**: Ideal for creating rules that applies to any protocol over a specific port or a set of ports. However, this option does not provide control over specific protocol-based security.

10. Depending on the protocol that you select from the list in the previous step, complete the following steps:
      - **TCP**
          1. **Remote**: Select a network security group or network address group to allow or deny traffic for the rule. If the network address group that you want is unavailable, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates from. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.
          4. **Allowed/Denied flags**: You can use the Advanced option to select one or more TCP flags from the list. Supported flags are:
                - `ack`
                - `fin`
                - `rst`
                - `syn`

      - **UDP**
          1. **Remote**: Select a network security group or network address group to allow or deny traffic for the rule. If you do not see the network address group that you want, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.

      - **ICMP**
          1. **Remote**: Select a network security group or network address group to allow or deny traffic for the rule. If the network address group that you want is unavailable, click **Create network address group** to create one.

          2. **ICMP Message type**: Select the required message type from the list. Supported types are:
                - `all`
                - `echo`
                - `echo-reply`
                - `source-quench`
                - `time-exceeded`
                - `destination-unreach`

      - **Any**
          1. **Remote**: Select a network security group or network address group to allow or deny traffic for the rule. If the network address group that you want is unavailable, click **Create network address group** to create one.

11.	Click **Create rule**.
12.	Click **Continue** to add members to the NSG.

13.	In the Members (optional) section, click **Add member**. Existing virtual server instances that are part of the workspace is listed. If you do not see any virtual servers listed, you can create one by competing the steps that are provided at [Creating an IBM Power Virtual Server](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

    Adding members to a network security group allows you to control inbound network traffic to these members. A member can only be associated with one network security group at a time.
    {: note}

14.	Select the virtual server instance and click **Next**. A list of network interfaces that belong to the virtual server instance is displayed.

15.	 Select one or more network interfaces from the list and click **Add member**.

16.	Click **Finish**.

17.	Click **Create**. You can find the NSG that you created listed on the **Network security groups** tab.

After the NSGs are created, you can manage them by performing the following actions:
- [Renaming an NSG](#rename-nsg)
- [Deleting an NSG](#delete-nsg)

### Renaming an NSG
{: #rename-nsg}

To rename an NSG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG to rename.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Click the overflow menu (icon with 3 vertical dots) on the NSG entry that you want to rename and select **Edit**. The Edit network security group details pane is displayed.

6.	Enter a new name for the NSG and click **Save**.

### Deleting an NSG
{: #delete-nsg}

To delete a custom (user-created) NSG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG to delete.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Click the overflow menu (icon with 3 vertical dots) on the NSG entry that you want to delete and select **Delete**. The Delete network security group confirmation message box appears.

6.	Click **Delete** to initiate the deletion request. This action cannot be undone.

You cannot delete the default NSG that is created when you enable the NSG feature on a {{site.data.keyword.powerSys_notm}} workspace.
{: note}

When you delete a {{site.data.keyword.powerSys_notm}} workspace, all NSGs in that workspace are also deleted.
{: note}

When you remove a network or subnet that is attached to a VM, the NIC is also detached from all associated NSGs.
{: note}

You must delete all the NSGs and NAGs before you disable the NSG feature by using the CLI, or API, or Terraform.
{: remember}

### Creating and managing NAGs in a workspace
{: #create-manage-nag}

NAGs form a part of the inbound rules that defines inbound traffic from network addresses external to your {{site.data.keyword.powerSys_notm}} workspace to members of an NSG. Since NAGs are used to identify network traffic that is external to the {{site.data.keyword.powerSys_notm}} workspace, you can create NAGs in your workspace and add CIDR members to it. You can create up to 10 NAGs in a single workspace.

To create an NAG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace in which you want to create the NAG.

4.	Click **Network security groups** under Networking in the left navigation pane. The Network security groups pane is displayed.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed.

5.	Select the **Network address groups** tab. A list of existing NAGs is displayed.

6.	Click **Create network address group**. The Create network address group pane is displayed.

7.	Enter a name and user tags (optional) for the NAG. At this step, you can optionally choose to add members by adding external IP addresses through CIDR. Note that the same CIDR cannot be used in more than one NAG. Follow these guidelines for adding members using CIDR:

    - You must use a CIDR notation that is defined in [RFC 1518](https://datatracker.ietf.org/doc/html/rfc1518){: external} and [RFC 1519](https://datatracker.ietf.org/doc/html/rfc1519){: external} documents.
    - The valid CIDR format is `<IPv4 address>/<number>`. For example, `192.168.1.0/24` represents the IP range of `192.168.1.0 — 192.168.1.255` and `10.0.0.0/16` represents the IP range of `10.0.0.0—10.0.255.255`.
    - Click **Add another** to add more members.

    You cannot add more than three members when creating an NAG. More members can be added after the NAG is created.
    {: note}

    Besides customer-defined NAGs, a default NAG is available for convenience consisting of the 0.0.0.0/0 CIDR.
    {: note}

    CIDR `161.26.0.0/16` can be used to identify IBM Cloud IaaS private endpoints such as DNS, Linux® software repositories, and NTP.<br>
    CIDR `166.8.0.0/14` can be used to identify IBM Cloud PaaS private endpoints such as IBM Cloud Databases.
    {: tip}

8. Click **Create group**.

After the NAGs are created, you can manage them by performing the following actions:

- [Renaming an NAG](#rename-nag)
- [Deleting an NAG](#delete-nag)

### Renaming an NAG
{: #rename-nag}

To rename an NAG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NAG to rename.

4.	Click **Network security groups** under Networking in the left navigation pane.

4. In the navigation pane, click **Networking** > **Network security groups**.

5.	Select the **Network address groups** tab. A list of existing NAGs is displayed.

6.	Click the overflow menu (icon with 3 vertical dots) on the far right of the NAG entry that you want to rename and select **Edit**. The Edit network address group details pane is displayed.

7.	Enter a new name for the NAG and click **Save**.

### Deleting an NAG
{: #delete-nag}

To delete an NAG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NAG to be deleted.

4. In the navigation pane, click **Networking** > **Network security groups**.

5.	Select the **Network address groups** tab. A list of existing NAGs is displayed.

6.	Click the overflow menu (icon with 3 vertical dots) on the NAG entry that you want to delete and select **Delete**. The Delete network address group confirmation message box appears.

7.	Click **Delete** to initiate the deletion request. This action cannot be undone.

### Creating and managing inbound rules in an NSG
{: #create-manage-ib-rules}

You can manage inbound security rules in an NSG by performing the following operations:

- [Creating a rule on an NSG](#create-new-nsg-rule)
- [Cloning rules on an existing NSG](#clone-nsg-rules)
- [Deleting rules from an existing NSG](#delete-rule-nsg)

### Creating a rule on an NSG
{: #create-new-nsg-rule}

Rules can be created on NSGs at two points. First, when you are initially creating an NSG, and second, at a later point by revisiting the Network security group details page of an existing NSG. To create rules on NSGs when you are creating the NSG, complete the steps provided in the [Creating an NSG with inbound rules and members](#create-new-nsg-rule) section.

NSGs are stateless, and since all outbound traffic is automatically permitted, rules must be defined for all return packet that flows into NSG members from other NSGs or NAGs.
{: note}

To create rules on an existing NSG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG in which you want to create rules.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Select the NSG in which you want to create the rule. The Network security group detail of the selected NSG is displayed.

6.	In the Inbound rules section, click **Create rule**. The Create rule pane is displayed.

7.	Complete the steps provided in the [Creating an NSG with inbound rules and members](#create-nsg-custom}) section.

### Cloning rules on an existing NSG
{: #clone-nsg-rules}

To create an inbound rule with the same configuration as an existing inbound rule, you can clone the rules of an existing NSG. Note that only the rules in an NSG can be cloned and not the members. When you clone an existing rule, all properties such as action (allow or deny), protocol, remote, and source and destination port ranges, are copied to the new rule. The cloning process ensures that all rules in an NSG are transferred when a member is moved from one NSG to another.

You can also customize the cloned properties of a rule to create a different rule efficiently and quickly. To clone an existing rule, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG with the rules that you want to clone.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Select the NSG that contains the rule that you want to clone. The Network security group details page of the selected NSG is displayed.

6.	In the Inbound rules section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) which contains the rule to be cloned.

7.	Click the overflow menu (icon with 3 vertical dots) on the rule entry that you want to clone and select **Duplicate**. The Create rule pane is displayed.

8.	Click **Create** rule. The new rule is created with the exact same configuration. You can also create a rule with different configurations by making the necessary changes before you click **Create rule**.


### Deleting rules from an existing NSG
{: #delete-rule-nsg}

To delete a rule from an existing NSG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG with the rule that you want to delete.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Select the NSG with the rule that you want to delete. The Network security group details page of the selected NSG is displayed.

6.	In the Inbound rules section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) which contains the rule to delete.

8.	Click the overflow menu (icon with 3 vertical dots) on the rule entry that you want to clone and select **Delete**. The Delete network security group rule confirmation message box appears.

9.	Click **Delete** to initiate the deletion request. This action cannot be undone.

### Adding members to an NSG and managing them
{: #add-manage-memebers-nsg}

You can manage members that are associated with an NSG by performing the following operations:

- [Adding members to a network security group](#add-members-nsg})
- [Removing members from a network security group](#remove-members-nsg)

### Adding members to a network security group
{: #add-members-nsg}

You can add members to an NSG to control the inbound network traffic to the associated network interfaces.

Members can be added at two points. First, when you are initially creating an NSG, and second, at a later point by revisiting the Network security group details page of an existing NSG. To add members to an NSG when you are creating it, complete the steps provided in the [Creating an NSG with inbound rules and members](#create-nsg-custom) section.

To add members to an existing NSG, complete the following steps:

1.	Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2.	Click **Workspaces** in the left navigation menu.

3.	Select the workspace that contains the NSG for adding members.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5.	Select the NSG to which you want to add members. The Network security group details page of the selected NSG is displayed.

6.	In the Members section, click **Add member**. Existing virtual server instances that are part of the workspace is listed. If virtual servers are not listed, you can create a virtual server by completing the steps provided at [Creating an IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

A member can only be associated with one network security group at a time.
{: note}

7.	Select the virtual server instance and click **Next**. Existing network interfaces that are part of the virtual server instance are displayed.
8.	Select one or more network interfaces from the list and click **Add member**.
9.	Click **Create**.

### Removing members from an NSG
{: #remove-members-nsg}

To remove members that are associated with an NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the left navigation menu.

3. Select the workspace that contains the NSG from which you want to remove the members.

4. In the navigation pane, click **Networking** > **Network security groups**. The Network security groups page is displayed with a list of existing NSGs on the **Network security groups** tab.

5. Select the NSG from which you want to remove the members. The Network security group details page of the selected NSG is displayed.

6. In the Members section, click the delete icon against the member entry that you want to remove from the NSG. The Delete network security group member confirmation message box appears.

7.	Click **Delete** to initiate the deletion request. This action cannot be undone.


## Quotas and limitations
{: #quotas-limitations}

NSGs have the following limitations in the {{site.data.keyword.powerSys_notm}} environment:

- You can only create 10 NSGs and 10 NAGs in a single workspace. These quotas are defined at a data center level and can be increased, subject to standard limits through a [support ticket](https://cloud.ibm.com/unifiedsupport/supportcenter).

The support tickets to increase the quota are evaluated by customer support and {{site.data.keyword.powerSys_notm}} operations and are at the discretion of IBM.
{: note}




- A network port can be identified based on Ethernet MAC address or IPv4 address. A single network port must not be added to two different NSGs using the two different identifiers. Doing so results in unknown network traffic behavior, and it is not a supported configuration.




- A member can only be associated with one NSG at a time.



- You cannot add members to an NSG if their attached network interface (NIC) is assigned a public IP address. NSGs can only be applied to private networks.



## Security considerations
{: #security-con}

When the NSG feature is disabled on a {{site.data.keyword.powerSys_notm}} workspace, the system allows unrestricted communication between VMs and subnets in that workspace. Enabling the NSG feature on a workspace maintains this behavior but also allows you to control the network traffic with security rules to meet specific requirements.
