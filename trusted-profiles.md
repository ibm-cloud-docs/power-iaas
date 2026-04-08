---

copyright:
  years: 2024, 2026

lastupdated: "2026-04-08"

keywords: trusted profiles, iam, identity and access management, compute resource, api keys, authentication, security

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding trusted profiles for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles}

A trusted profile is a security mechanism that removes the need to store static secrets, such as {{site.data.keyword.cloud_notm}} API keys, in potentially vulnerable environments like virtual machines. By using trusted profiles, you can grant {{site.data.keyword.powerSysFull}} virtual machines secure access to call other service API endpoints without storing credentials within the instance.
{: shortdesc}

## How trusted profiles work
{: #trusted-profiles-how-it-works}

A trusted profile establishes a compute identity for your {{site.data.keyword.powerSys_notm}} virtual machine and grants it access rights to call other service API endpoints. The profile is linked directly to the instance, creating a secure authentication mechanism based on the virtual machine's identity rather than stored credentials.

When your virtual machine needs to access {{site.data.keyword.cloud_notm}} services, a series of exchanges occur between internal components. A token is generated at the time of need based on metadata associated with the physical entity making the API call. This metadata includes:

* The virtual machine's Cloud Resource Name (CRN)
* The host server information

Because authentication relies on this metadata-based token generation, no private key or password needs to be stored within your calling application. This approach significantly reduces security risks by eliminating the need to manage and protect static credentials on your virtual machines.

## Benefits of using trusted profiles
{: #trusted-profiles-benefits}

Using trusted profiles with {{site.data.keyword.powerSys_notm}} provides several security and operational advantages:

Enhanced security
:   Eliminates the risk of credential exposure by removing the need to store API keys or passwords on virtual machines.

Simplified credential management
:   No need to rotate, update, or manage static credentials across your virtual machine fleet.

Dynamic authentication
:   Tokens are generated on demand based on the virtual machine's identity, ensuring that access is always current and tied to the specific instance.

Reduced attack surface
:   Without stored credentials, compromised virtual machines cannot expose long-lived secrets that could be used to access other resources.

Granular access control
:   Assign specific access rights to individual virtual machines through IAM policies and access groups.

## Managing trusted profiles
{: #trusted-profiles-management}

Trusted profiles are managed through IBM Identity and Access Management (IAM). You can create, configure, and manage trusted profiles from the [IBM Cloud Trusted Profiles UI](https://cloud.ibm.com/iam/trusted-profiles){: external}. Each profile can be associated with one or more {{site.data.keyword.powerSys_notm}} virtual machines, and you can assign access policies to control which IBM Cloud services and resources the virtual machines can access.

## Creating a trusted profile for {{site.data.keyword.powerSys_notm}}
{: #trusted-profiles-create}

To use trusted profiles with your {{site.data.keyword.powerSys_notm}} virtual machines, you must first create a trusted profile in IAM and configure it to work with PowerVS compute resources.

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for creating a trusted profile in the IAM console, including:
- Navigation path to trusted profiles
- Button labels and field names
- Options for configuring compute resources
- Steps for selecting PowerVS as the compute service type
- Configuration options for determining which VMs can use the profile
- Access policy assignment interface]

## Assigning access to a trusted profile
{: #trusted-profiles-assign-access}

You can control which IBM Cloud services and resources your {{site.data.keyword.powerSys_notm}} virtual machines can access by assigning access policies to the trusted profile. Access can be granted through individual access policies or by adding the compute resource identity to an existing access group.

### Assigning individual access policies
{: #trusted-profiles-individual-policies}

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for assigning individual access policies, including:
- Navigation to the trusted profile's access tab
- Button labels for assigning access
- Service selection interface
- Scope configuration options
- Role selection interface (platform and service roles)
- Confirmation and assignment steps]

### Adding to an access group
{: #trusted-profiles-access-groups}

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for adding trusted profiles to access groups, including:
- Navigation to access groups
- Interface for adding trusted profiles to a group
- Selection mechanism for choosing profiles
- Confirmation steps]

## Updating trusted profile access policies
{: #trusted-profiles-update-policies}

You can modify the access policies assigned to a trusted profile at any time to add, remove, or change roles.

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for updating access policies, including:
- Navigation to policy editing interface
- Actions menu options
- Role modification interface (checkboxes, dropdowns, etc.)
- Scope modification options
- Save/confirmation steps]

## Obtaining an instance identity token
{: #trusted-profiles-instance-token}

Your {{site.data.keyword.powerSys_notm}} virtual machine can obtain a short-lived instance identity token that can be exchanged for an IAM token. This token allows your workloads to authenticate with IBM Cloud services without storing credentials.

The instance identity token is valid for 5 minutes by default and is generated based on your virtual machine's metadata.

[API DETAILS NEEDED: Provide exact API endpoint, request format, and response format for obtaining instance identity tokens from the metadata service, including:
- Metadata service endpoint URL
- Required headers
- Request body parameters
- Response structure
- Token expiration details]

### Exchanging the instance identity token for an IAM token
{: #trusted-profiles-exchange-token}

[API DETAILS NEEDED: Provide exact API endpoint and parameters for exchanging instance identity token for IAM token, including:
- IAM token endpoint URL
- Required headers and content type
- Request parameters (grant_type, cr_token, profile_id)
- Response structure with access token details]

## Retrieving virtual machine metadata
{: #trusted-profiles-metadata}

You can use the instance identity token to retrieve metadata about your {{site.data.keyword.powerSys_notm}} virtual machine. This metadata includes information about the virtual machine's configuration, network settings, and associated trusted profiles.

[API DETAILS NEEDED: Provide exact metadata API endpoint and response structure, including:
- Metadata API endpoint URL
- Required authorization headers
- Complete response structure showing all available metadata fields
- Specific fields related to trusted profiles]

### Accessing metadata during cloud-init
{: #trusted-profiles-cloud-init}

You can retrieve virtual machine metadata during the cloud-init phase at first boot by including user-data scripts that query the metadata API. This allows you to configure your virtual machine based on its identity and associated trusted profiles.

[EXAMPLE NEEDED: Provide validated cloud-init user-data script example that works with PowerVS metadata service]

## Managing trusted profile assignments for virtual machines
{: #trusted-profiles-vm-management}

You can add, remove, or change the trusted profile ID associated with a specific {{site.data.keyword.powerSys_notm}} virtual machine at any time. This allows you to adjust access rights as your security requirements evolve.

### Adding a trusted profile to a virtual machine
{: #trusted-profiles-add-vm}

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for adding a trusted profile to a VM in the PowerVS console, including:
- Navigation path to virtual server instances
- VM configuration interface
- Trusted profile section location and appearance
- Dropdown or selection mechanism for choosing profiles
- Save/confirmation steps]

### Changing a virtual machine's trusted profile
{: #trusted-profiles-change-vm}

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for changing a VM's trusted profile, including:
- Navigation to the trusted profile edit interface
- Selection mechanism for choosing a different profile
- Confirmation steps]

### Removing a trusted profile from a virtual machine
{: #trusted-profiles-remove-vm}

[UI DETAILS NEEDED: Provide Figma screens and detailed UI flow for removing a trusted profile from a VM, including:
- Steps to access the removal interface
- Option to select "None" or remove the profile
- Confirmation steps]

## Viewing trusted profile information in metadata
{: #trusted-profiles-view-metadata}

The metadata API returns information about all trusted profiles that your {{site.data.keyword.powerSys_notm}} virtual machine is linked to. This information is useful for auditing and troubleshooting access issues.

[API DETAILS NEEDED: Provide exact API endpoint and response structure for retrieving trusted profile information from metadata, including:
- Metadata API endpoint URL for trusted profiles
- Required authorization headers
- Complete response structure with all available fields
- Example response with actual field names and data types]

## Next steps
{: #trusted-profiles-next-steps}

After you configure trusted profiles for your {{site.data.keyword.powerSys_notm}} virtual machines, you can:

* [Configure IAM access policies](/docs/account?topic=account-access-policies) to control service access
* [Create access groups](/docs/account?topic=account-groups) to manage access for multiple compute resources
* [Monitor IAM events](/docs/activity-tracker?topic=activity-tracker-at_events_iam) to track authentication and authorization activities
* Review the [IAM trusted profiles documentation](/docs/account?topic=account-create-trusted-profile) for advanced configuration options
