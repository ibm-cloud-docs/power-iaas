---

copyright:
  year: 2024, 2026 

lastupdated: "2026-08-26"

keywords: Network security group, Power virtual server NSG, PowerVS NSGs, network address groups, NAG, NAGs, rules, security rules, members, nsg rules evaluation order, NAG precedence, traffic matching

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security groups in IBM {{site.data.keyword.powerSys_notm}}
{: #nsg}

---




{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

A {{site.data.keyword.nsg-lc}} (NSG) defines security rules to allow or deny specific network traffic for resources that are provisioned in an {{site.data.keyword.powerSysFull}} workspace. You can create NSGs to inspect and filter network traffic between resources in {{site.data.keyword.powerSys_notm}} workspaces.
{: shortdesc}

Security rules in an NSG define which inbound network traffic is allowed or denied from reaching members. Members are one or more network interfaces (NIC) at the subnet and virtual server instance (VSI) level. All outbound or egress traffic is automatically allowed.

Using NSGs in your {{site.data.keyword.powerSys_notm}} environment provides the following benefits:

- Enhances security and traffic control to limit unauthorized access to VSIs and network resources
- Supports creating specific security rules that are based on source, destination, port, and protocol (TCP, UDP, ICMP, and Any)
- Incurs no additional cost; NSG is included as part of {{site.data.keyword.powerSys_notm}} workspaces
- Does not negatively affect overall network throughput or network latency for any NSG members



Existing workspaces can support NSG only after the data center where the workspaces are deployed is updated to use the new metering code. The metering code must be based on cloud resource name (CRN). For more information about the rollout schedule, see [Release notes](/docs/power-iaas?topic=power-iaas-release-notes#Feb-2025).



## NSG components
{: #nsg-components}

Review the following components of the NSG implementation in {{site.data.keyword.powerSys_notm}}:

- [{{site.data.keyword.nag-sc}}s](#nag)
- [Members](#members)
- [Rules](#rules)

### {{site.data.keyword.nag-sc}}s
{: #nag}

A {{site.data.keyword.nag-lc}} (NAG) is a collection of one or more external network address ranges, such as Classless Inter-Domain Routing (CIDRs), that are not directly related to provisioned network resources in your {{site.data.keyword.powerSys_notm}} workspace. NAGs are used to categorize external network address ranges, such as those accessible over Transit Gateway or natively by PER, such as [IBM Cloud Private endpoints](https://www.ibm.com/docs/en/cloud-private/3.2.x?topic=cluster-cloud-private-endpoints).

NAGs serve as reference points in NSG rules and simplify NSG configuration by grouping multiple external IP addresses, subnets, or virtual network segments under a single entity. Instead of listing multiple IP addresses or subnets in an NSG rule, you can refer to a NAG to apply the same rule to all addresses in that group.

Using NAGs provides the following benefits:

- Simplifies management of NSG rules for external network addresses
- Reduces complexity when you apply security policies across multiple addresses
- Improves scalability, as you can add new IP addresses, subnets, or virtual network segments to an NAG without modifying the NSG rules

### Members
{: #members}

Members are one or more network interfaces that are provisioned in your {{site.data.keyword.powerSys_notm}} workspace. A network interface can be identified by its Ethernet MAC address or its IPv4 address. Do not add the same network interface as a member to two different NSGs, one identified by the MAC address and the other by the IPv4 address. Doing so can lead to unexpected behavior.

An NSG is a collection of members and security rules. For more information, see [rules](#rules).

An NSG member can only be associated with a single NSG. A provisioned network resource cannot belong to multiple NSGs concurrently.
{: note}

### Rules
{: #rules}

Security rules define the inbound network traffic that is allowed or denied from reaching members of an NSG. By default, all inbound network traffic is denied unless security rules are explicitly defined. To learn more about defining rules to allow inbound traffic, see [Creating a rule on an NSG](#create-new-nsg-rule).


All outbound traffic is automatically allowed.
{: note}

## Network traffic rules and precedence in NSG
{: #traffic-rules-prec}

Review the following topics to understand how network traffic and security rules are processed and prioritized in an NSG-enabled {{site.data.keyword.powerSys_notm}} workspace:

- [Rules evaluation order](#rules-eval-order)
- [NAG precedence in traffic matching](#nag-precedence)

### Rules evaluation order
{: #rules-eval-order}

The order in which a rule identifies inbound network traffic to be allowed or denied depends on the following key factors:
{: shortdesc}

- Deny rules are always evaluated first and take the highest precedence. If a deny rule matches the traffic, the traffic is immediately blocked and the evaluation stops, regardless of any existing allow rules.
- The system processes allow rules only after all deny rules are evaluated. If no deny rules are matched, the system proceeds to evaluate the allow rules.
- If multiple allow rules overlap, the first matching rule in the list is applied. Overlapping rules do not cause conflicts. For example,
     - **Rule A**: Allow TCP `All`.
     - **Rule B**: Allow TCP `Port 22`.

     **Result**: Either rule might be applied, depending on which rule is matched first.

- Traffic that does not match any allow rules is denied by default, following the implicit deny rule.

### NAG precedence in traffic matching
{: #nag-precedence}

Review the following information to understand how inbound network traffic is matched to NAGs:
{: shortdesc}

- Inbound network traffic is matched to the most specific CIDR in any custom NAGs. When allow or deny rules for an NAG are evaluated, the source IP address is matched against the most specific CIDR in a custom NAG and not the default NAG (`0.0.0.0/0`).

- If a source IP falls in a more specific NAG, it must have an explicit NSG rule allowing network traffic from that NAG.
- If a more specific CIDR exists in a custom NAG, relying on the default NAG (`0.0.0.0/0`) does not allow inbound traffic.

For example, consider a remote system and a custom NAG with the following configuration:

- Remote system with the IP address `10.55.55.2`.
- Existing custom NAG with the CIDR `10.55.55.0/24`.

To allow traffic from `10.55.55.2`, an NSG rule must explicitly allow traffic from the custom NAG (`10.55.55.0/24`). This traffic does not match against the default NAG (`0.0.0.0/0`).

For more information about working with NAGs, see [Creating and managing NAGs in a workspace](#create-manage-nag).

## Setting up {{site.data.keyword.nsg-lc}}s in a workspace
{: #setting-nsg-ws}

When you provision a workspace in your {{site.data.keyword.powerSys_notm}} environment, a default NSG and NAG are automatically created to allow bidirectional communication between the existing network interfaces in that workspace.
{: shortdesc}

Review the following topics to set up, configure, and manage NSGs:

- [Enabling or disabling NSG on a workspace](#enable-disable-nsg)
- [Creating and managing NSGs in a workspace](#create-manage-NSG)
- [Creating and managing NAGs in a workspace](#create-manage-nag)
- [Managing rules in an NSG](#create-manage-ib-rules)
- [Adding members to an NSG and managing them](#add-manage-members-nsg)

### Enabling or disabling NSG on a workspace
{: #enable-disable-nsg}

You can enable or disable the NSG feature on PER and enhanced CRN-enabled workspaces. However, you cannot enable NSG on non-PER, manual, VPN, or Cloud Connection workspaces.
{: shortdesc}

To determine whether your {{site.data.keyword.powerSys_notm}} workspace has the prerequisites to support NSGs, run the following IBM Cloud CLI command:

```sh
ibmcloud resource service-instance <WORKSPACE_CRN> -o json
```
{: pre}

Verify that the output contains the `resourceCRNs` property with a value of `true`:

```sh
"extensions": {
            "resourceCRNs": true
        },
```
{: pre}

To enable or disable the NSG feature on an existing workspace, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Locate the workspace on which you want to enable or disable the NSG feature, click the overflow menu (three vertical dots), and select **View details**. The "Workspace details" panel is displayed.

5. In the "Workspace details" panel, set the **Network security groups** toggle to **Enabled** or **Disabled**.

When the NSG feature is enabled on a workspace, a default NSG with two rules is automatically created. The default NSG includes all existing network interfaces (members) in the workspace. The first rule allows all inbound traffic from other members in the **Default local addresses** NSG. The second rule allows all inbound traffic from the **Default external addresses** NAG.



Before you disable the {{site.data.keyword.nsg-lc}}s feature on a workspace, you must delete all the existing NSGs and NAGs, except the NSG and NAG that are tagged as **Default**.
{: important}



You can delete the default rules to achieve complete isolation between members in the same NSG and from external addresses. When the default rules are deleted, all inbound traffic is blocked. To delete these rules, complete the steps that are listed in the [Deleting rules from an existing NSG](#delete-rule-nsg) section.
{: tip}

### Creating and managing NSGs in a workspace
{: #create-manage-NSG}

You can create an NSG with the default configuration (no rules or members), or you can define inbound rules and members when you create the NSG.
{: shortdesc}

### Creating an NSG with the default configuration
{: #create-nsg-default}

When you create an NSG in your workspace, you are not required to define security rules or add members. However, after an NSG is created with default settings, you can add rules and members to it later.
{: shortdesc}

By default, all inbound network traffic is denied and does not reach any member of the {{site.data.keyword.nsg-lc}}. To create an NSG with the default configuration, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace in which you want to create the NSG. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

   Before you can create an NSG, you must enable the NSG feature on the workspace. If NSG is not enabled, the **Create network security group** button is unavailable. To enable NSG on a workspace, see [Enabling or disabling NSG on a workspace](#enable-disable-nsg).
   {: note}

6. Click **Create network security group**. The "Create network security group" page is displayed.

7. In the **General** section, enter a name for the network security group in the **Name** field. Optionally, enter one or more tags in the **User tags** field to help organize and identify the NSG. Click **Continue**.

8. In the **Inbound rules (optional)** section, click **Continue** to skip adding rules.

   If you skip this step, a warning is displayed: *"All network traffic will be denied to members."* This is expected behavior. By default, all inbound traffic is denied until rules are defined. You can add rules later.
   {: note}

9. In the **Members (optional)** section, click **Finish**, and then click **Create**.

### Creating an NSG with inbound rules and members
{: #create-nsg-custom}

You must explicitly define inbound rules to allow or deny traffic. To create and define an NSG with inbound rules and members, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace in which you want to create the NSG. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Click **Create network security group**. The "Create network security group" panel is displayed.

7. In the General section, enter a name for the network security group in the **Name** field and click **Continue**.

8. In the Inbound rules (optional) section, click **Create rule**. The "Create rule" panel is displayed.

9. Select any of the following actions:
     - **Allow**: Use this option to allow network traffic from the specified Remote.
     - **Deny**: Use this option to create traffic exceptions by overriding the allow rules.

10. Select one of the following protocols based on the type of traffic that you want to control:
      - **Transmission Control Protocol (TCP)**: Ideal for reliable, connection-oriented traffic such as web (HTTP/HTTPS), SSH, RDP, FTP, and databases. This protocol guarantees that all packets reach the destination in the correct order.

      - **User Datagram Protocol (UDP)**: Ideal for fast, real-time, and connectionless traffic such as DNS, VoIP, network monitoring, video streaming, and gaming. This protocol does not guarantee delivery, order, or error correction.

      - **Internet Control Message Protocol (ICMP)**: Ideal for network diagnostics such as `ping` and `traceroute`. Unlike TCP or UDP, ICMP does not support data transmission between applications.

      - **Any**: Ideal for creating rules that apply to any protocol over a specific port or a set of ports. However, this option does not provide control over specific protocol-based security.

11. Depending on the protocol that you select from the list in the previous step, complete the following steps:

      TCP
      :   1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If you do not see the {{site.data.keyword.nag-lc}} that you want, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.

        

          4. **Allowed/Denied flags**: You can use the **Advanced** section to select one or more TCP flags from the **Allowed/Denied flags** list to evaluate the incoming packets based on the selected flags. If you do not select any flags, the network fabric does not apply flag-based filtering. When you select multiple flags, the network fabric applies the rule only to the packets in which all the selected flags are present simultaneously. Therefore, the incoming packet must contain every flag that you have selected for the rule to take effect. You can select the following TCP flags:
                - `ack`
                - `fin`
                - `rst`
                - `syn`

        

      UDP
      :   1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If you do not see the {{site.data.keyword.nag-lc}} that you want, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.

      ICMP
      :   1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If you do not see the {{site.data.keyword.nag-lc}} that you want, click **Create network address group** to create one.

          2. **ICMP Message type**: Select the required message type from the list. Supported types are:
                - `all`
                - `echo`
                - `echo-reply`
                - `source-quench`
                - `time-exceeded`
                - `destination-unreach`

      Any
      :   1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If you do not see the {{site.data.keyword.nag-lc}} that you want, click **Create network address group** to create one.

12. Click **Create rule**.
13. Click **Continue** to add members to the NSG.

14. In the Members (optional) section, click **Add member**. All existing virtual server instances that are part of the workspace are listed. If you do not see any virtual servers listed, you can create one by completing the steps that are provided in the [Creating an IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) section.

    Adding members to a {{site.data.keyword.nsg-lc}} allows you to control inbound network traffic to the associated network interfaces. A member can only be associated with one {{site.data.keyword.nsg-lc}} at a time.
    {: note}

15. Select the virtual server instance and click **Next**. A list of network interfaces that belong to the virtual server instance is displayed.

16. Select one or more network interfaces from the list and click **Add member**.

17. Click **Finish**.

18. Click **Create**. You can find the NSG that you created listed on the **Network security groups** tab.

After the NSGs are created, you can manage them by performing the following actions:
- [Renaming an NSG](#rename-nsg)
- [Cloning an NSG](#clone-nsg)
- [Deleting an NSG](#delete-nsg)

### Renaming an NSG
{: #rename-nsg}

To rename an NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG that you want to rename. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Click the overflow menu (three vertical dots) on the NSG entry that you want to rename and select **Edit**. The "Edit network security group details" panel is displayed.

7. Enter a new name for the NSG in the **Name** field and click **Save**.



### Cloning an NSG
{: #clone-nsg}

When you clone an NSG, a new {{site.data.keyword.nsg-lc}} is created with the same rules and member configurations as the original. To clone an NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG that you want to clone. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Click the overflow menu (three vertical dots) on the NSG entry that you want to clone and select **Clone**. The "Clone network security group" dialog is displayed.

7. Enter a name for the NSG in the **Name** field and click **Clone**.




### Deleting an NSG
{: #delete-nsg}

You can delete any NSG that you created. However, you cannot delete the default NSG that is created when the NSG feature is enabled on a {{site.data.keyword.powerSys_notm}} workspace.



You cannot delete an NSG or NAG until all the associated rules and members are removed. For more information, see [Deleting rules from an existing NSG](#delete-rule-nsg) and [Removing members from an NSG](#remove-members-nsg).
{: important}



To delete an NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG that you want to delete. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Click the overflow menu (three vertical dots) on the NSG entry that you want to delete and select **Delete**. The Delete network security group confirmation message box appears.

7. Click **Delete** to initiate the deletion request. This action cannot be undone.


When you delete a {{site.data.keyword.powerSys_notm}} workspace, all NSGs in that workspace are also deleted.
{: important}



### Creating and managing NAGs in a workspace
{: #create-manage-nag}

NAGs form a part of the inbound rules that define inbound traffic from network addresses that are external to your {{site.data.keyword.powerSys_notm}} workspace to members of an NSG. Because NAGs identify network traffic that is external to the {{site.data.keyword.powerSys_notm}} workspace, you can create NAGs in your workspace and add CIDR addresses to them. You can create up to 10 NAGs in a single workspace.

To create an NAG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace in which you want to create the NAG. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed.

6. Select the **Network address groups** tab. A list of existing NAGs is displayed.

7. Click **Create network address group**. The "Create network address group" panel is displayed.

8. Enter a name in the **Name** field for the NAG. Optionally, you can provide user tags in the **User tags (optional)** field.

9. Optionally, enter one or more CIDR addresses in the **CIDR** field to add external IP addresses as members. The same CIDR cannot be used in more than one NAG.
    {: note}

    Follow these guidelines for adding members using CIDR:

    - You must use CIDR notation as defined in [RFC 1518](https://datatracker.ietf.org/doc/html/rfc1518){: external} and [RFC 1519](https://datatracker.ietf.org/doc/html/rfc1519){: external}.
    - The valid CIDR format is `<IPv4 address>/<number>`. For example, `192.168.1.0/24` represents the IP range of `192.168.1.0 — 192.168.1.255` and `10.0.0.0/16` represents the IP range of `10.0.0.0—10.0.255.255`.
    - Click **Add another** to add more members.

    You cannot add more than three members when creating an NAG. More members can be added after the NAG is created.
    {: note}

    In addition to customer-defined NAGs, a default NAG consisting of the `0.0.0.0/0` CIDR is available.
    {: note}

    You can use CIDR `161.26.0.0/16` to identify IBM Cloud IaaS private endpoints such as DNS, Linux® software repositories, and NTP. You can use CIDR `166.8.0.0/14` to identify IBM Cloud PaaS private endpoints such as IBM Cloud Databases.
    {: tip}

10. Click **Create group**.

After the NAGs are created, you can manage them by performing the following actions:

- [Renaming an NAG](#rename-nag)
- [Deleting an NAG](#delete-nag)

### Renaming an NAG
{: #rename-nag}

To rename an NAG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NAG that you want to rename. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**.

6. Select the **Network address groups** tab. A list of existing NAGs is displayed.

7. Click the overflow menu (three vertical dots) on the NAG entry that you want to rename and select **Edit**. The "Edit network address group details" panel is displayed.

8. Enter a new name for the NAG and click **Save**.

### Deleting an NAG
{: #delete-nag}

To delete an NAG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NAG that you want to delete. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**.

6. Select the **Network address groups** tab. A list of existing NAGs is displayed.

7. Click the overflow menu (three vertical dots) on the NAG entry that you want to delete and select **Delete**. The Delete network address group confirmation message box appears.

8. Click **Delete** to initiate the deletion request. This action cannot be undone.

### Creating and managing inbound rules in an NSG
{: #create-manage-ib-rules}

You can manage inbound security rules in an NSG by performing the following operations:

- [Creating a rule on an NSG](#create-new-nsg-rule)
- [Cloning rules on an existing NSG](#clone-nsg-rules)
- [Deleting rules from an existing NSG](#delete-rule-nsg)

### Creating a rule on an NSG
{: #create-new-nsg-rule}

You can create rules on an NSG in two ways: when you initially create the NSG, or later by revisiting the "Network security group details" page. To create rules when you are creating an NSG, see [Creating an NSG with inbound rules and members](#create-nsg-custom).

NSGs are stateless. Because all outbound traffic is automatically allowed, you must define rules for all return packets that flow into NSG members from other NSGs or NAGs.
{: note}

To create rules on an existing NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG in which you want to create rules. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Select the NSG in which you want to create the rule. The "Network security group details" page is displayed.

7. In the Inbound rules section, click **Create rule**. The "Create rule" panel is displayed.

8. Complete the steps provided in the [Creating an NSG with inbound rules and members](#create-nsg-custom) section.

### Cloning rules on an existing NSG
{: #clone-nsg-rules}

To create an inbound rule with the same configuration as an existing inbound rule, you can clone the rules of an existing NSG. Only the rules in an NSG can be cloned, not the members.
{: note}

When you clone an existing rule, all properties such as action (allow or deny), protocol, remote, and source and destination port ranges, are copied to the new rule. The cloning process ensures that all rules in an NSG are transferred when a member is moved from one NSG to another.

You can also customize the cloned properties of a rule to create a different rule efficiently and quickly. To clone an existing rule, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG with the rules that you want to clone. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Select the NSG that contains the rule that you want to clone. The "Network security group details" page is displayed.

7. In the **Inbound rules** section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) that contains the rule that you want to clone.

8. Click the overflow menu (three vertical dots) on the rule entry that you want to clone and select **Duplicate**. The "Create rule" panel is displayed.

9. Click **Create rule**. The new rule is created with the same configuration. You can also create a rule with different configurations by making the necessary changes before you click **Create rule**.


### Deleting rules from an existing NSG
{: #delete-rule-nsg}

To delete a rule from an existing NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG with the rule that you want to delete. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Select the NSG with the rule that you want to delete. The "Network security group details" page is displayed.

7. In the **Inbound rules** section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) that contains the rule that you want to delete.

8. Click the overflow menu (three vertical dots) on the rule entry that you want to delete and select **Delete**. The Delete network security group rule confirmation message box appears.

9. Click **Delete** to initiate the deletion request. This action cannot be undone.

### Adding members to an NSG and managing them
{: #add-manage-members-nsg}

You can manage members that are associated with an NSG by performing the following operations:

- [Adding members to a {{site.data.keyword.nsg-lc}}](#add-members-nsg)
- [Moving members from one NSG to another NSG](#move-members)
- [Removing members from a {{site.data.keyword.nsg-lc}}](#remove-members-nsg)

### Adding members to a {{site.data.keyword.nsg-lc}}
{: #add-members-nsg}

You can add members to an NSG to control the inbound network traffic to the associated network interfaces.

You can add members in two ways: when you initially create the NSG, or later by revisiting the **{{site.data.keyword.nsg-sc}} details** page of an existing NSG. To add members when you are creating an NSG, see [Creating an NSG with inbound rules and members](#create-nsg-custom).

To add members to an existing NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG for adding members. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Select the NSG to which you want to add members. The "Network security group details" page is displayed.

7. In the Members section, click **Add member**. Existing virtual server instances that are part of the workspace are listed. If virtual servers are not listed, you can create a virtual server by completing the steps provided at [Creating an IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

    A member can only be associated with one {{site.data.keyword.nsg-lc}} at a time.
    {: note}

8. Select the virtual server instance and click **Next**. All existing network interfaces for the virtual server instance are displayed.

9. Select one or more network interfaces from the list and click **Add member**.

10. Click **Create**.



### Moving members from one NSG to another NSG
{: #move-members}

You can use the **Move** option to transfer members from one NSG to another NSG in some of the following situations:

- **Security policy changes**: When security policies or requirements evolve, you can use the Move option to apply updated rules to specific members without affecting other members in the original NSG.

- **Environment segmentation**: During network reconfiguration or restructuring, such as separating development, staging, and production environments, you can move members to different NSGs to achieve member isolation and meet compliance or operational requirements.

- **Access control adjustments**: When a member requires access to a different set of services or external networks, you can move the member to a new NSG with appropriate rules to ensure the required connectivity and permissions.

- **Incident response and troubleshooting**: When you respond to cybersecurity incidents or troubleshoot connectivity issues, you can move the affected member to a more restrictive or isolated NSG to contain the security threat and safely test network behavior.

When you move a network interface (member) from one {{site.data.keyword.nsg-lc}} to another, the change is applied instantly and does not require approval. After the member is successfully moved and associated with the new NSG, the rules of the new NSG take effect immediately.
{: important}

To move a member from one NSG to another NSG, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}**, and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

4. Select the workspace that contains the NSG from which you want to move the members. The "Virtual server instances" page is displayed.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

6. Select the NSG from which you want to move the members. The "Network security group details" page is displayed.

7. In the Members section, click the overflow menu (three vertical dots) on the member entry that you want to move and select **Move**. The "Move network interface" dialog is displayed.

8. From the **Target network security group** list, select the NSG to which you want to move the member.

9. Click **Move network interface**.



### Removing members from an NSG
{: #remove-members-nsg}

To remove members that are associated with an NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG from which you want to remove the members. The "Virtual server instances" page is displayed.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of existing NSGs on the **Network security groups** tab.

5. Select the NSG from which you want to remove the members. The "Network security group details" page is displayed.

6. In the **Members** section, click the delete icon next to the member entry that you want to remove. The Delete network security group member confirmation message box appears.

7. Click **Delete** to initiate the deletion request. This action cannot be undone.

When you remove a network interface or a subnet that is attached to a VSI, the NIC is also detached from all associated NSGs.
{: note}

## Quotas and limitations
{: #quotas-limitations}

NSGs have the following limitations in the {{site.data.keyword.powerSys_notm}} environment:

- You can create a maximum of 10 NSGs and 10 NAGs in a single workspace. These quotas are defined at the data center level. To request an increase, open a [support ticket](https://cloud.ibm.com/unifiedsupport/supportcenter), subject to standard limits.




The support tickets for quota increases are evaluated by Customer Support and the Power Virtual Server operations team. IBM makes the final decision at its discretion and might decline the request depending on resource availability and the business justification.
{: important}










- A network interface can be identified by its Ethernet MAC address or IPv4 address. Do not add the same network interface to two different NSGs using different identifiers. Doing so can result in unexpected network traffic behavior and is not a supported configuration.




- A member can only be associated with one NSG at a time.



- You cannot add members to an NSG if their attached network interface (NIC) is assigned a public IP address. NSGs can only be applied to private networks.



## Security considerations
{: #security-con}

When the NSG feature is disabled on a {{site.data.keyword.powerSys_notm}} workspace, the system allows unrestricted communication between VSIs and subnets in that workspace. Enabling the NSG feature on a workspace maintains this behavior but also allows you to control the network traffic with security rules to meet specific requirements.
