---

copyright:
  years: 2024
lastupdated: "2025-07-16"

---

{{site.data.keyword.attribute-definition-list}}

# IBM {{site.data.keyword.powerSys_notm}} CLI version 1.6.0 for {{site.data.keyword.on-prem}}
{: #power-iaas-cli-on-prem}

---

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}

----


The following list of commands are available with command-line interface (CLI) for IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.on-prem}}.


# `ibmcloud pi`
{: #ibmcloud-pi}

**Alias**: `pi`

**Description**: Manage IBM Cloud Power Virtual Server service.

**Usage**: `pi`

**Available Commands**:

- `datacenter`:    IBM Cloud Power Virtual Server Datacenters.
- `disaster-recovery`:    List disaster recovery locations for the current region or all regions.
- `image`:    IBM Cloud Power Virtual Server Images.
- `instance`:    IBM Cloud Power Virtual Server Instances.
- `job`:    IBM Cloud Power Virtual Server Jobs.
- `network-peer`:    IBM Cloud Power Virtual Server Network Peers.
- `placement-group`:    IBM Cloud Power Virtual Server Placement Groups.
- `shared-processor-pool`:    IBM Cloud Power Virtual Server Shared Processor Pools.
- `snapshot`:    [DEPRECATED] IBM Cloud Power Virtual Server Snapshots.
- `ssh-key`:    IBM Cloud Power Virtual Server SSH-Keys.
- `storage-pools`:    List all storage pools for the targeted region.
- `storage-tiers`:    List all storage tiers for the targeted region.
- `subnet`:    IBM Cloud Power Virtual Server Subnets.
- `virtual-serial-number`:    IBM Cloud Power Virtual Server Virtual Serial Number.
- `volume`:    IBM Cloud Power Virtual Server Volumes.
- `volume-group`:    IBM Cloud Power Virtual Server Volume Groups.
- `workspace`:    IBM Cloud Power Virtual Server Workspaces.

---

## `ibmcloud pi datacenter`
{: #ibmcloud-pi-datacenter}

**Alias**: `datacenter, dat`

**Description**: IBM Cloud Power Virtual Server Datacenters.

**Usage**: `datacenter`

**Available Commands**:

- `get`:    View details of a datacenter.
- `list`:    List all datacenter details.

---

### `ibmcloud pi datacenter get`
{: #ibmcloud-pi-datacenter-get}

**Alias**: `get`

**Description**: View details of a datacenter.

**Usage**:

```bash
get DATACENTER [--private=True|False]

  DATACENTER: The name of the datacenter.
```

**Available Flags**:

```bash
  -p, --private   Retrieve additional details about a private datacenter that you own.
                  Required if getting information from a private/on-prem datacenter.
```

---

### `ibmcloud pi datacenter list`
{: #ibmcloud-pi-datacenter-list}

**Alias**: `list, ls`

**Description**: List all datacenter details.

**Usage**: `list [--long=True|False] [--private=True|False]`

**Available Flags**:

```bash
  -l, --long      Retrieve additional details for datacenters.
  -p, --private   Retrieve additional details for private datacenters that you own.
```

---

## `ibmcloud pi disaster-recovery`
{: #ibmcloud-pi-disaster-recovery}

**Alias**: `disaster-recovery, drl`

**Description**: List disaster recovery locations for the current region or all regions.

**Usage**: `disaster-recovery [--all-regions=True|False]`

**Available Flags**:

```bash
  -a, --all-regions   List disaster recovery locations for all regions.
```

---

## `ibmcloud pi image`
{: #ibmcloud-pi-image}

**Alias**: `image, img`

**Description**: IBM Cloud Power Virtual Server Images.

**Usage**: `image`

**Available Commands**:

- `create`:    Create a copy of an available stock image into this account; stock image names cannot be changed.
- `delete`:    Delete an image.
- `export`:    Export an image to IBM Cloud Object Storage.
- `export-show`:    View details of the last image export job.
- `get`:    View details of an image.
- `import`:    Import an image to IBM Cloud Object Storage.
- `import-show`:    View details of the last image import job.
- `list`:    List all images in a workspace.
- `list-catalog`:    List images available in the regional image catalog.

---

### `ibmcloud pi image create`
{: #ibmcloud-pi-image-create}

**Alias**: `create, cr`

**Description**: Create a copy of an available stock image into this account; stock image names cannot be changed.

**Usage**:

```bash
create IMAGE_ID [--user-tags USER_TAG1[,USER_TAGn]]

  IMAGE_ID: The unique identifier or name of the image.
```

**Available Flags**:

```bash
  -u, --user-tags strings   Comma separated list of user tags to be attached to the created image.
```

**Examples**:

```bash
    ibmcloud pi image create 7100-05-05 --user-tags "project:customer-poc,env:dev,dataresidency:germany"
```

---

### `ibmcloud pi image delete`
{: #ibmcloud-pi-image-delete}

**Alias**: `delete, del`

**Description**: Delete an image.

**Usage**:

```bash
delete IMAGE_ID

  IMAGE_ID: The unique identifier or name of the image.
```

---

### `ibmcloud pi image export`
{: #ibmcloud-pi-image-export}

**Alias**: `export, ex`

**Description**: Export an image to IBM Cloud Object Storage.

**Usage**:

```bash
export IMAGE_ID --access-key KEY --bucket BUCKET_NAME --region REGION_NAME --secret-key KEY [--checksum=True|False]

  IMAGE_ID: The unique identifier or name of the image.
```

**Available Flags**:

```bash
  -a, --access-key string   Cloud Object Storage HMAC access key.
  -b, --bucket string       Cloud Object Storage bucket name.
  -c, --checksum            Creates a checksum file. Default is "false".
  -r, --region string       Cloud Object Storage region au-syd, br-sao, ca-tor, che01, eu-de, eu-es, eu-gb, jp-osa, jp-tok, us-east, us-south.
  -s, --secret-key string   Cloud Object Storage HMAC secret key.
```

**Examples**:

```bash
    ibmcloud pi image export 43064761-948f-469d-ac8e-b8e5f0d6056f --bucket "bucket/stock-images" --region us-east --access-key access-key-sample --secret-key secret-key-sample
```

---

### `ibmcloud pi image export-show`
{: #ibmcloud-pi-image-export-show}

**Alias**: `export-show, exs`

**Description**: View details of the last image export job.

**Usage**:

```bash
export-show IMAGE_ID

  IMAGE_ID: The unique identifier or name of the image.
```

---

### `ibmcloud pi image get`
{: #ibmcloud-pi-image-get}

**Alias**: `get`

**Description**: View details of an image.

**Usage**:

```bash
get IMAGE_ID

  IMAGE_ID: The unique identifier or name of the image.
```

---

### `ibmcloud pi image import`
{: #ibmcloud-pi-image-import}

**Alias**: `import, im`

**Description**: Import an image to IBM Cloud Object Storage.

**Usage**:

```bash
import IMAGE_NAME [--bucket-access private] [--storage-tier STORAGE_TIER] [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --access-key KEY --secret-key KEY --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME [--bucket-access private] [--storage-tier STORAGE_TIER] --storage-pool POOL [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False]  [--user-tags USER_TAG1[,USER_TAGn]] --access-key KEY --secret-key KEY --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME [--bucket-access private] [--storage-tier STORAGE_TIER] --affinity-policy affinity (--affinity-instance INSTANCE | --affinity-volume VOLUME) [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --access-key KEY --secret-key KEY --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME [--bucket-access private] [--storage-tier STORAGE_TIER] --affinity-policy anti-affinity (--anti-affinity-instances "INSTANCE1 [INSTANCEn]" | --anti-affinity-volumes "VOLUME1 [VOLUMEn]") [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --access-key KEY --secret-key KEY --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME --bucket-access public [--storage-tier STORAGE_TIER] [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME --bucket-access public [--storage-tier STORAGE_TIER] --storage-pool POOL [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME --bucket-access public [--storage-tier STORAGE_TIER] --affinity-policy affinity (--affinity-instance INSTANCE | --affinity-volume VOLUME) [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME
  pi image import IMAGE_NAME --bucket-access public [--storage-tier STORAGE_TIER] --affinity-policy anti-affinity (--anti-affinity-instances "INSTANCE1 [INSTANCEn]" | --anti-affinity-volumes "VOLUME1 [VOLUMEn]") [--os-type OSTYPE] [--import-details "LICENSE,PRODUCT,VENDOR"] [--checksum=True|False] [--user-tags USER_TAG1[,USER_TAGn]] --image-file-name IMAGE_FILE_NAME --bucket BUCKET_NAME --region REGION_NAME

  IMAGE_NAME: The desired name of the image.
```

**Available Flags**:

```bash
  -k, --access-key string                 Cloud Object Storage HMAC access key.
  -i, --affinity-instance string          PVM instance identifier or name to base volume affinity policy against;
                                          required if "--affinity-policy affinity" is specified and "--affinity-volume" is not provided.
  -a, --affinity-policy string            Affinity policy for data volume being created. Valid values are "affinity" and "anti-affinity".
                                          If "--storage-pool" is provided then this cannot be specified.
  -v, --affinity-volume string            Volume identifier or name to base volume affinity policy against;
                                          required if "--affinity-policy affinity" is specified and "--affinity-instance" is not provided.
  -j, --anti-affinity-instances strings   Comma separated list of instance identifiers or names to base volume anti-affinity policy against;
                                          required if "--affinity-policy anti-affinity" is specified and "--anti-affinity-volumes" is not provided.
  -w, --anti-affinity-volumes strings     Comma separated list of volume identifiers or names to base volume anti-affinity policy against;
                                          required if "--affinity-policy anti-affinity" is specified  and "--anti-affinity-instances" is not provided.
  -b, --bucket string                     Cloud Object Storage bucket name.
  -u, --bucket-access string              Indicates the bucket access type ("private" or "public"). Private access requires access and secret keys.
                                          Default is "private".
  -c, --checksum                          Checks the checksum file from the COS bucket against the one computed on the downloaded image.
  -n, --image-file-name string            The image file name.
  -d, --import-details strings            Import details for SAP image. Must include a license, product and vendor.
                                          Valid license values: byol.
                                          Valid product values: Hana, Netweaver.
                                          Valid vendor values: SAP.
  -o, --os-type string                    Operating system contained in the image (rhel, sles, aix, ibmi). Required when importing a raw image.
  -r, --region string                     Cloud Object Storage region au-syd, br-sao, ca-tor, che01, eu-de, eu-es, eu-gb, jp-osa, jp-tok, us-east, us-south.
  -s, --secret-key string                 Cloud Object Storage HMAC secret key.
  -p, --storage-pool string               Storage pool where the image will be imported to (use "ibmcloud pi storage-pools" to see available storage pools).
                                          If "--storage-pool" is provided then "--affinity-policy" cannot be specified.
  -t, --storage-tier string               Tier of the disk storage (use "ibmcloud pi storage-tiers" to see available tiers in the targeted region).
                                          Default to tier3 if not provided.
      --user-tags strings                 Comma separated list of user tags to be attached to the imported image.
```

**Examples**:

```bash
    ibmcloud pi image import import-image-name --bucket-access public --image-file-name imageFileName.ova --bucket test-bucket --region us-east
    ibmcloud pi image import import-image-name --bucket-access private --storage-tier tier1 --image-file-name imageFileName.ova --bucket test-bucket --region us-east --access-key access-key-sample --secret-key secret-key-sample
```

---

### `ibmcloud pi image import-show`
{: #ibmcloud-pi-image-import-show}

**Alias**: `import-show, ims`

**Description**: View details of the last image import job.

**Usage**: `import-show`

---

### `ibmcloud pi image list`
{: #ibmcloud-pi-image-list}

**Alias**: `list, ls`

**Description**: List all images in a workspace.

**Usage**: `list`

---

### `ibmcloud pi image list-catalog`
{: #ibmcloud-pi-image-list-catalog}

**Alias**: `list-catalog, lc`

**Description**: List images available in the regional image catalog.

**Usage**: `list-catalog [--sap=True|False]`

**Available Flags**:

```bash
  -s, --sap   Include SAP images.
```

**Examples**:

```bash
    ibmcloud pi image list-catalog --sap
```

---

## `ibmcloud pi instance`
{: #ibmcloud-pi-instance}

**Alias**: `instance, ins`

**Description**: IBM Cloud Power Virtual Server Instances.

**Usage**: `instance`

**Available Commands**:

- `action`:    Perform an operation in a PVM server instance.
- `capture`:    IBM Cloud Power Virtual Server Instance Capture.
- `console`:    IBM Cloud Power Virtual Server Instance Console.
- `create`:    Create a server instance.
- `delete`:    Delete a server instance.
- `get`:    View details of a server instance.
- `list`:    List all server instances.
- `operation`:    Perform an operation on an IBMi server instance.
- `snapshot`:    IBM Cloud Power Virtual Server Instance Snapshots.
- `subnet`:    IBM Cloud Power Virtual Server Instance Subnets.
- `update`:    Update a server instance.
- `virtual-serial-number`:    IBM Cloud Power Virtual Server Instance Virtual Serial Number.
- `volume`:    IBM Cloud Power Virtual Server Instance Volumes.

---

### `ibmcloud pi instance action`
{: #ibmcloud-pi-instance-action}

**Alias**: `action, act`

**Description**: Perform an operation in a PVM server instance.

**Usage**:

```bash
action INSTANCE_ID --operation OPERATION

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -o, --operation string   Operation to be done in a PVM server instance. Valid values are: hard-reboot, immediate-shutdown, soft-reboot, reset-state, start, stop.
```

**Examples**:

```bash
    ibmcloud pi instance action 43064761-948f-469d-ac8e-b8e5f0d6056f --operation immediate-shutdown
```

---

### `ibmcloud pi instance capture`
{: #ibmcloud-pi-instance-capture}

**Alias**: `capture, cap`

**Description**: IBM Cloud Power Virtual Server Instance Capture.

**Usage**: `capture`

**Available Commands**:

- `create`:    Create a capture of a server instance.
- `show`:    View the job details of the last server instance capture.

---

#### `ibmcloud pi instance capture create`
{: #ibmcloud-pi-instance-capture-create}

**Alias**: `create, cr`

**Description**: Create a capture of a server instance.

**Usage**:

```bash
create INSTANCE_ID --destination DEST --name NAME [--access-key KEY] [--checksum=True|False] [--image-path PATH] [--region REGION] [--secret-key KEY] [--user-tags USER_TAG1[,USER_TAGn]] [--volumes VOLUME1[,VOLUMEn]]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -a, --access-key string    Cloud Object Storage HMAC access key. Required if destination is cloud-storage.
  -c, --checksum             Creates a checksum file. Default is "false".
  -d, --destination string   Destination for the deployable image (image-catalog, cloud-storage, both).
  -i, --image-path string    Cloud Object Storage image path. Required if destination is cloud-storage. E.g. bucket-name[/optional/folder].
  -n, --name string          Name of the deployable image created for the captured instance.
  -r, --region string        Cloud Object Storage regions au-syd, br-sao, ca-tor, che01, eu-de, eu-es, eu-gb, jp-osa, jp-tok, us-east, us-south. Required if destination is cloud-storage.
  -s, --secret-key string    Cloud Object Storage HMAC secret key. Required if destination is cloud-storage.
  -u, --user-tags strings    Comma separated list of user tags to be attached to the instance capture.
  -v, --volumes strings      Comma separated list of volume identifiers or names to include in the captured instance.
```

**Examples**:

```bash
    ibmcloud pi instance capture create 43064761-948f-469d-ac8e-b8e5f0d6056f --destination both --name deployable-image-name --access-key access-key-sample --secret-key secret-key-sample --region us-south --image-path "imageBucket/imageLocation"
```

---

#### `ibmcloud pi instance capture show`
{: #ibmcloud-pi-instance-capture-show}

**Alias**: `show, sh`

**Description**: View the job details of the last server instance capture.

**Usage**:

```bash
show INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

### `ibmcloud pi instance console`
{: #ibmcloud-pi-instance-console}

**Alias**: `console, con`

**Description**: IBM Cloud Power Virtual Server Instance Console.

**Usage**: `console`

**Available Commands**:

- `get`:    Get the console of an instance.

---

#### `ibmcloud pi instance console get`
{: #ibmcloud-pi-instance-console-get}

**Alias**: `get`

**Description**: Get the console of an instance.

**Usage**:

```bash
get INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

### `ibmcloud pi instance create`
{: #ibmcloud-pi-instance-create}

**Alias**: `create, cr`

**Description**: Create a server instance.

**Usage**:

```bash
create INSTANCE_NAME --image IMAGE --subnets "SUBNET1 [IP1]"[,"SUBNETn [IPn]"]
    [--boot-volume-replication-enabled=True|False]
    [--IBMiCSS-license=True|False] [--IBMiPHA-license=True|False] [--IBMiRDS-users NUMBER-USERS]
    [--key-name NAME] [--memory MEMORY] [--pin-policy POLICY] [--placement-group GROUP_ID]
    [--processor-type PROC_TYPE] [--processors PROCESSORS] [--replicant-affinity-policy AFFINITY_POLICY]
    [--replicant-scheme SCHEME] [--replicants NUMBER] [--replication-sites SITE1[,SITEn]]
    [--shared-processor-pool SHARED_PROCESSOR_POOL] [--storage-affinity STORAGE_AFFINITY_POLICY]
    [--storage-affinity-instance INSTANCE] [--storage-affinity-volume VOLUME]
    [--storage-anti-affinity-instances INSTANCE1[,INSTANCEn]]
    [--storage-anti-affinity-volumes VOLUME1[,VOLUMEn]] [--storage-connection STORAGE_CONNECTION]
    [--storage-pool STORAGE_POOL] [--storage-pool-affinity] [--storage-tier STORAGE_TIER]
    [--sys-type TYPE] [--user-data USER_DATA] [--user-tags USER_TAG1[,USER_TAGn]]
    [--virtual-serial-number "(SERIAL | 'auto-assign')[,DESCRIPTION]" [--software-tier SOFTWARE-TIER]]
    [--virtual-cores ASSIGNED_CORES] [--volumes VOLUME1[,VOLUMEn]]

  INSTANCE_NAME: The name of the instance.
```

**Available Flags**:

```bash
      --IBMiCSS-license                           IBMi CSS software license associated with the instance.
      --IBMiPHA-license                           IBMi PHA software license associated with the instance.
      --IBMiRDS-users int                         Number of IBMi RDS users software license associated with the instance, default IBMiRDSUsers=0 (no license).
  -b, --boot-volume-replication-enabled           Enables storage replication on the boot volume. Default is "false".
  -i, --image string                              Operating system image identifier or name.
  -k, --key-name string                           Name of SSH key.
  -m, --memory float                              Amount of memory (in GB) to allocate to the instance. Default is 2GB.
      --pin-policy string                         Pin policy ("none", "soft", "hard"). Default is "none".
      --placement-group string                    The placement group ID of the group that the server will be added to.
  -r, --processor-type string                     Type of processors: "shared" or "dedicated" or "capped". Default is "dedicated".
  -p, --processors float                          Amount of processors to allocate to the instance. Default is 1 core.
      --replicant-affinity-policy string          Affinity policy to use when multicreate is used. Valid values are: affinity, anti-affinity, none.
      --replicant-scheme string                   Naming scheme to use for duplicate VMs. Valid values are: prefix, suffix.
      --replicants int                            The number of replicant instances to be created with this request.
                                                  Values greater than 1 will result in the creation of multiple instances.
      --replication-sites strings                 Indicates the replication sites of the boot volume. See "ibmcloud pi disaster-recovery" command to get a list of replication sites.
      --shared-processor-pool string              The shared processor pool ID of the pool that the server will be in.
      --software-tier string                      IBMi licensing software tiers. Must be set with "--virtual-serial-number" flag. Valid values are: P05, P10, P20, P30.
      --storage-affinity string                   Affinity policy for storage pool selection. Valid values are "affinity" and "anti-affinity".
                                                  If "--storage-pool" is provided, then this flag cannot be specified.
      --storage-affinity-instance string          PVM instance identifier or name to base storage affinity policy against;
                                                  required if "--storage-affinity affinity" is specified and "--storage-affinity-volume" is not provided.
      --storage-affinity-volume string            Volume identifier or name to base storage affinity policy against;
                                                  required if "--storage-affinity affinity" is specified and "--storage-affinity-instance" is not provided.
      --storage-anti-affinity-instances strings   Comma separated list of PVM instance identifiers or names to base storage affinity policy against;
                                                  required if "--storage-affinity anti-affinity" is specified and "--storage-anti-affinity-volumes" is not provided.
      --storage-anti-affinity-volumes strings     Comma separated list of volume identifiers or names to base storage affinity policy against;
                                                  required if "--storage-affinity anti-affinity" is specified and "--storage-anti-affinity-instances" is not provided.
      --storage-connection string                 The storage connection type. Valid values are: vSCSI, maxVolumeSupport.
      --storage-pool string                       Storage pool for server deployment (use "ibmcloud pi storage-pools" to see available storage pools).
                                                  Only valid when you deploy one of the IBM supplied stock images.
                                                  Storage tier and pool for a custom image (an imported image or an image that is created from a PVMInstance capture)
                                                  defaults to the storage tier and pool the image was created in.
      --storage-pool-affinity                     Indicates if all volumes attached to the server must reside in the same storage pool.
                                                  If set to false, then volumes from any storage tier and pool can be attached to the PVM instance;
                                                  This impacts PVM instance snapshot, capture, and clone. For capture and clone only data volumes that are of
                                                  the same storage tier and in the same storage pool of the PVM instance's boot volume can be included.
                                                  For snapshot all data volumes to be included in the snapshot must reside in the same storage tier and pool.
                                                  Once set to false, cannot be set back to true unless all volumes attached reside in the same storage tier and pool.
  -t, --storage-tier string                       Storage tier for server deployment when deploying a stock or custom image
                                                  (use "ibmcloud pi storage-tiers" to see available storage tiers in the targeted region).
                                                  Default to tier3 if not provided.
  -n, --subnets strings                           Comma separated list of subnet identifiers or names and optional IP address to associate with the instance.
  -s, --sys-type string                           Name of System Type ('s1022', 's1122', 'e1050', 'e1080', 'e1150', 'e1180')
  -u, --user-data string                          The user data passed into the instance. Strings and file names are supported. File names must be prepended with "@".
      --user-tags strings                         Comma separated list of user tags to be attached to the instance.
      --virtual-cores int                         The number of virtual cores assigned.
      --virtual-serial-number string              IBMi virtual serial number information added with the instance.
                                                  Must include an existing virtual serial number or 'auto-assign' and optionally a description.
  -v, --volumes strings                           Comma separated list of volume identifiers or names to associate with the instance.
```

**Examples**:

```bash
    ibmcloud pi instance create test-instance --image 43064761-948f-469d-ac8e-b8e5f0d6056f --subnets 85716e61-948f-309d-de8b-c4e5f0d3126d
    ibmcloud pi instance create test-instance --image 43064761-948f-469d-ac8e-b8e5f0d6056f --subnets 85716e61-948f-309d-de8b-c4e5f0d3126d --volumes 43064761-948f-469d-ac8e-b8e5f0d6056f --storage-tier tier1 --processors 1 --processor-type dedicated --deployment-type EPIC --sys-type e980
    ibmcloud pi instance create test-instance --image 43064761-948f-469d-ac8e-b8e5f0d6056f --subnets 85716e61-948f-309d-de8b-c4e5f0d3126d --storage-tier tier1 --replicants 2 --replicant-scheme prefix --replicant-affinity-policy affinity
    ibmcloud pi instance create test-instance --image 43064761-948f-469d-ac8e-b8e5f0d6056f --subnets 85716e61-948f-309d-de8b-c4e5f0d3126d --boot-volume-replication-enabled --replication-sites dal10
```

---

### `ibmcloud pi instance delete`
{: #ibmcloud-pi-instance-delete}

**Alias**: `delete, del`

**Description**: Delete a server instance.

**Usage**:

```bash
delete INSTANCE_ID [--delete-data-volumes=True|False] [--retainVSN=True|False]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -d, --delete-data-volumes   Indicates whether all data volumes attached to the instance must be deleted.
                              Shared data volumes will be deleted if no other instances are attached.
  -r, --retainVSN             Determines if the virtual serial number will be retained after being removed from the instance. Default is "false".
```

---

### `ibmcloud pi instance get`
{: #ibmcloud-pi-instance-get}

**Alias**: `get`

**Description**: View details of a server instance.

**Usage**:

```bash
get INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

### `ibmcloud pi instance list`
{: #ibmcloud-pi-instance-list}

**Alias**: `list, ls`

**Description**: List all server instances.

**Usage**: `list`

---

### `ibmcloud pi instance operation`
{: #ibmcloud-pi-instance-operation}

**Alias**: `operation, op`

**Description**: Perform an operation on an IBMi server instance.

**Usage**:

```bash
operation INSTANCE_ID --operation-type TYPE [--boot-mode MODE] [--boot-operating-mode MODE] [--job-task TASK]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -b, --boot-mode string             Name of the server boot mode. Valid values are: a, b, c, d.
  -m, --boot-operating-mode string   Name of the server operating mode. Valid values are: manual, normal.
  -j, --job-task string              Name of the job task to execute. Valid values are: consoleservice, dston, dumprestart, iopdump, iopreset, remotedstoff, remotedston, retrydump.
  -o, --operation-type string        Name of the operation to execute. Valid values are: boot, job.
```

**Examples**:

```bash
    ibmcloud pi instance operation 43064761-948f-469d-ac8e-b8e5f0d6056f --operation-type boot --boot-mode c --boot-operating-mode normal
```

---

### `ibmcloud pi instance snapshot`
{: #ibmcloud-pi-instance-snapshot}

**Alias**: `snapshot, snap`

**Description**: IBM Cloud Power Virtual Server Instance Snapshots.

**Usage**: `snapshot`

**Available Commands**:

- `create`:    Create a snapshot for an instance.
- `delete`:    Delete a snapshot from an instance.
- `get`:    Get a snapshot for an instance
- `list`:    List all snapshots for an instance or all snapshots in the workspace.
- `restore`:    Restore a snapshot for an instance.
- `update`:    Update a snapshot for an instance.

---

#### `ibmcloud pi instance snapshot create`
{: #ibmcloud-pi-instance-snapshot-create}

**Alias**: `create, cr`

**Description**: Create a snapshot for an instance.

**Usage**:

```bash
create INSTANCE_ID --name SNAPSHOT_NAME [--description DESCRIPTION] [--user-tags USER_TAG1[,USER_TAGn]] [--volumes VOLUME1[,VOLUMEn]]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -d, --description string   Snapshot description.
  -n, --name string          Name of the snapshot.
  -u, --user-tags strings    Comma separated list of user tags to be attached to the snapshot.
  -v, --volumes strings      Comma separated list of volume identifiers or names to include in the snapshot.
                             If you do not specify this parameter or if the volumes list is empty,
                             all the volumes that are attached to the instance are included in the snapshot.
```

**Examples**:

```bash
    ibmcloud pi instance snapshot create 85716e61-948f-309d-de8b-c4e5f0d3126d --name test-snapshot-name
```


---

#### `ibmcloud pi instance snapshot delete`
{: #ibmcloud-pi-instance-snapshot-delete}

**Alias**: `delete, del`

**Description**: Delete a snapshot from an instance.

**Usage**:

```bash
delete SNAPSHOT_ID

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

---

#### `ibmcloud pi instance snapshot get`
{: #ibmcloud-pi-instance-snapshot-get}

**Alias**: `get`

**Description**: Get a snapshot for an instance

**Usage**:

```bash
get SNAPSHOT_ID

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

---

#### `ibmcloud pi instance snapshot list`
{: #ibmcloud-pi-instance-snapshot-list}

**Alias**: `list, ls`

**Description**: List all snapshots for an instance or all snapshots in the workspace.

**Usage**:

```bash
list [INSTANCE_ID]

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

#### `ibmcloud pi instance snapshot restore`
{: #ibmcloud-pi-instance-snapshot-restore}

**Alias**: `restore, res`

**Description**: Restore a snapshot for an instance.

**Usage**:

```bash
restore INSTANCE_ID --snapshot SNAPSHOT_ID [--force] [--restore VALUE]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -f, --force             By default the VM must be shutoff during a snapshot restore, force set to true will relax the VM shutoff pre-condition.
  -r, --restore string    Action to take on a failed snapshot restore. Valid values for "--restore" are: retry, rollback.
  -s, --snapshot string   The unique identifier of the snapshot.
```

**Examples**:

```bash
    ibmcloud pi instance snapshot restore 85716e61-948f-309d-de8b-c4e5f0d3126d --snapshot 43064761-948f-469d-ac8e-b8e5f0d6056f --force --restore retry
```

---

#### `ibmcloud pi instance snapshot update`
{: #ibmcloud-pi-instance-snapshot-update}

**Alias**: `update, upd`

**Description**: Update a snapshot for an instance.

**Usage**:

```bash
update SNAPSHOT_ID [--description DESCRIPTION] [--name NAME]

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

**Available Flags**:

```bash
  -d, --description string   New snapshot description.
  -n, --name string          New name of the snapshot.
```

---

### `ibmcloud pi instance subnet`
{: #ibmcloud-pi-instance-subnet}

**Alias**: `subnet, snet`

**Description**: IBM Cloud Power Virtual Server Instance Subnets.

**Usage**: `subnet`

**Available Commands**:

- `attach`:    Attach a subnet to a server instance.
- `detach`:    Detach a specific subnet or mac address from a server instance.
- `list`:    List all the attached subnets.

---

#### `ibmcloud pi instance subnet attach`
{: #ibmcloud-pi-instance-subnet-attach}

**Alias**: `attach, att`

**Description**: Attach a subnet to a server instance.

**Usage**:

```bash
attach INSTANCE_ID --subnet SUBNET_ID [--ip-address IP_ADDRESS]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -i, --ip-address string   The requested ip address of this subnet interface (192.168.1.0).
  -n, --subnet string       The subnet ID.
```

**Examples**:

```bash
    ibmcloud pi instance subnet attach 85716e61-948f-309d-de8b-c4e5f0d3126d --subnet 43064761-948f-469d-ac8e-b8e5f0d6056f --ip-address 192.168.0.12
```

---

#### `ibmcloud pi instance subnet detach`
{: #ibmcloud-pi-instance-subnet-detach}

**Alias**: `detach, det`

**Description**: Detach a specific subnet or mac address from a server instance.

**Usage**:

```bash
detach INSTANCE_ID --subnet SUBNET_ID [--mac-address MAC_ADDRESS]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -m, --mac-address string   The mac address of the subnet interface to be removed. Default is all mac addresses.
  -n, --subnet string        The subnet ID.
```

**Examples**:

```bash
    ibmcloud pi instance subnet detach 85716e61-948f-309d-de8b-c4e5f0d3126d --subnet 43064761-948f-469d-ac8e-b8e5f0d6056f --mac-address eb:26:8f:ba:5f:62
```

---

#### `ibmcloud pi instance subnet list`
{: #ibmcloud-pi-instance-subnet-list}

**Alias**: `list, ls`

**Description**: List all the attached subnets.

**Usage**:

```bash
list INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

### `ibmcloud pi instance update`
{: #ibmcloud-pi-instance-update}

**Alias**: `update, upd`

**Description**: Update a server instance.

**Usage**:

```bash
update INSTANCE_ID [--IBMiCSS-license=True|False]  [--IBMiPHA-license=True|False]
    [--IBMiRDS-users NUMBER-USERS] [--memory AMOUNT] [--name NAME] [--pin-policy POLICY]
    [--processor-type TYPE] [--processors NUMBER] [--storage-pool-affinity=True|False]
    [--virtual-cores ASSIGNED_CORES] [--virtual-optional-device ("attach" | "detach")]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
      --IBMiCSS-license                 New IBMi CSS software license associated with the instance.
      --IBMiPHA-license                 New IBMi PHA software license associated with the instance.
      --IBMiRDS-users int               New number of IBMi RDS users software license associated with the instance.
  -m, --memory float                    New amount of memory for the server instance.
  -n, --name string                     New name of the server instance.
      --pin-policy string               New pin policy for the server instance ("none", "soft", "hard").
  -r, --processor-type string           New processor type for the server instance.
  -p, --processors float                New amount of processors for the server instance.
  -s, --storage-pool-affinity           Indicates if all volumes attached to the server must reside in the same storage pool.
                                        If set to false, then volumes from any storage tier and pool can be attached to the PVM instance;
                                        This impacts PVM instance snapshot, capture, and clone. For capture and clone only data volumes that are of
                                        the same storage tier and in the same storage pool of the PVM instance's boot volume can be included.
                                        For snapshot all data volumes to be included in the snapshot must reside in the same storage tier and pool.
                                        Once set to false, cannot be set back to true unless all volumes attached reside in the same storage tier and pool.
      --virtual-cores int               New number of virtual cores assigned.
  -v, --virtual-optical-device string   Attach or detach a virtual optical device to this instance. Valid values are: attach, detach.
```

**Examples**:

```bash
    ibmcloud pi instance update 43064761-948f-469d-ac8e-b8e5f0d6056f --memory 2 --name new-instance-name --pin-policy hard --processors 2 --processor-type shared --storage-pool-affinity
```

---

### `ibmcloud pi instance virtual-serial-number`
{: #ibmcloud-pi-instance-virtual-serial-number}

**Alias**: `virtual-serial-number, vsn`

**Description**: IBM Cloud Power Virtual Server Instance Virtual Serial Number.

**Usage**: `virtual-serial-number`

**Available Commands**:

- `assign`:    Assign a virtual serial number to a virtual server instance.
- `get`:    Get a virtual serial number assigned to a virtual server instance.
- `unassign`:    Unassign a virtual serial number from a virtual server instance.
- `update`:    Update a virtual serial number assigned to a virtual server instance.

---

#### `ibmcloud pi instance virtual-serial-number assign`
{: #ibmcloud-pi-instance-virtual-serial-number-assign}

**Alias**: `assign, asn`

**Description**: Assign a virtual serial number to a virtual server instance.

**Usage**:

```bash
assign INSTANCE_ID [--description DESCRIPTION] [--serial SERIAL]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -d, --description string   Description for the virtual serial number.
  -s, --serial string        Virtual serial number to attach. If no serial is specified or 'auto-assign' is set, a virtual serial number will be automatically generated.
```

**Examples**:

```bash
    ibmcloud pi instance virtual-serial-number assign 43064761-948f-469d-ac8e-b8e5f0d6056f --description "new-virtual-serial-number-description"
```

---

#### `ibmcloud pi instance virtual-serial-number get`
{: #ibmcloud-pi-instance-virtual-serial-number-get}

**Alias**: `get`

**Description**: Get a virtual serial number assigned to a virtual server instance.

**Usage**:

```bash
get INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

#### `ibmcloud pi instance virtual-serial-number unassign`
{: #ibmcloud-pi-instance-virtual-serial-number-unassign}

**Alias**: `unassign, uasn`

**Description**: Unassign a virtual serial number from a virtual server instance.

**Usage**:

```bash
unassign INSTANCE_ID [--retainVSN=True|False]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -r, --retainVSN   Determines if virtual serial number will be retained after being unassigned from the instance. Default is "false".
```

**Examples**:

```bash
    ibmcloud pi instance virtual-serial-number unassign 43064761-948f-469d-ac8e-b8e5f0d6056f --retainVSN
```

---

#### `ibmcloud pi instance virtual-serial-number update`
{: #ibmcloud-pi-instance-virtual-serial-number-update}

**Alias**: `update, upd`

**Description**: Update a virtual serial number assigned to a virtual server instance.

**Usage**:

```bash
update INSTANCE_ID (--description DESCRIPTION | --software-tier SOFTWARE-TIER)

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -d, --description string     New virtual serial number description.
      --software-tier string   IBMi licensing software tiers. Valid values are: P05, P10, P20, P30.
```

---

### `ibmcloud pi instance volume`
{: #ibmcloud-pi-instance-volume}

**Alias**: `volume, vol`

**Description**: IBM Cloud Power Virtual Server Instance Volumes.

**Usage**: `volume`

**Available Commands**:

- `attach`:    Attach one or more volumes to an instance.
- `bulk-detach`:    Detach multiple volumes from an instance.
- `detach`:    Detach a volume from an instance.
- `list`:    List all the attached volumes.

---

#### `ibmcloud pi instance volume attach`
{: #ibmcloud-pi-instance-volume-attach}

**Alias**: `attach, att`

**Description**: Attach one or more volumes to an instance.

**Usage**:

```bash
attach INSTANCE_ID --volumes VOLUME1[,VOLUMEn] [--boot-volume BOOT_VOLUME]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -b, --boot-volume string   Boot volume to be attached to an instance.
  -v, --volumes strings      Comma separated list of volume identifiers or names to associate with the instance.
```

**Examples**:

```bash
    ibmcloud pi instance volume attach 85716e61-948f-309d-de8b-c4e5f0d3126d --boot-volume e5d394ef-3156-21a3-8b12-de15c6d5e276 --volumes 43064761-948f-469d-ac8e-b8e5f0d6056f,32064761-298e-469a-bc6f-d8e5f0d6067a
```

---

#### `ibmcloud pi instance volume bulk-detach`
{: #ibmcloud-pi-instance-volume-bulk-detach}

**Alias**: `bulk-detach, bdet`

**Description**: Detach multiple volumes from an instance.

**Usage**:

```bash
bulk-detach INSTANCE_ID (--detach-all=True|False | --volumes VOLUME1[,VOLUMEn]) [--detach-primary=True|False]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -a, --detach-all        Indicates if all volumes, except primary boot volume, attached to the instance should be detached. Required if "--volumes" is not provided.
  -p, --detach-primary    Indicates if primary boot volume attached to the instance should be detached.
  -v, --volumes strings   List of volumes to be detached from an instance. Required if "--detach-all" is not provided.
```

**Examples**:

```bash
    ibmcloud pi instance volume bulk-detach 85716e61-948f-309d-de8b-c4e5f0d3126d --detach-all --detach-primary
```

---

#### `ibmcloud pi instance volume detach`
{: #ibmcloud-pi-instance-volume-detach}

**Alias**: `detach, det`

**Description**: Detach a volume from an instance.

**Usage**:

```bash
detach INSTANCE_ID --volume VOLUME_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -v, --volume string   Volume to detach from the instance.
```

**Examples**:

```bash
    ibmcloud pi instance volume detach 85716e61-948f-309d-de8b-c4e5f0d3126d --volume 43064761-948f-469d-ac8e-b8e5f0d6056f
```

---

#### `ibmcloud pi instance volume list`
{: #ibmcloud-pi-instance-volume-list}

**Alias**: `list, ls`

**Description**: List all the attached volumes.

**Usage**:

```bash
list INSTANCE_ID

  INSTANCE_ID: The unique identifier or name of the instance.
```

---

## `ibmcloud pi job`
{: #ibmcloud-pi-job}

**Alias**: `job`

**Description**: IBM Cloud Power Virtual Server Jobs.

**Usage**: `job`

**Available Commands**:

- `delete`:    Delete a job.
- `get`:    View details of a job.
- `list`:    List up to the last 5 jobs in a workspace.

---

### `ibmcloud pi job delete`
{: #ibmcloud-pi-job-delete}

**Alias**: `delete, del`

**Description**: Delete a job.

**Usage**:

```bash
delete JOB_ID

  JOB_ID: The unique identifier of the job.
```

---

### `ibmcloud pi job get`
{: #ibmcloud-pi-job-get}

**Alias**: `get`

**Description**: View details of a job.

**Usage**:

```bash
get JOB_ID

  JOB_ID: The unique identifier of the job.
```

---

### `ibmcloud pi job list`
{: #ibmcloud-pi-job-list}

**Alias**: `list, ls`

**Description**: List up to the last 5 jobs in a workspace.

**Usage**: `list [--operation-action ACTION] [--operation-id ID] [--operation-target TARGET]`

**Available Flags**:

```bash
  -a, --operation-action string   Operation action to filter returned jobs. Valid values are: imageExport, imageImport, storage, vmCapture.
  -i, --operation-id string       Operation ID to filter returned jobs.
  -t, --operation-target string   Operation target to filter returned jobs. Valid values are: cloudConnection, image, pvmInstance.
```

---

## `ibmcloud pi network-peer`
{: #ibmcloud-pi-network-peer}

**Alias**: `network-peer, np`

**Description**: IBM Cloud Power Virtual Server Network Peers.

**Usage**: `network-peer`

**Available Commands**:

- `list`:    List all network peers.

---

### `ibmcloud pi network-peer list`
{: #ibmcloud-pi-network-peer-list}

**Alias**: `list, ls`

**Description**: List all network peers.

**Usage**: `list`

---

## `ibmcloud pi placement-group`
{: #ibmcloud-pi-placement-group}

**Alias**: `placement-group, pg`

**Description**: IBM Cloud Power Virtual Server Placement Groups.

**Usage**: `placement-group`

**Available Commands**:

- `create`:    Create a server placement group.
- `delete`:    Delete a server placement group.
- `get`:    View details of a server placement group.
- `list`:    List all server placement groups.
- `server-add`:    Add a server to a server placement group.
- `server-remove`:    Remove a server from a server placement group.

---

### `ibmcloud pi placement-group create`
{: #ibmcloud-pi-placement-group-create}

**Alias**: `create, cr`

**Description**: Create a server placement group.

**Usage**:

```bash
create PLACEMENT_GROUP_NAME --policy POLICY [--user-tags USER_TAG1[,USER_TAGn]]

  PLACEMENT_GROUP_NAME: A unique name of the placement group.
```

**Available Flags**:

```bash
  -p, --policy string       Affinity policy for placement group being created. Valid values are affinity and anti-affinity.
  -u, --user-tags strings   Comma separated list of user tags to be attached to the placement group.
```

**Examples**:

```bash
    ibmcloud pi placement-group test-placement-group --policy anti-affinity
```

---

### `ibmcloud pi placement-group delete`
{: #ibmcloud-pi-placement-group-delete}

**Alias**: `delete, del`

**Description**: Delete a server placement group.

**Usage**:

```bash
delete PLACEMENT_GROUP_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

---

### `ibmcloud pi placement-group get`
{: #ibmcloud-pi-placement-group-get}

**Alias**: `get`

**Description**: View details of a server placement group.

**Usage**:

```bash
get PLACEMENT_GROUP_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

---

### `ibmcloud pi placement-group list`
{: #ibmcloud-pi-placement-group-list}

**Alias**: `list, ls`

**Description**: List all server placement groups.

**Usage**: `list`

---

### `ibmcloud pi placement-group server-add`
{: #ibmcloud-pi-placement-group-server-add}

**Alias**: `server-add, sa`

**Description**: Add a server to a server placement group.

**Usage**:

```bash
server-add PLACEMENT_GROUP_ID --server INSTANCE_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

**Available Flags**:

```bash
  -s, --server string   The server instance ID of the server to add to the placement group.
```

**Examples**:

```bash
    ibmcloud pi placement-group server-add 43064761-948f-469d-ac8e-b8e5f0d6056f --server 85716e61-948f-309d-de8b-c4e5f0d3126d
```

---

### `ibmcloud pi placement-group server-remove`
{: #ibmcloud-pi-placement-group-server-remove}

**Alias**: `server-remove, sr`

**Description**: Remove a server from a server placement group.

**Usage**:

```bash
server-remove PLACEMENT_GROUP_ID --server INSTANCE_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

**Available Flags**:

```bash
  -s, --server string   The server instance ID of the server to add to the placement group.
```

**Examples**:

```bash
    ibmcloud pi placement-group server-remove 43064761-948f-469d-ac8e-b8e5f0d6056f --server 85716e61-948f-309d-de8b-c4e5f0d3126d
```

---

## `ibmcloud pi shared-processor-pool`
{: #ibmcloud-pi-shared-processor-pool}

**Alias**: `shared-processor-pool, spp`

**Description**: IBM Cloud Power Virtual Server Shared Processor Pools.

**Usage**: `shared-processor-pool`

**Available Commands**:

- `create`:    Create a shared processor pool.
- `delete`:    Delete a shared processor pool.
- `get`:    View details of a shared processor pool.
- `list`:    List all shared processor pools.
- `placement-group`:    IBM Cloud Power Virtual Server Placement Groups.
- `update`:    Update a shared processor pool.

---

### `ibmcloud pi shared-processor-pool create`
{: #ibmcloud-pi-shared-processor-pool-create}

**Alias**: `create, cr`

**Description**: Create a shared processor pool.

**Usage**:

```bash
create SHARED_PROCESSOR_POOL_NAME --host-group HOST_GROUP --reserved-cores NUMBER_OF_CORES [--placement-group-id PLACEMENT_GROUP_ID] [--user-tags USER_TAG1[,USER_TAGn]]

  SHARED_PROCESSOR_POOL_NAME: A unique name of the shared processor pool. A minimum of 2 characters and a maximum of 12 are allowed. The only special character allowed is the underscore '_'.
```

**Available Flags**:

```bash
  -g, --host-group string           The host group where the host will be chosen.
  -p, --placement-group-id string   The identifier of the shared processor pool placement group the pool will be added to.
  -r, --reserved-cores int          The integer amount of reserved processor cores for the shared processor pool.
  -u, --user-tags strings           Comma separated list of user tags to be attached to the placement-group.
```

**Examples**:

```bash
    ibmcloud pi shared-processor-pool create test-shared-processor-pool --host-group e980 --reserver-cores 2 --placement-group-id 43064761-948f-469d-ac8e-b8e5f0d6056f
```

---

### `ibmcloud pi shared-processor-pool delete`
{: #ibmcloud-pi-shared-processor-pool-delete}

**Alias**: `delete, del`

**Description**: Delete a shared processor pool.

**Usage**:

```bash
delete SHARED_PROCESSOR_POOL_ID

  SHARED_PROCESSOR_POOL_ID: The unique identifier or name of the shared processor pool.
```

---

### `ibmcloud pi shared-processor-pool get`
{: #ibmcloud-pi-shared-processor-pool-get}

**Alias**: `get`

**Description**: View details of a shared processor pool.

**Usage**:

```bash
get SHARED_PROCESSOR_POOL_ID

  SHARED_PROCESSOR_POOL_ID: The unique identifier or name of the shared processor pool.
```

---

### `ibmcloud pi shared-processor-pool list`
{: #ibmcloud-pi-shared-processor-pool-list}

**Alias**: `list, ls`

**Description**: List all shared processor pools.

**Usage**: `list`

---

### `ibmcloud pi shared-processor-pool placement-group`
{: #ibmcloud-pi-shared-processor-pool-placement-group}

**Alias**: `placement-group, pg`

**Description**: IBM Cloud Power Virtual Server Placement Groups.

**Usage**: `placement-group`

**Available Commands**:

- `create`:    Create a shared processor pool placement group.
- `delete`:    Delete a shared processor pool placement group.
- `get`:    View details of a shared processor pool placement group.
- `list`:    List all shared processor pool placement groups.
- `member-add`:    Add a shared processor pool to a placement group.
- `member-remove`:    Remove a shared processor pool from a placement group.

---

#### `ibmcloud pi shared-processor-pool placement-group create`
{: #ibmcloud-pi-shared-processor-pool-placement-group-create}

**Alias**: `create, cr`

**Description**: Create a shared processor pool placement group.

**Usage**:

```bash
create PLACEMENT_GROUP_NAME --policy POLICY [--user-tags USER_TAG1[,USER_TAGn]]

  PLACEMENT_GROUP_NAME: A unique name of the placement group.
```

**Available Flags**:

```bash
  -p, --policy string       Affinity policy for placement group being created. Valid values are affinity and anti-affinity.
  -u, --user-tags strings   Comma separated list of user tags to be attached to the shared processor pool placement group.
```

**Examples**:

```bash
    ibmcloud pi shared-processor-pool placement-group create spp-pg-test --policy affinity
```

---

#### `ibmcloud pi shared-processor-pool placement-group delete`
{: #ibmcloud-pi-shared-processor-pool-placement-group-delete}

**Alias**: `delete, del`

**Description**: Delete a shared processor pool placement group.

**Usage**:

```bash
delete PLACEMENT_GROUP_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

---

#### `ibmcloud pi shared-processor-pool placement-group get`
{: #ibmcloud-pi-shared-processor-pool-placement-group-get}

**Alias**: `get`

**Description**: View details of a shared processor pool placement group.

**Usage**:

```bash
get PLACEMENT_GROUP_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

---

#### `ibmcloud pi shared-processor-pool placement-group list`
{: #ibmcloud-pi-shared-processor-pool-placement-group-list}

**Alias**: `list, ls`

**Description**: List all shared processor pool placement groups.

**Usage**: `list`

---

#### `ibmcloud pi shared-processor-pool placement-group member-add`
{: #ibmcloud-pi-shared-processor-pool-placement-group-member-add}

**Alias**: `member-add, ma`

**Description**: Add a shared processor pool to a placement group.

**Usage**:

```bash
member-add PLACEMENT_GROUP_ID --shared-processor-pool POOL_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

**Available Flags**:

```bash
  -s, --shared-processor-pool string   The shared processor pool ID of the pool to add to the placement group.
```

**Examples**:

```bash
    ibmcloud pi shared-processor-pool placement-group member-add 43064761-948f-469d-ac8e-b8e5f0d6056 --shared-processor-pool 32bec9b0-560a-4baa-8cc0-7c68e41e5843
```

---

#### `ibmcloud pi shared-processor-pool placement-group member-remove`
{: #ibmcloud-pi-shared-processor-pool-placement-group-member-remove}

**Alias**: `member-remove, mr`

**Description**: Remove a shared processor pool from a placement group.

**Usage**:

```bash
member-remove PLACEMENT_GROUP_ID --shared-processor-pool POOL_ID

  PLACEMENT_GROUP_ID: The unique identifier of the placement group.
```

**Available Flags**:

```bash
  -s, --shared-processor-pool string   The shared processor pool ID of the pool to remove from the placement group.
```

**Examples**:

```bash
    ibmcloud pi shared-processor-pool placement-group member-remove 43064761-948f-469d-ac8e-b8e5f0d6056 --shared-processor-pool 32bec9b0-560a-4baa-8cc0-7c68e41e5843
```

---

### `ibmcloud pi shared-processor-pool update`
{: #ibmcloud-pi-shared-processor-pool-update}

**Alias**: `update, upd`

**Description**: Update a shared processor pool.

**Usage**:

```bash
update SHARED_PROCESSOR_POOL_ID [--name SHARED_PROCESSOR_POOL_NAME] [--reserved-cores NUMBER_OF_CORES]

  SHARED_PROCESSOR_POOL_ID: The unique identifier or name of the shared processor pool.
```

**Available Flags**:

```bash
  -n, --name string          New name of the shared processor pool. A minimum of 2 characters and a maximum of 12 are allowed. The only special character allowed is the underscore '_'.
  -r, --reserved-cores int   The integer amount of reserved processor cores for the shared processor pool.
```

---

## `ibmcloud pi snapshot`
{: #ibmcloud-pi-snapshot}

**Alias**: `snapshot, snap`

**Description**: [DEPRECATED] IBM Cloud Power Virtual Server Snapshots.

**Usage**: `snapshot`

**Available Commands**:

- `create`:    [DEPRECATED] Create a snapshot.
- `delete`:    [DEPRECATED] Delete a snapshot.
- `get`:    [DEPRECATED] View details of a snapshot.
- `list`:    [DEPRECATED] List all snapshots.
- `restore`:    [DEPRECATED] Restore a snapshot.
- `update`:    [DEPRECATED] Update a snapshot.

---

### `ibmcloud pi snapshot create`
{: #ibmcloud-pi-snapshot-create}

**Alias**: `create, cr`

**Description**: [DEPRECATED] Create a snapshot.

**Usage**:

```bash
create INSTANCE_ID --name SNAPSHOT_NAME [--description DESCRIPTION] [--user-tags USER_TAG1[,USER_TAGn]] [--volumes VOLUME1[,VOLUMEn]]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -d, --description string   Snapshot description.
  -n, --name string          Name of the snapshot.
  -u, --user-tags strings    Comma separated list of user tags to be attached to the snapshot.
  -v, --volumes strings      Comma separated list of volume identifiers or names to include in the snapshot.
                             If you do not specify this parameter or if the volumes list is empty,
                             all the volumes that are attached to the instance are included in the snapshot.
```

**Examples**:

```bash
    ibmcloud pi snapshot create 85716e61-948f-309d-de8b-c4e5f0d3126d --name test-snapshot-name
```

---

### `ibmcloud pi snapshot delete`
{: #ibmcloud-pi-snapshot-delete}

**Alias**: `delete, del`

**Description**: [DEPRECATED] Delete a snapshot.

**Usage**:

```bash
delete SNAPSHOT_ID

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

---

### `ibmcloud pi snapshot get`
{: #ibmcloud-pi-snapshot-get}

**Alias**: `get`

**Description**: [DEPRECATED] View details of a snapshot.

**Usage**:

```bash
get SNAPSHOT_ID

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

---

### `ibmcloud pi snapshot list`
{: #ibmcloud-pi-snapshot-list}

**Alias**: `list, ls`

**Description**: [DEPRECATED] List all snapshots.

**Usage**: `list`

---

### `ibmcloud pi snapshot restore`
{: #ibmcloud-pi-snapshot-restore}

**Alias**: `restore, res`

**Description**: [DEPRECATED] Restore a snapshot.

**Usage**:

```bash
restore INSTANCE_ID --snapshot SNAPSHOT_ID [--force] [--restore VALUE]

  INSTANCE_ID: The unique identifier or name of the instance.
```

**Available Flags**:

```bash
  -f, --force             By default the VM must be shutoff during a snapshot restore, force set to true will relax the VM shutoff pre-condition.
  -r, --restore string    Action to take on a failed snapshot restore - allowable values: ["retry","rollback"].
  -s, --snapshot string   The unique identifier of the snapshot.
```

**Examples**:

```bash
    ibmcloud pi snapshot restore 85716e61-948f-309d-de8b-c4e5f0d3126d --snapshot 43064761-948f-469d-ac8e-b8e5f0d6056f --force --restore retry
```

---

### `ibmcloud pi snapshot update`
{: #ibmcloud-pi-snapshot-update}

**Alias**: `update, upd`

**Description**: [DEPRECATED] Update a snapshot.

**Usage**:

```bash
update SNAPSHOT_ID [--description DESCRIPTION] [--name NAME]

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

**Available Flags**:

```bash
  -d, --description string   New snapshot description.
  -n, --name string          New name of the snapshot.
```

---

## `ibmcloud pi ssh-key`
{: #ibmcloud-pi-ssh-key}

**Alias**: `ssh-key, ssh`

**Description**: IBM Cloud Power Virtual Server SSH-Keys.

**Usage**: `ssh-key`

**Available Commands**:

- `create`:    Create an SSH-Key with an imported RSA public key.
- `delete`:    Delete an SSH-Key.
- `get`:    View details of an SSH-Key.
- `list`:    List all SSH-Keys.
- `update`:    Update an SSH-Key.

---

### `ibmcloud pi ssh-key create`
{: #ibmcloud-pi-ssh-key-create}

**Alias**: `create, cr`

**Description**: Create an SSH-Key with an imported RSA public key.

**Usage**:

```bash
create KEY_NAME --key KEY [--description DESCRIPTION] [--visibility ("account" | "workspace")]

  KEY_NAME: The name of the key.
```

**Available Flags**:

```bash
  -d, --description string   Description of the SSH-Key.
  -k, --key string           SSH RSA key string within a double quotation marks. For example, "ssh-rsa AAA... "
  -v, --visibility string    Visibility of the SSH-Key. Valid values are: account, workspace.
                             Value of "workspace" means SSH-Key is only accessible in a workspace.
                             Value of "account" means SSH-Key is accessible throughout an account.
                             Default is "workspace".
```

**Examples**:

```bash
    ibmcloud pi ssh-key create test-ssh-key --key ssh-key-sample
```

---

### `ibmcloud pi ssh-key delete`
{: #ibmcloud-pi-ssh-key-delete}

**Alias**: `delete, del`

**Description**: Delete an SSH-Key.

**Usage**:

```bash
delete KEY_NAME

  KEY_NAME: The name of the key.
```

---

### `ibmcloud pi ssh-key get`
{: #ibmcloud-pi-ssh-key-get}

**Alias**: `get`

**Description**: View details of an SSH-Key.

**Usage**:

```bash
get KEY_NAME

  KEY_NAME: The name of the key.
```

---

### `ibmcloud pi ssh-key list`
{: #ibmcloud-pi-ssh-key-list}

**Alias**: `list, ls`

**Description**: List all SSH-Keys.

**Usage**: `list`

---

### `ibmcloud pi ssh-key update`
{: #ibmcloud-pi-ssh-key-update}

**Alias**: `update, upd`

**Description**: Update an SSH-Key.

**Usage**:

```bash
update KEY_NAME [--description DESCRIPTION] [--key KEY] [--name NAME] [--visibility ("account" | "workspace")]

  KEY_NAME: The name of the key.
```

**Available Flags**:

```bash
  -d, --description string   Description of the SSH-Key.
  -k, --key string           SSH RSA key string.
  -n, --name string          SSH-Key name.
  -v, --visibility string    Visibility of the SSH-Key. Valid values are: account, workspace.
                             Value of "workspace" means SSH-Key is only accessible in a workspace.
                             Value of "account" means SSH-Key is accessible throughout an account.
```

---

## `ibmcloud pi storage-pools`
{: #ibmcloud-pi-storage-pools}

**Alias**: `storage-pools, spools`

**Description**: List all storage pools for the targeted region.

**Usage**: `storage-pools`

---

## `ibmcloud pi storage-tiers`
{: #ibmcloud-pi-storage-tiers}

**Alias**: `storage-tiers, stiers`

**Description**: List all storage tiers for the targeted region.

**Usage**: `storage-tiers`

---

## `ibmcloud pi subnet`
{: #ibmcloud-pi-subnet}

**Alias**: `subnet, snet`

**Description**: IBM Cloud Power Virtual Server Subnets.

**Usage**: `subnet`

**Available Commands**:

- `create`:    Create a subnet.
- `delete`:    Delete a subnet.
- `get`:    View details of a subnet.
- `list`:    List all subnets in a workspace.
- `update`:    Update a subnet.

---

### `ibmcloud pi subnet create`
{: #ibmcloud-pi-subnet-create}

**Alias**: `create, cr`

**Description**: Create a subnet.

**Usage**:

```bash
create SUBNET_NAME --cidr-block CIDR --net-type private [--dns-servers "DNS1,[DNSn]]"] [--gateway GATEWAY]
      [--ip-range "startIP-endIP[,startIP-endIP]"] [--mtu MTU] [--user-tags "USER_TAG1[,USER_TAGn]"]

  SUBNET_NAME: The name of the subnet.
```

**Available Flags**:

```bash
  -c, --cidr-block string     Subnet in CIDR notation (192.168.1.0/22).
  -d, --dns-servers strings   Comma separated list of DNS Servers to use for this subnet.
                              127.0.0.1 by default if DNS server is not specified for private subnet types.
                              9.9.9.9 by default for public subnet types.
  -g, --gateway string        Gateway to use for this subnet.
  -i, --ip-range string       IP Addresses range(s) for this subnet, format: startIP-endIP[,startIP-endIP].
  -m, --mtu int               Maximum Transmission Unit. MTU be between 1450 and 9000. Default is 1450.
  -n, --net-type string       Subnet type.
  -u, --user-tags strings     Comma separated list of user tags to be attached to the subnet.
```

**Examples**:

```bash
    ibmcloud pi subnet create test-private-subnet --net-type private --cidr-block "192.168.0.0/24" --ip-range "192.168.0.10-192.168.0.20" --dns-servers "8.8.8.8" --gateway "192.168.0.1"
    ibmcloud pi subnet create test-public-subnet --net-type public --dns-servers "8.8.8.8" --mtu 2000
```

---

### `ibmcloud pi subnet delete`
{: #ibmcloud-pi-subnet-delete}

**Alias**: `delete, del`

**Description**: Delete a subnet.

**Usage**:

```bash
delete SUBNET_ID

  SUBNET_ID: The unique identifier or name of the subnet.
```

---

### `ibmcloud pi subnet get`
{: #ibmcloud-pi-subnet-get}

**Alias**: `get`

**Description**: View details of a subnet.

**Usage**:

```bash
get SUBNET_ID

  SUBNET_ID: The unique identifier or name of the subnet.
```

---

### `ibmcloud pi subnet list`
{: #ibmcloud-pi-subnet-list}

**Alias**: `list, ls`

**Description**: List all subnets in a workspace.

**Usage**: `list`

---

### `ibmcloud pi subnet update`
{: #ibmcloud-pi-subnet-update}

**Alias**: `update, upd`

**Description**: Update a subnet.

**Usage**:

```bash
update SUBNET_ID [--dns-servers "DNS1,[DNSn]"] [--gateway GATEWAY] [--ip-range "startIP-endIP[,startIP-endIP]"] [--name SUBNET_NAME]

  SUBNET_ID: The unique identifier or name of the subnet.
```

**Available Flags**:

```bash
  -d, --dns-servers strings   Comma separated list of DNS Servers to use for this subnet.
  -g, --gateway string        Gateway to use for this subnet.
  -i, --ip-range string       IP Addresses range(s) for this subnet, format: startIP-endIP[,startIP-endIP].
  -n, --name string           New name of the subnet.
```

---

## `ibmcloud pi virtual-serial-number`
{: #ibmcloud-pi-virtual-serial-number}

**Alias**: `virtual-serial-number, vsn`

**Description**: IBM Cloud Power Virtual Server Virtual Serial Number.

**Usage**: `virtual-serial-number`

**Available Commands**:

- `delete`:    Delete a virtual serial number.
- `get`:    View details of a virtual serial number.
- `list`:    List all virtual serial number assigned to an instance or all virtual serial numbers in the workspace.
- `software-tiers`:    List all supported software tiers.
- `update`:    Update a retained virtual serial number.

---

### `ibmcloud pi virtual-serial-number delete`
{: #ibmcloud-pi-virtual-serial-number-delete}

**Alias**: `delete, del`

**Description**: Delete a virtual serial number.

**Usage**:

```bash
delete VIRTUAL_SERIAL_NUMBER

  VIRTUAL_SERIAL_NUMBER: The virtual serial number.
```

---

### `ibmcloud pi virtual-serial-number get`
{: #ibmcloud-pi-virtual-serial-number-get}

**Alias**: `get`

**Description**: View details of a virtual serial number.

**Usage**:

```bash
get VIRTUAL_SERIAL_NUMBER

  VIRTUAL_SERIAL_NUMBER: The virtual serial number.
```

---

### `ibmcloud pi virtual-serial-number list`
{: #ibmcloud-pi-virtual-serial-number-list}

**Alias**: `list, ls`

**Description**: List all virtual serial number assigned to an instance or all virtual serial numbers in the workspace.

**Usage**:

```bash
list ([PVM_INSTANCE_ID] | [--retainVSN=True|False])

  PVM_INSTANCE_ID: The unique identifier or name of the PVM instance.
```

**Available Flags**:

```bash
  -r, --retainVSN   Lists only retained virtual serial numbers. Default is "false".
```

---

### `ibmcloud pi virtual-serial-number software-tiers`
{: #ibmcloud-pi-virtual-serial-number-software-tiers}

**Alias**: `software-tiers, st`

**Description**: List all supported software tiers.

**Usage**: `software-tiers`

---

### `ibmcloud pi virtual-serial-number update`
{: #ibmcloud-pi-virtual-serial-number-update}

**Alias**: `update, upd`

**Description**: Update a retained virtual serial number.

**Usage**:

```bash
update VIRTUAL_SERIAL_NUMBER [--description DESCRIPTION]

  VIRTUAL_SERIAL_NUMBER: The virtual serial number.
```

**Available Flags**:

```bash
  -d, --description string   New virtual serial number description.
```

---

## `ibmcloud pi volume`
{: #ibmcloud-pi-volume}

**Alias**: `volume, vol`

**Description**: IBM Cloud Power Virtual Server Volumes.

**Usage**: `volume`

**Available Commands**:

- `action`:    Perform an action on a volume.
- `bulk-delete`:    Delete multiple volumes.
- `clone`:    IBM Cloud Power Virtual Server Volume Clone Requests. This command can be used to create clone requests whose lifecycle must be managed. It cannot be used to clone single volumes.
- `clone-async`:    IBM Cloud Power Virtual Server Volume Clones. This command asynchronously creates clone tasks whose status can be queried. It can be used to clone one or more volumes.
- `create`:    Create a volume.
- `delete`:    Delete a volume.
- `flash-copy-mapping`:    Get a list of flash copy mappings of a volume directly from primary storage host.
- `get`:    View details of a volume.
- `list`:    List all storage volumes in a workspace.
- `onboarding`:    IBM Cloud Power Virtual Server Volume Onboarding.
- `remote-copy-relationship`:    Get the remote copy relationship information of a volume.
- `snapshot`:    IBM Cloud Power Virtual Server Volume Snapshot.
- `update`:    Update a volume.

---

### `ibmcloud pi volume action`
{: #ibmcloud-pi-volume-action}

**Alias**: `action, act`

**Description**: Perform an action on a volume.

**Usage**:

```bash
action VOLUME_ID [--replication-enabled=True|False] [--target-tier STORAGE_TIER]

  VOLUME_ID: The unique identifier or name of the volume.
```

**Available Flags**:

```bash
  -r, --replication-enabled   Enables storage replication on the volume. Default is "false".
  -t, --target-tier string    Change the storage tier of the volume (use "ibmcloud pi storage-tiers" to see available storage tiers in the targeted region). "Tier5k" volumes cannot exceed 200GB.
```


**Examples**:

```bash
    ibmcloud pi volume action test-volume --replication-enabled
```

---

### `ibmcloud pi volume bulk-delete`
{: #ibmcloud-pi-volume-bulk-delete}

**Alias**: `bulk-delete, bdel`

**Description**: Delete multiple volumes.

**Usage**: `bulk-delete --volumes VOLUME1[,VOLUMEn]`

**Available Flags**:

```bash
  -v, --volumes strings   List of volumes to be deleted.
```

---

### `ibmcloud pi volume clone`
{: #ibmcloud-pi-volume-clone}

**Alias**: `clone, cl`

**Description**: IBM Cloud Power Virtual Server Volume Clone Requests. This command can be used to create clone requests whose lifecycle must be managed. It cannot be used to clone single volumes.

**Usage**: `clone`

**Available Commands**:

- `cancel`:    Cancel a volume clone request.
- `create`:    Create a volume clone request using the specified volumes.
- `delete`:    Delete a volume clone request.
- `execute`:    Execute a volume clone request using the specified options.
- `get`:    View details of a volume clone request.
- `list`:    List all volume clone requests in a workspace.
- `start`:    Starts a volume clone request.

---

#### `ibmcloud pi volume clone cancel`
{: #ibmcloud-pi-volume-clone-cancel}

**Alias**: `cancel, ca`

**Description**: Cancel a volume clone request.

**Usage**:

```bash
cancel VOLUME_CLONE_REQUEST_ID [--force=True|False]

  VOLUME_CLONE_REQUEST_ID: The unique identifier of a volume clone request.
```

**Available Flags**:

```bash
  -f, --force   Force the cancellation of a volume clone request. If false, cancel will only be allowed if the status is 'prepared', or 'available'. If true, cancel will be allowed when the status is NOT completed, cancelling, cancelled, or failed. Default false.
```

**Examples**:

```bash
    ibmcloud pi volume clone cancel 43064761-948f-469d-ac8e-b8e5f0d6056f
```

---

#### `ibmcloud pi volume clone create`
{: #ibmcloud-pi-volume-clone-create}

**Alias**: `create, cr`

**Description**: Create a volume clone request using the specified volumes.

**Usage**:

```bash
create --name VOLUME_CLONE_REQUEST_NAME --volumes VOLUME1[,VOLUMEn]

  VOLUME_CLONE_REQUEST_NAME: The name of a volume clone request.
```

**Available Flags**:

```bash
  -n, --name string       Name to assign to volume clones request.
  -v, --volumes strings   Comma separated list of volume identifiers or names to be cloned.
                          A minimum of 2 Volume IDs are required and at least one of them must be in the in-use state.
```

**Examples**:

```bash
    ibmcloud pi volume clone create --name test-volume-clone --volumes "43064761-948f-469d-ac8e-b8e5f0d6056f,85716e61-948f-309d-de8b-c4e5f0d3126d"
```

---

#### `ibmcloud pi volume clone delete`
{: #ibmcloud-pi-volume-clone-delete}

**Alias**: `delete, del`

**Description**: Delete a volume clone request.

**Usage**:

```bash
delete VOLUME_CLONE_REQUEST_ID

  VOLUME_CLONE_REQUEST_ID: The unique identifier of a volume clone request.
```

**Examples**:

```bash
    ibmcloud pi volume clone delete 43064761-948f-469d-ac8e-b8e5f0d6056f
```

---

#### `ibmcloud pi volume clone execute`
{: #ibmcloud-pi-volume-clone-execute}

**Alias**: `execute, ex`

**Description**: Execute a volume clone request using the specified options.

**Usage**:

```bash
execute VOLUME_CLONE_REQUEST_ID --name BASE_NAME [--replication-enabled=True|False] [--rollback-prepare=True|False] [--target-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]

  VOLUME_CLONE_REQUEST_ID: The unique identifier of a volume clone request.
```

**Available Flags**:

```bash
  -n, --name string           Base name of the new cloned volume(s).
      --replication-enabled   Enables replication for the cloned volume. By default, the replication property of the source volume will be used to determine the replication property of the cloned target volume.
      --rollback-prepare      Determines rollback behavior. If false, execute failure rolls back clone activity but leaves prepared snapshot. If true, Execute failure rolls back clone activity and removes the prepared snapshot. Default false.
  -t, --target-tier string    Target storage tier for the cloned volumes (use "ibmcloud pi storage-tiers" to see available tiers in the targeted region). Default to the storage tier of the original volume(s) if not specified.
  -u, --user-tags strings     Comma separated list of user tags to be attached to the cloned volume.
```

**Examples**:

```bash
    ibmcloud pi volume clone execute 43064761-948f-469d-ac8e-b8e5f0d6056f --name test-volume-clone --rollback-prepare --target-tier tier3 --user-tags "project:customer-poc,env:dev,dataresidency:germany"
```

---

#### `ibmcloud pi volume clone get`
{: #ibmcloud-pi-volume-clone-get}

**Alias**: `get`

**Description**: View details of a volume clone request.

**Usage**:

```bash
get VOLUME_CLONE_REQUEST_ID

  VOLUME_CLONE_REQUEST_ID: The unique identifier of a volume clone request.
```

---

#### `ibmcloud pi volume clone list`
{: #ibmcloud-pi-volume-clone-list}

**Alias**: `list, ls`

**Description**: List all volume clone requests in a workspace.

**Usage**: `list [--filter FILTER]`

**Available Flags**:

```bash
  -f, --filter string   Volume clone filter to limit list items.
                        cancel - includes status values (cancelling)
                        cancelled - includes status values (cancelled)
                        completed - includes status values (completed)
                        execute - includes status values (executing, available-rollback)
                        failed - includes status values (failed)
                        finalized - included status values (completed, failed, cancelled)
                        prepare - includes status values (preparing, prepared)
                        start - includes status values (starting, available)
```

---

#### `ibmcloud pi volume clone start`
{: #ibmcloud-pi-volume-clone-start}

**Alias**: `start, st`

**Description**: Starts a volume clone request.

**Usage**:

```bash
start VOLUME_CLONE_REQUEST_ID

  VOLUME_CLONE_REQUEST_ID: The unique identifier of a volume clone request.
```

**Examples**:

```bash
    ibmcloud pi volume clone start 43064761-948f-469d-ac8e-b8e5f0d6056f
```

---

### `ibmcloud pi volume clone-async`
{: #ibmcloud-pi-volume-clone-async}

**Alias**: `clone-async, cla`

**Description**: IBM Cloud Power Virtual Server Volume Clones. This command asynchronously creates clone tasks whose status can be queried. It can be used to clone one or more volumes.

**Usage**: `clone-async`

**Available Commands**:

- `create`:    Create a volume clone for specific volumes.
- `get`:    Get the status of a clone request for the specified clone task ID.

---

#### `ibmcloud pi volume clone-async create`
{: #ibmcloud-pi-volume-clone-async-create}

**Alias**: `create, cr`

**Description**: Create a volume clone for specific volumes.

**Usage**:

```bash
create CLONE_NAME --volumes VOLUME1[,VOLUMEn] [--replication-enabled=True|False] [--target-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]

  CLONE_NAME:The name of a clone.
```

**Available Flags**:

```bash
  -r, --replication-enabled   Enables replication for the cloned volume. If no value is provided, it will default to the replication status of the source volume.
  -t, --target-tier string    Target storage tier for the cloned volumes (use "ibmcloud pi storage-tiers" to see available tiers in the targeted region). Default to the storage tier of the original volume(s) if not specified.
  -u, --user-tags strings     Comma separated list of user tags to be attached to the cloned volume.
  -v, --volumes strings       Comma separated list of volume identifiers or names to be cloned.
```

**Examples**:

```bash
    ibmcloud pi volume clone-async create test-volume --volumes 43064761-948f-469d-ac8e-b8e5f0d6056f --target-tier tier1 --user-tags "project:customer-poc,env:dev,dataresidency:germany"
```

---

#### `ibmcloud pi volume clone-async get`
{: #ibmcloud-pi-volume-clone-async-get}

**Alias**: `get`

**Description**: Get the status of a clone request for the specified clone task ID.

**Usage**:

```bash
get CLONE_TASK_ID

  CLONE_TASK_ID:The unique identifier of a clone task.
```

---

### `ibmcloud pi volume create`
{: #ibmcloud-pi-volume-create}

**Alias**: `create, cr`

**Description**: Create a volume.

**Usage**:

```bash
create VOLUME_NAME --size SIZE [--count COUNT] [--replication-enabled=True|False] [--replication-sites SITE1[,SITEn]] [--shareable=True|False] [--storage-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]
  pi volume create VOLUME_NAME --size SIZE --storage-pool POOL [--count COUNT] [--replication-enabled=True|False] [--replication-sites SITE1[,SITEn]] [--shareable=True|False] [--storage-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]
  pi volume create VOLUME_NAME --affinity-policy affinity (--affinity-volume VOLUME | --affinity-instance INSTANCE) --size SIZE [--count COUNT] [--replication-enabled=True|False] [--replication-sites SITE1[,SITEn]] [--shareable=True|False] [--storage-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]
  pi volume create VOLUME_NAME --affinity-policy anti-affinity (--anti-affinity-volumes "VOLUME1,[VOLUMEn]" | --anti-affinity-instances "INSTANCE1,[INSTANCEn]") --size SIZE [--count COUNT] [--replication-enabled=True|False] [--replication-sites SITE1[,SITEn]] [--shareable=True|False] [--storage-tier STORAGE_TIER] [--user-tags USER_TAG1[,USER_TAGn]]

  VOLUME_NAME: The name of the volume.
```

**Available Flags**:

```bash
  -i, --affinity-instance string          PVM instance identifier or name to base volume affinity policy against; required if "--affinity-policy affinity" is specified and "--affinity-volume" is not provided.
  -a, --affinity-policy string            Affinity policy for data volume being created. Valid values are "affinity" and "anti-affinity". If "--storage-pool" is provided then this cannot be specified.
  -v, --affinity-volume string            Volume identifier or name to base volume affinity policy against; required if "--affinity-policy affinity" is specified and "--affinity-instance" is not provided.
  -j, --anti-affinity-instances strings   Comma separated list of instance identifiers or names to base volume anti-affinity policy against; required if "--affinity-policy anti-affinity" is specified and "--anti-affinity-volumes" is not provided.
  -w, --anti-affinity-volumes strings     Comma separated list of volume identifiers or names to base volume anti-affinity policy against; required if "--affinity-policy anti-affinity" is specified  and "--anti-affinity-instances" is not provided.
  -c, --count int                         Number of volumes to create. Default is 1.
  -r, --replication-enabled               Enables storage replication on the volume. Default is "false".
      --replication-sites strings         List of replication sites for volume replication. See "ibmcloud pi disaster-recovery" command to get a list of replication sites.
  -e, --shareable                         Whether the volumes can be attached to multiple VMs. Default is "false".
  -s, --size int                          Size of the volume (in GB). Size cannot exceed 200GB for storage tier "Tier5k".
  -p, --storage-pool string               Volume pool where the volume will be created. If the "--storage-pool" flag is set then the "--affinity-policy" flag cannot be specified.
  -t, --storage-tier string               Tier of the volume (use "ibmcloud pi storage-tiers" to see available storage tiers in the targeted region). Default to tier3 if not provided.
  -u, --user-tags strings                 Comma separated list of user tags to be attached to the volume.
```

**Examples**:

```bash
    ibmcloud pi volume create test-volume --size 1
    ibmcloud pi volume create test-volume --size 1 --storage-tier tier1 --affinity-policy anti-affinity --anti-affinity-volumes anti-affinity-volume
    ibmcloud pi volume create test-volume --size 1 --storage-tier tier1 --count 2
    ibmcloud pi volume create test-volume --size 1 --replication-enabled --replication-sites dal10
```

---

### `ibmcloud pi volume delete`
{: #ibmcloud-pi-volume-delete}

**Alias**: `delete, del`

**Description**: Delete a volume.

**Usage**:

```bash
delete VOLUME_ID

  VOLUME_ID: The unique identifier or name of the volume.
```

---

### `ibmcloud pi volume flash-copy-mapping`
{: #ibmcloud-pi-volume-flash-copy-mapping}

**Alias**: `flash-copy-mapping, fcm`

**Description**: Get a list of flash copy mappings of a volume directly from primary storage host.

**Usage**:

```bash
flash-copy-mapping VOLUME_ID

  VOLUME_ID: The unique identifier or name of the volume.
```

---

### `ibmcloud pi volume get`
{: #ibmcloud-pi-volume-get}

**Alias**: `get`

**Description**: View details of a volume.

**Usage**:

```bash
get VOLUME_ID

  VOLUME_ID: The unique identifier or name of the volume.
```

---

### `ibmcloud pi volume list`
{: #ibmcloud-pi-volume-list}

**Alias**: `list, ls`

**Description**: List all storage volumes in a workspace.

**Usage**: `list [--auxiliary=True|False] [--long=True|False] [--replication-enabled=True|False]`

**Available Flags**:

```bash
  -a, --auxiliary             Filter auxiliary volumes if set to "true" or non-auxiliary volumes if set to "false". Default is "true".
  -l, --long                  Retrieve all volume details.
  -r, --replication-enabled   Filter replication-enabled volumes if set to "true" or non-replication-enabled volumes if set to "false". Default is "true".
```

---

### `ibmcloud pi volume onboarding`
{: #ibmcloud-pi-volume-onboarding}

**Alias**: `onboarding, on`

**Description**: IBM Cloud Power Virtual Server Volume Onboarding.

**Usage**: `onboarding`

**Available Commands**:

- `create`:    Create a volume onboarding operation.
- `get`:    Get the information of volume onboarding operation.
- `list`:    List all volume onboarding operations.

---

#### `ibmcloud pi volume onboarding create`
{: #ibmcloud-pi-volume-onboarding-create}

**Alias**: `create, cr`

**Description**: Create a volume onboarding operation.

**Usage**: `create <--auxiliary-volumes "AUXVOLUMENAME1 [NAME1]"> --source-crn SOURCE_CRN [--description DESCRIPTION] [--user-tags USER_TAG1[,USER_TAGn]]`

**Available Flags**:

```bash
  -a, --auxiliary-volumes strings   Comma separated list of identifiers of the volume(s) at storage host level. Repeat this flag to add more auxiliary volumes.
  -d, --description string          Volume onboarding description.
  -s, --source-crn string           CRN of source ServiceBroker instance from where auxiliary volumes need to be onboarded.
  -u, --user-tags strings           Comma separated list of user tags to be attached to the volume onboarding.
```

**Examples**:

```bash
    ibmcloud pi volume onboarding create test-volume --auxiliary-volumes "test-auxiliary-volume-name" --source-crn "crn:v1:staging:public:power-iaas:dal13:a/mockcrn::"
```

---

#### `ibmcloud pi volume onboarding get`
{: #ibmcloud-pi-volume-onboarding-get}

**Alias**: `get`

**Description**: Get the information of volume onboarding operation.

**Usage**:

```bash
get VOLUME_ONBOARDING_ID

  VOLUME_ONBOARDING_ID: The unique identifier of the onboarding operation.
```

---

#### `ibmcloud pi volume onboarding list`
{: #ibmcloud-pi-volume-onboarding-list}

**Alias**: `list, ls`

**Description**: List all volume onboarding operations.

**Usage**: `list`

---

### `ibmcloud pi volume remote-copy-relationship`
{: #ibmcloud-pi-volume-remote-copy-relationship}

**Alias**: `remote-copy-relationship, rcr`

**Description**: Get the remote copy relationship information of a volume.

**Usage**:

```bash
remote-copy-relationship VOLUME_ID

  VOLUME_ID: The unique identifier or name of the volume.
```

---

### `ibmcloud pi volume snapshot`
{: #ibmcloud-pi-volume-snapshot}

**Alias**: `snapshot, snap`

**Description**: IBM Cloud Power Virtual Server Volume Snapshot.

**Usage**: `snapshot`

**Available Commands**:

- `get`:    Get a snapshot for a volume.
- `list`:    List all snapshots in the workspace.

---

#### `ibmcloud pi volume snapshot get`
{: #ibmcloud-pi-volume-snapshot-get}

**Alias**: `get`

**Description**: Get a snapshot for a volume.

**Usage**:

```bash
get SNAPSHOT_ID

  SNAPSHOT_ID: The unique identifier of the snapshot.
```

---

#### `ibmcloud pi volume snapshot list`
{: #ibmcloud-pi-volume-snapshot-list}

**Alias**: `list, ls`

**Description**: List all snapshots in the workspace.

**Usage**: `list`

---

### `ibmcloud pi volume update`
{: #ibmcloud-pi-volume-update}

**Alias**: `update, upd`

**Description**: Update a volume.

**Usage**:

```bash
update VOLUME_ID [--bootable=True|False] [--name NAME] [--size SIZE] [--shareable=True|False]

  VOLUME_ID: The unique identifier or name of the volume.
```

**Available Flags**:

```bash
  -b, --bootable      New value for whether the volume can be booted.
  -n, --name string   New name of the volume.
  -t, --shareable     New value for whether the volume can be attached to multiple VMs.
  -s, --size int      New size of the volume. Size cannot exceed 200GB for storage tier "Tier5k".
```

---

## `ibmcloud pi volume-group`
{: #ibmcloud-pi-volume-group}

**Alias**: `volume-group, vg`

**Description**: IBM Cloud Power Virtual Server Volume Groups.

**Usage**: `volume-group`

**Available Commands**:

- `action`:    Perform an action on a volume group.
- `create`:    Create a volume group.
- `delete`:    Delete a volume group.
- `get`:    View details of a volume group.
- `list`:    List all storage volume groups in a workspace.
- `remote-copy-relationships`:    Get the remote copy relationship information of a volume group.
- `storage-details`:    Get storage details for a volume group.
- `update`:    Update a volume group.

---

### `ibmcloud pi volume-group action`
{: #ibmcloud-pi-volume-group-action}

**Alias**: `action, act`

**Description**: Perform an action on a volume group.

**Usage**:

```bash
action VOLUME_GROUP_ID --operation reset [--status STATUS]
  pi volume-group action VOLUME_GROUP_ID --operation start [--source SOURCE]
  pi volume-group action VOLUME_GROUP_ID --operation stop [--allow-read-access=True|False]


  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

**Available Flags**:

```bash
  -a, --allow-read-access   Allow the auxiliary volume to be accessible after stopping the volume group. Default is "false".
  -o, --operation string    Operation to be done in a volume group. Valid values are: reset, start, stop.
      --source string       The copying volume source. Valid values are: auxiliary, master.Default is "master".
      --status string       New status to be set for a volume group. Default is "available".
```

**Examples**:

```bash
    ibmcloud pi volume-group action test-volume-group --operation reset
    ibmcloud pi volume-group action test-volume-group --operation start --source master
```

---

### `ibmcloud pi volume-group create`
{: #ibmcloud-pi-volume-group-create}

**Alias**: `create, cr`

**Description**: Create a volume group.

**Usage**:

```bash
create (--volume-group-name VOLUME_GROUP_NAME | --consistency-group-name CONSISTENCY_GROUP_NAME) --member-volume-ids "VOLUME_ID_1,[VOLUME_ID_N]"

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

**Available Flags**:

```bash
  -c, --consistency-group-name string   Storage volume group name. This is required to onboard existing volume group on the target site for DR set up.
  -m, --member-volume-ids strings       Comma separated member volume identifiers.
  -v, --volume-group-name string        Storage volume group name. This is required for the creation of new volume group.
```

**Examples**:

```bash
    ibmcloud pi volume-group create --volume-group-name test-volume-group-name --member-volume-ids "43064761-948f-469d-ac8e-b8e5f0d6056f,85716e61-948f-309d-de8b-c4e5f0d3126d"
```

---

### `ibmcloud pi volume-group delete`
{: #ibmcloud-pi-volume-group-delete}

**Alias**: `delete, del`

**Description**: Delete a volume group.

**Usage**:

```bash
delete VOLUME_GROUP_ID

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

---

### `ibmcloud pi volume-group get`
{: #ibmcloud-pi-volume-group-get}

**Alias**: `get`

**Description**: View details of a volume group.

**Usage**:

```bash
get VOLUME_GROUP_ID [--long=True|False]

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

**Available Flags**:

```bash
  -l, --long   Retrieve additional details for the volume group.
```

---

### `ibmcloud pi volume-group list`
{: #ibmcloud-pi-volume-group-list}

**Alias**: `list, ls`

**Description**: List all storage volume groups in a workspace.

**Usage**: `list [--long=True|False]`

**Available Flags**:

```bash
  -l, --long   Retrieve additional details for the volume group.
```

---

### `ibmcloud pi volume-group remote-copy-relationships`
{: #ibmcloud-pi-volume-group-remote-copy-relationships}

**Alias**: `remote-copy-relationships, rcr`

**Description**: Get the remote copy relationship information of a volume group.

**Usage**:

```bash
remote-copy-relationships VOLUME_GROUP_ID

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

---

### `ibmcloud pi volume-group storage-details`
{: #ibmcloud-pi-volume-group-storage-details}

**Alias**: `storage-details, sd`

**Description**: Get storage details for a volume group.

**Usage**:

```bash
storage-details VOLUME_GROUP_ID

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

---

### `ibmcloud pi volume-group update`
{: #ibmcloud-pi-volume-group-update}

**Alias**: `update, upd`

**Description**: Update a volume group.

**Usage**:

```bash
update VOLUME_GROUP_ID [--add-member-volume-ids "VOLUME_ID_1,[VOLUME_ID_N]"] [--remove-member-volume-ids "VOLUME_ID_1,[VOLUME_ID_N]"]

  VOLUME_GROUP_ID: The unique identifier or name of the volume group.
```

**Available Flags**:

```bash
  -a, --add-member-volume-ids strings      Comma separated volume identifiers to add as members of the volume group.
  -r, --remove-member-volume-ids strings   Comma separated volume identifiers to remove as members of the volume group.
```

---

## `ibmcloud pi workspace`
{: #ibmcloud-pi-workspace}

**Alias**: `workspace, ws`

**Description**: IBM Cloud Power Virtual Server Workspaces.

**Usage**: `workspace`

**Available Commands**:

- `context`:    Display the CRN of the currently targeted workspace.
- `create`:    Create a workspace.
- `delete`:    Delete a workspace.
- `list`:    List all workspaces for this account.
- `target`:    Target a workspace.

---

### `ibmcloud pi workspace context`
{: #ibmcloud-pi-workspace-context}

**Alias**: `context, con`

**Description**: Display the CRN of the currently targeted workspace.

**Usage**: `context`

---

### `ibmcloud pi workspace create`
{: #ibmcloud-pi-workspace-create}

**Alias**: `create, cr`

**Description**: Create a workspace.

**Usage**:

```bash
create WORKSPACE_NAME --datacenter DATACENTER --group RESOURCE_GROUP --plan PLAN [--user-tags USER_TAG1[,USER_TAGn]]

  WORKSPACE_NAME: The desired name of the workspace.
```

**Available Flags**:

```bash
  -d, --datacenter string   The datacenter location where the instance should be hosted.
                            Use the "ibmcloud pi datacenter list" command to see values for public datacenters,
                            and the "ibmcloud sat location ls" command to see values for private datacenters.
                            When using the "ibmcloud sat location ls" to get a private datacenter,
                            please prefix "satloc_<REGION>_" to the displayed id.
  -g, --group string        The ID of the resource group. Use the "ibmcloud resource groups" command to see possible values.
  -p, --plan string         Plan associated with the offering. Valid values are "public"/"off-prem" or "private"/"on-prem".
  -u, --user-tags strings   Comma separated list of user tags to be attached to the workspace.
```

**Examples**:

```bash
    ibmcloud pi workspace create test-workspace --datacenter dal12 --group 393843beabcdea9d803840a384093841 --plan public --user-tags "project:customer-poc,env:dev,dataresidency:germany"
```

---

### `ibmcloud pi workspace delete`
{: #ibmcloud-pi-workspace-delete}

**Alias**: `delete, del`

**Description**: Delete a workspace.

**Usage**:

```bash
delete (WORKSPACE_CRN | WORKSPACE_ID)

  WORKSPACE_CRN:  The cloud resource name that uniquely identifies IBM Cloud resources.

  WORKSPACE_ID: The unique identifier of the workspace.
```

---

### `ibmcloud pi workspace list`
{: #ibmcloud-pi-workspace-list}

**Alias**: `list, ls`

**Description**: List all workspaces for this account.

**Usage**: `list ([--long=True|False | --private=True|False])`

**Available Flags**:

```bash
  -l, --long      Retrieve all workspace details.
  -p, --private   List private workspaces.
```

---

### `ibmcloud pi workspace target`
{: #ibmcloud-pi-workspace-target}

**Alias**: `target, tg`

**Description**: Target a workspace.

**Usage**:

```bash
target WORKSPACE_CRN

  WORKSPACE_CRN:  The cloud resource name that uniquely identifies IBM Cloud resources.
```

---
