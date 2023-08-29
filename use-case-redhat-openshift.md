---

copyright:
  years: 2020, 2023

lastupdated: "2023-08-29"

keywords: use case, Application, modernization, cloud, native

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

# Cloud native development and application modernization by using Red Hat OpenShift on Power Systems Virtual Server
{: #app-modernization-using-RedHat-openshift}

Cloud-native applications are the applications that are **born in the cloud**, which means that the applications use microservice-based architecture, containers, and a corresponding container orchestration platform. Red Hat&reg; OpenShift&reg; is enterprise Kubernetes platform enabling IT organizations to develop applications faster, deploy them reliably, and manage them efficiently.

By packaging and running existing monolithic applications within Red Hat OpenShift Container Platform, enterprises can achieve a lower infrastructure footprint, lower maintenance and support costs, and easier portability across a range of cloud infrastructure and platform services.

For information on application modernization on Power Systems, see [Field Guide to Application Modernization on IBM Power Systems](https://www.ibm.com/downloads/cas/D9POQ3YR){: external}.

You can deploy Red Hat OpenShift on {{site.data.keyword.powerSys_notm}} in the following possible deployment methods: <!-- IPI is not applicable to PPCAS -->
- IPI (Installer-provisioned installation) - Includes all the necessary infrastructure services within the Red Hat OpenShift cluster and provides a turn-key solution. Choose this for a automated and faster installation. For more information, see [Installing OpenShift Container Platform on {{site.data.keyword.powerSys_notm}} with IPI](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.13/html/installing/installing-on-ibm-power-virtual-server){: external}.
- UPI (User Provisioned Infrastructure) - Uses the pre-existing install process that gives the administrator the ability to create and manage OpenShift nodes themselves. For more information, see [Installing OpenShift Container Platform on {{site.data.keyword.powerSys_notm}} with UPI](https://docs.openshift.com/container-platform/4.13/installing/installing_platform_agnostic/installing-platform-agnostic.html){: external}.
- Additionally, IBM developers have created a set of playbooks to help you get started with a UPI install. You can use this as-is, or take as examples. For more information, see the [Github Playbooks](https://github.com/ocp-power-automation/ocp4-upi-powervs){: external}.