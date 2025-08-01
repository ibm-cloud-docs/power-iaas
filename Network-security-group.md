---

copyright:
  year: 2025

lastupdated: "2025-07-25"

keywords: Network security group, Power virtual server NSG, PowerVS NSGs, network address groups, NAG, NAGs, rules, security rules, memebers, nsg rules evaluation order, NAG precedence, traffic matching

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security groups
{: #nsg}

---




{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

A {{site.data.keyword.nsg-lc}} (NSG) is used to define security rules to allow or deny specific network traffic that is related to resources provisioned in an {{site.data.keyword.powerSysFull}} workspace. You can create NSGs in the Power Virtual Server environment to inspect and filter network traffic between resources in {{site.data.keyword.powerSys_notm}} workspaces.
{: shortdesc}

Security rules in NSG define which inbound or ingress network traffic is allowed or denied from reaching members. Members are one or more network interfaces (NIC) at the subnet and virtual machine (VM) level. All outbound or egress traffic is automatically allowed.

Using NSGs in your {{site.data.keyword.powerSys_notm}} environment provides the following benefits:

- Enhances security and traffic control to limit unauthorized access to VMs and network resources
- Supports creation of specific security rules based on source, destination, port, and protocols (TCP, UDP, ICMP, and Any)
- Incurs no additional cost for using NSG; included as part of {{site.data.keyword.powerSys_notm}} workspaces
- Does not negatively impact on overall network throughput or network latency for any NSG members



The existing workspaces can provide NSG support only after the data center in which the workspaces are deployed is enabled with the new metering code. The metering code must be based on Cloud Resource Name (CRN). For more information about the rollout schedule, see [Release notes](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-release-notes#Feb-2025).



## NSG components
{: #nsg-components}

Review the following topics to understand the components that are part of the NSG implementation:

- [{{site.data.keyword.nag-sc}}s](#nag)
- [Members](#members)
- [Rules](#rules)

### {{site.data.keyword.nag-sc}}s
{: #nag}

A {{site.data.keyword.nag-lc}} (NAG) is a collection of one or more external network address ranges, such as Classless Inter-Domain Routing (CIDRs), that are not directly related to provisioned network resources in your {{site.data.keyword.powerSys_notm}} workspace. NAGs are used to categorize external network address ranges, such as those accessible over Transit Gateway or natively by PER, such as [IBM Cloud Private endpoints](https://www.ibm.com/docs/en/cloud-private/3.2.x?topic=cluster-cloud-private-endpoints).

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

## Setting up {{site.data.keyword.nsg-lc}}s in a workspace
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

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace on which you want to enable or disable the NSG feature. The "Workspace details" panel is displayed.

4. Set the **Network security groups** switch to **Enabled** or **Disabled**.

When the NSG feature is enabled on a workspace, a default NSG is automatically created containing members of any existing NIC attachments in the workspace with two rules. The first rule allows all bidirectional communication (`Protocol=ALL`) from other members in the “default” NSG. The second rule allows all bidirectional communication (`Protocol=ALL`) with the “default” NAG (`0.0.0.0/0` network CIDR outside of the workspace).



Before you disable the {{site.data.keyword.nsg-lc}}s feature on a workspace, you must delete all the existing NSGs and NAGs, except the NSG and NAG that are tagged as **Default**.
{: important}



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

By default, all inbound network traffic is denied and does not reach any member of the {{site.data.keyword.nsg-lc}}. To create an NSG with default configuration, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.
3. Select the workspace in which you want to create the NSG. The "Workspace details" panel is displayed.
4. Click **View virtual servers**.
5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.
6. Click **Create network security group**. The "Create network security group" page is displayed.
7. In the General section, enter a name for the network security group in the **Name** field and click **Continue**.
8. To define **Inbound security rules** and add **Members** to the NSG later, click **Continue** > **Finish** > **Create**.

### Creating an NSG with inbound rules and members
{: #create-nsg-custom}

To allow or deny inbound traffic, inbound rules must be explicitly defined. To create and define an NSG with inbound rules and members, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace in which you want to create the NSG. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

6. Click **Create network security group**. The "Create network security group" panel is displayed.

7. In the General section, enter a name for the network security group in the **Name** field and click **Continue**.

8. In the Inbound rules (optional) section, click **Create rule**. The "Create rule" panel is displayed.

9. Select any of the following actions:
     - **Allow**: Use this option to allow network traffic from the specified Remote.
     - **Deny**:  Use this option to create traffic exceptions by overriding the allow rules.

10. Select one of the following protocols based on the type of traffic that you want to control:
      - **Transmission Control Protocol (TCP)**: Ideal for reliable, connection-oriented traffic such as web (HTTP/HTTPS), SSH, RDP, FTP, and databases. This protocol guarantees that all sent packets reach the destination and in the correct order.

      - **User Datagram Protocol (UDP)**: Ideal for real-time communication, fast, and connection-less traffic such as DNS, VoIP, network monitoring, video streaming, and gaming. This protocol does not guarantee delivery, order, or error correction.

      - **Internet Control Message Protocol (ICMP)**: Ideal for network diagnostics such as `ping` and `traceroute`. Unlike TCP or UDP, ICMP does not support data transmission between applications.

      - **Any**: Ideal for creating rules that apply to any protocol over a specific port or a set of ports. However, this option does not provide control over specific protocol-based security.

11. Depending on the protocol that you select from the list in the previous step, complete the following steps:
      - **TCP**
          1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If the {{site.data.keyword.nag-lc}} that you want is unavailable, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates from. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.
          4. **Allowed/Denied flags**: You can use the Advanced option to select one or more TCP flags from the list. Supported flags are:
                - `ack`
                - `fin`
                - `rst`
                - `syn`

      - **UDP**
          1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If you do not see the {{site.data.keyword.nag-lc}} that you want, click **Create network address group** to create one.

          2. **Source port range**: Specify the range of ports from which the inbound traffic originates. The valid range is `1–65535`.
          3. **Destination port range**: Specify the range of ports on which the inbound traffic is received. The valid range is `1–65535`.

      - **ICMP**
          1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If the {{site.data.keyword.nag-lc}} that you want is unavailable, click **Create network address group** to create one.

          2. **ICMP Message type**: Select the required message type from the list. Supported types are:
                - `all`
                - `echo`
                - `echo-reply`
                - `source-quench`
                - `time-exceeded`
                - `destination-unreach`

      - **Any**
          1. **Remote**: Select a {{site.data.keyword.nsg-lc}} or {{site.data.keyword.nag-lc}} to allow or deny traffic for the rule. If the {{site.data.keyword.nag-lc}} that you want is unavailable, click **Create network address group** to create one.

12. Click **Create rule**.
13. Click **Continue** to add members to the NSG.

14. In the Members (optional) section, click **Add member**. All the existing virtual server instances that are part of the workspace is listed. If you do not see any virtual servers listed, you can create one by competing the steps that are provided at [Creating an IBM Power Virtual Server](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

    Adding members to a {{site.data.keyword.nsg-lc}} allows you to control inbound network traffic to these members. A member can only be associated with one {{site.data.keyword.nsg-lc}} at a time.
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

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG to rename. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

6. Click the overflow menu (icon with 3 vertical dots) on the NSG entry that you want to rename and select **Edit**. The "Edit network security group details" panel is displayed.

7. Enter a new name for the NSG in the **Name** field and click **Save**.



### Cloning an NSG
{: #clone-nsg}

When you clone an NSG, a new {{site.data.keyword.nsg-lc}} is created with the same rules and member configurations as the original NSG from which it was cloned. To clone an NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG to be cloned. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Click the overflow menu (icon with 3 vertical dots) on the NSG entry that you want to clone and select **Clone**. The "Clone network security group" dialog is displayed.

6. Enter a name for the NSG in the **Name** field and click **Clone**.




### Deleting an NSG
{: #delete-nsg}

You can delete the NSGs that you have created. However, you cannot delete the default NSG that is created when the NSG feature is enabled on a {{site.data.keyword.powerSys_notm}} workspace.



You cannot delete an NSG or NAG until all the associated rules and members are removed. For more information, see [Deleting rules from an existing NSG](#delete-rule-nsg) and [Removing members from an NSG](#remove-members-nsg).
{: important}



To delete a NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG to delete. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups page" is displayed with a list of the existing NSGs on the **Network security groups** tab.

6. Click the overflow menu (icon with 3 vertical dots) on the NSG entry that you want to delete and select **Delete**. The "Delete network security group" confirmation message box appears.

7. Click **Delete** to initiate the deletion request. This action cannot be undone.


When you delete a {{site.data.keyword.powerSys_notm}} workspace, all NSGs in that workspace are also deleted.
{: important}



### Creating and managing NAGs in a workspace
{: #create-manage-nag}

NAGs form a part of the inbound rules that defines inbound traffic from network addresses external to your {{site.data.keyword.powerSys_notm}} workspace to members of an NSG. Since NAGs are used to identify network traffic that is external to the {{site.data.keyword.powerSys_notm}} workspace, you can create NAGs in your workspace and add CIDR members to it. You can create up to 10 NAGs in a single workspace.

To create an NAG, complete the following steps:

1 Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace in which you want to create the NAG. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed.

6. Select the **Network address groups** tab. A list of the existing NAGs is displayed.

7. Click **Create network address group**. The "Create network address group" panel is displayed.

8. Enter a name in the **Name** field for the NAG. Optionally, you can provide user tags in the **User tags (optional)** field.

9. Optionally, you can use the **CIDR** field to add members by adding external IP addresses through CIDR. Note that the same CIDR cannot be used in more than one NAG. Follow these guidelines for adding members using CIDR:

    - You must use a CIDR notation that is defined in [RFC 1518](https://datatracker.ietf.org/doc/html/rfc1518){: external} and [RFC 1519](https://datatracker.ietf.org/doc/html/rfc1519){: external} documents.
    - The valid CIDR format is `<IPv4 address>/<number>`. For example, `192.168.1.0/24` represents the IP range of `192.168.1.0 — 192.168.1.255` and `10.0.0.0/16` represents the IP range of `10.0.0.0—10.0.255.255`.
    - Click **Add another** to add more members.

    You cannot add more than three members when creating an NAG. More members can be added after the NAG is created.
    {: note}

    Besides customer-defined NAGs, a default NAG is available for convenience consisting of the 0.0.0.0/0 CIDR.
    {: note}

    CIDR `161.26.0.0/16` can be used to identify IBM Cloud IaaS private endpoints such as DNS, Linux® software repositories, and NTP. CIDR `166.8.0.0/14` can be used to identify IBM Cloud PaaS private endpoints such as IBM Cloud Databases.
    {: tip}

8. Click **Create group**.

After the NAGs are created, you can manage them by performing the following actions:

- [Renaming an NAG](#rename-nag)
- [Deleting an NAG](#delete-nag)

### Renaming an NAG
{: #rename-nag}

To rename an NAG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NAG to rename. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**.

6. Select the **Network address groups** tab. A list of the existing NAGs is displayed.

7. Click the overflow menu (icon with 3 vertical dots) on the far right of the NAG entry that you want to rename and select **Edit**. The "Edit network address group details" panel is displayed.

7. Enter a new name for the NAG and click **Save**.

### Deleting an NAG
{: #delete-nag}

To delete an NAG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NAG to be deleted. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**.

6. Select the **Network address groups** tab. A list of the existing NAGs is displayed.

7. Click the overflow menu (icon with 3 vertical dots) on the NAG entry that you want to delete and select **Delete**. The "Delete network address group" confirmation message box appears.

8. Click **Delete** to initiate the deletion request. This action cannot be undone.

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

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG in which you want to create rules. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Select the NSG in which you want to create the rule. The "Network security group details" page is displayed.

6. In the Inbound rules section, click **Create rule**. The "Create rule" panel is displayed.

7. Complete the steps provided in the [Creating an NSG with inbound rules and members](#create-nsg-custom}) section.

### Cloning rules on an existing NSG
{: #clone-nsg-rules}

To create an inbound rule with the same configuration as an existing inbound rule, you can clone the rules of an existing NSG. Note that only the rules in an NSG can be cloned and not the members. When you clone an existing rule, all properties such as action (allow or deny), protocol, remote, and source and destination port ranges, are copied to the new rule. The cloning process ensures that all rules in an NSG are transferred when a member is moved from one NSG to another.

You can also customize the cloned properties of a rule to create a different rule efficiently and quickly. To clone an existing rule, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG with the rules that you want to clone. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

5. In the navigation panel, click **Networking** > **Network security groups**. The 'Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

6. Select the NSG that contains the rule that you want to clone. The "Network security group details" page of the selected NSG is displayed.

7. In the Inbound rules section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) which contains the rule to be cloned.

8. Click the overflow menu (icon with 3 vertical dots) on the rule entry that you want to clone and select **Duplicate**. The "Create rule" panel is displayed.

9. Click **Create** rule. The new rule is created with the exact same configuration. You can also create a rule with different configurations by making the necessary changes before you click **Create rule**.


### Deleting rules from an existing NSG
{: #delete-rule-nsg}

To delete a rule from an existing NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG with the rule that you want to delete. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Select the NSG with the rule that you want to delete. The "Network security group details" page of the selected NSG is displayed.

6. In the Inbound rules section, select the tab (**TCP**, **UDP**, **ICMP**, or **Any**) which contains the rule to delete.

8. Click the overflow menu (icon with 3 vertical dots) on the rule entry that you want to clone and select **Delete**. The "Delete network security group rule" confirmation message box appears.

9. Click **Delete** to initiate the deletion request. This action cannot be undone.

### Adding members to an NSG and managing them
{: #add-manage-memebers-nsg}

You can manage members that are associated with an NSG by performing the following operations:

- [Adding members to a {{site.data.keyword.nsg-lc}}](#add-members-nsg})
- [Moving members from one NSG to another NSG](#move-members)
- [Removing members from a {{site.data.keyword.nsg-lc}}](#remove-members-nsg)

### Adding members to a {{site.data.keyword.nsg-lc}}
{: #add-members-nsg}

You can add members to an NSG to control the inbound network traffic to the associated network interfaces.

Members can be added at two points. First, when you are initially creating an NSG, and second, at a later point by revisiting the {{site.data.keyword.nsg-sc}} details page of an existing NSG. To add members to an NSG when you are creating it, complete the steps provided in the [Creating an NSG with inbound rules and members](#create-nsg-custom) section.

To add members to an existing NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of existing workspaces.

3. Select the workspace that contains the NSG for adding members. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Select the NSG to which you want to add members. The "Network security group details" page of the selected NSG is displayed.

6. In the Members section, click **Add member**. Existing virtual server instances that are part of the workspace is listed. If virtual servers are not listed, you can create a virtual server by completing the steps provided at [Creating an IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).

    A member can only be associated with one {{site.data.keyword.nsg-lc}} at a time.
    {: note}

7. Select the virtual server instance and click **Next**. All the existing network interfaces that are part of the virtual server instance are displayed.
8. Select one or more network interfaces from the list and click **Add member**.
9. Click **Create**.



### Moving members from one NSG to another NSG
{: #move-members}

You can use the **Move** option to transfer members from one NSG to another NSG in some of the following situations:

- **Security policy changes**: When security policies or requirements evolve and you need to apply updated rules to specific members without affecting other members in the original NSG.

- **Environment segmentation**: When you want to isolate certain members during network reconfiguration or restructuring, such as separating development, staging, and production environments. You can move members to different NSGs to achieve member isolation and meet compliance or operational requirements.

- **Access control adjustments**: When a member requires access to a different set of services or external networks. You can move the member to a new NSG with appropriate rules to ensure the required connectivity and permissions.

- **Incident response and troubleshooting**: When you respond to cybersecurity incidents or troubleshoot connectivity issues. You can move the affected member to a more restrictive or isolated NSG to contain the security threat and safely test network behavior.

When you move a network interface (member) from one {{site.data.keyword.nsg-lc}} to another, the change is applied instantly and does not require approval. After the member is successfully moved and associated with the new NSG, the rules of the new NSG take effect immediately.
{: important}

To move a member from one NSG to another NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of the existing workspaces.

3. Select the workspace that contains the NSG from which you want to move the members. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Select the NSG from which you want to move the members. The "Network security group details" page of the selected NSG is displayed.

6. In the Members section, click the overflow menu (icon with 3 vertical dots) on the member entry that you want to move and select **Move**. The "Move network interface" dialog is displayed.

7. From the **Target network security group** list, select the NSG to which you want to move the member.

8. Click **Move network interface**.



### Removing members from an NSG
{: #remove-members-nsg}

To remove members that are associated with an NSG, complete the following steps:

1. Open the Power Virtual Server user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Click **Workspaces** in the navigation panel. The Workspaces page is displayed with a list of the existing workspaces.

3. Select the workspace that contains the NSG from which you want to remove the members. The "Workspace details" panel is displayed.

4. Click **View virtual servers**.

4. In the navigation panel, click **Networking** > **Network security groups**. The "Network security groups" page is displayed with a list of the existing NSGs on the **Network security groups** tab.

5. Select the NSG from which you want to remove the members. The "Network security group details" page of the selected NSG is displayed.

6. In the Members section, click the delete icon against the member entry that you want to remove from the NSG. The "Delete network security group member" confirmation message box appears.

7. Click **Delete** to initiate the deletion request. This action cannot be undone.

When you remove a network interface or a subnet that is attached to a VM, the NIC is also detached from all associated NSGs.
{: note}

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
