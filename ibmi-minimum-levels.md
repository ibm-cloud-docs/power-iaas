---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-08"

keywords: ibm i, program temporary fixes

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Minimium PTF levels for IBM i
{: #minimum-levels}

You must install the following program temporary fixes (PTFs) depending on the version of IBM i that you are using:

- IBM i 7.1 Technology Refresh (TR) 11
  - C7192710 (IBM i 7.1 cumulative PTF level)
  - IBM i 7.1 HIPER Group PTF (SF99709) level 261, or later
  - 5770999 (PTFs: MF67822, MF67656, MF67836, MF67706, MF67715, MF67792, MF67794, MF67795, MF68346)
  - 5770SS1 (PTF: SI74413, SI75274, SI75050)
- IBM i 7.2 - 5770SS1 SI71091 (prerequisite System Licensed Internal Code (SLIC) PTFs: MF66395, MF66394, MF66391)
- IBM i 7.3 - MF99207 (TR7) and SI69686
- IBM i 7.4 - MF99301 (TR1) and SI70544

If you are using your own IBM i custom image of IBM i 7.1, and later, you must install these PTFs and the software that is required for `Cloud-Init`. For more information, see [Cloud-Init Support for IBM i](https://www.ibm.com/support/pages/node/1166194){: new_window}{: external}. For IBM i 7.1, you must perform the following instructions in addition to installing the required PTFs.
## Installing Cloud-Init on IBM i VM
{: install-cloud-init-ibmi-7.1}

To install Cloud-Init on IBM i 7.1, complete the following steps:

1. Install the following license programs:
   - 5733OPS with Option base, 3, 4, 7, and 9
   - 5733SC1 with Option *ALL
   - 5770DG1 with Option *ALL
   - 5770SS1 with Option 30 and 33
2. Install the following PTFs and PTF groups:
   - Cloud-Init PTFs:  SI63073, SI64612
   - Dependent PTF groups: SF99368, SF99123
   - Dependent PTFs:  MF61937 (apply permanently), SI69146, SI65636, SI64092, SI66737, SI65647, SI73750, SI63164, and SI74413
3. Run the following command before you capture the VM:
   `CALL PGM(QSYS/QAENGCHG) PARM(*ENABLECI)`
