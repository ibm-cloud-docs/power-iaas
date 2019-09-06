---

copyright:
  years: 2019

lastupdated: "2019-09-06"

keywords: accessing attached volume, system service tools, dedicated service tools

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Accessing an attached volume on IBM i (required)
{: #miv-attaching}

Complete the following tasks to get into **System Service Tools** (SST) and configure the newly attached disk:

1. Enter the `wkrsysval qipltype` command and change the value to **1**.
2. Enter the `pwrdwnsys` command to restart the IBM i operating system (OS).
3. At the **Dedicated Service Tools** (DST) console on restart, enter `QSECOFR/QSECOFR` and change the password.
4. Enter the `wrksysval qipltype` command and change the value to **0**.
5. Reenter the `pwrdwnsys` command to restart the IBM i OS again.

You should now be able to log in, run STRSST, and manage the newly attached disk as the password is manageable.
