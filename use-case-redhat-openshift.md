---

copyright:
  years: 2020, 2024

lastupdated: "2024-12-03"

keywords: Red hat use case, use case, Application, modernization, cloud, native

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Cloud native development and application modernization by using Red Hat OpenShift on IBM {{site.data.keyword.powerSys_notm}}
{: #app-modernization-using-RedHat-openshift}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Cloud-native applications are the applications that are **born in the cloud**, which means that the applications use microservice-based architecture, containers, and a corresponding container orchestration platform. Red Hat&reg; OpenShift&reg; is an enterprise Kubernetes platform enabling IT organizations to develop applications faster, deploy them reliably, and manage them efficiently.



In addition to developing new cloud-native applications, IT organizations are modernizing older, monolithic core business applications to support the faster delivery of new functions to the business.

For more information about application modernization on IBM Power, see [Field Guide to Application Modernization on IBM Power](https://www.ibm.com/downloads/cas/D9POQ3YR){: external}.

You can deploy Red Hat OpenShift on {{site.data.keyword.powerSys_notm}} by using one of the following possible deployment methods:
- [{{site.data.keyword.off-prem}}]{: tag-blue} IPI (Installer-Provisioned Installation) - Creates all the necessary infrastructure services within the Red Hat OpenShift cluster and provides a turn-key solution. Choose this deployment method for an automated and faster installation. For more information, see [Installing OpenShift Container Platform on {{site.data.keyword.powerSys_notm}} with IPI](https://docs.redhat.com/en/documentation/openshift_container_platform_installation/4.13/html/installing_on_ibm_power_virtual_server/index){: external}.
- UPI (User Provisioned Infrastructure) - Uses a manual process specific to your environment that gives the administrator the ability to create and manage OpenShift nodes themselves. For more information, see [Installing OpenShift Container Platform on {{site.data.keyword.powerSys_notm}} with UPI](https://docs.openshift.com/container-platform/4.13/installing/installing_platform_agnostic/installing-platform-agnostic.html){: external}.
- Additionally, IBM developers created a set of playbooks to help you get started with a UPI installation. You can use these playbooks as-is, or take as examples. For more information, see the [GitHub Playbooks](https://github.com/ocp-power-automation/ocp4-upi-powervs){: external}.

For application storage, you can deploy the IBM&reg; Block Storage CSI driver for {{site.data.keyword.powerSys_notm}} into Red Hat OpenShift clusters running on both {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem}} offerings of IBM {{site.data.keyword.powerSys_notm}}. For more information, see [readme file](https://github.com/kubernetes-sigs/ibm-powervs-block-csi-driver/blob/main/README.md){: external}.
