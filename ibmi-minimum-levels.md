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

# IBM i PTF minimium levels
{: #minimum-levels}

You must install the following program temporary fixes (PTFs) on your IBM i VM:

- IBM i 7.1 - Technology Refresh (TR) level and PTFs required:
  - IBM i 7.1 TR11
  - C7192710 (The final 7.1 GA cumulative PTF level, generally available on July 28, 2017)
  - 7.1 HIPER Group PTF (SF99709) level 261 or later
  - PTFs 5770999: MF67822, MF67656, MF67836, MF67706, MF67715, MF67792, MF67794, MF67795.
  - 5770SS1
  - SI74413
- IBM i 7.2 - 5770SS1 SI71091 (prereqs SLIC PTFs: MF66395, MF66394, MF66391)
- IBM i 7.3 - MF99207 (TR7) and SI69686
- IBM i 7.4 - MF99301 (TR1) and SI70544

If you are bringing your own IBM i custom image, you must install these PTFs and the software that is required for `cloud-init`. For more information, see [Cloud-Init Support for IBM i](https://www.ibm.com/support/pages/node/1166194){: new_window}{: external}.

## Installing cloud-init on IBM i 7.1
{: install-cloud-init-ibmi-7.1}

You can install cloud-init on IBM I 7.1 by completing the following steps:

1. Install the following required license programs:
   - 5733OPS with option base, 3, 4, 7 and 9
   - 5733SC1 with *ALL option
   - 5770DG1 with *ALL
   - 5770SS1 with Option 30 and 33
2. Install the following required PTFs and PTF groups:
   - cloud-init PTFs:  SI63073, SI64612
   - Dependent PTF groups: SF99368, SF99123
   - Dependent PTFs:  MF61937(apply permanently), SI69146, SI65636, SI64092, SI66737, SI65647, SI73750, SI63164 and SI74413
3. Run command `CALL PGM(QSYS/QAENGCHG) PARM(*ENABLECI)` before you capture the VM.
