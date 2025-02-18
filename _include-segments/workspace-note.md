[JIRA-POWERIAAS-17751-start]{: tag-green}

When you create a workspace using the terraform or CLI, consider the following suggestions:

- Terraform resource: [`ibm_resource_instance`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/resource_instance){: external}, use the service name as `power-iaas` for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}}.

- CLI command: [`ibmcloud resource service-instance-create`](https://cloud.ibm.com/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-workspace-create){: external}, use the plan name as `power-virtual-server-group` or `power-virtual-server-private-group` for Power Virtual Server in client locations.

[JIRA-POWERIAAS-17751-end]{: tag-green}
