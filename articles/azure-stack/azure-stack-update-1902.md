---
title: Azure Stack 1902 update | Microsoft Docs
description: Learn about the 1902 update for Azure Stack integrated systems, including what's new, known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''

ms.assetid:  
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2019
ms.author: sethm
ms.reviewer: adepue
ms.lastreviewed: 03/07/2019
---

# Azure Stack 1902 update

*Applies to: Azure Stack integrated systems*

This article describes the contents of the 1902 update package. The update includes improvements, fixes, and new features for this version of Azure Stack. This article also describes known issues in this release, and includes a link to download the update. Known issues are divided into issues directly related to the update process, and issues with the build (post-installation).

> [!IMPORTANT]  
> This update package is only for Azure Stack integrated systems. Do not apply this update package to the Azure Stack Development Kit.

## Build reference

The Azure Stack 1902 update build number is **1.1902.0.69**.

## Hotfixes

Azure Stack releases hotfixes on a regular basis. Be sure to install the [latest Azure Stack hotfix](#azure-stack-hotfixes) for 1901 before updating Azure Stack to 1902.

Azure Stack hotfixes are only applicable to Azure Stack integrated systems; do not attempt to install hotfixes on the ASDK.

> [!TIP]  
> Subscribe to the following *RSS* or *Atom* feeds to keep up with Azure Stack hotfixes:
> - [RSS](https://support.microsoft.com/app/content/api/content/feeds/sap/en-us/32d322a8-acae-202d-e9a9-7371dccf381b/rss)
> - [Atom](https://support.microsoft.com/app/content/api/content/feeds/sap/en-us/32d322a8-acae-202d-e9a9-7371dccf381b/atom)

### Azure Stack hotfixes

- **1809**: [KB 4481548 – Azure Stack hotfix 1.1809.12.114](https://support.microsoft.com/help/4481548/)
- **1811**: No current hotfix available.
- **1901**: No current hotfix available.
- **1902**: No current hotfix available.

## Prerequisites

> [!IMPORTANT]
- Install the [latest Azure Stack hotfix](#azure-stack-hotfixes) for 1901 (if any) before updating to 1902.

- Before you start installation of this update, run [Test-AzureStack](azure-stack-diagnostic-test.md) with the following parameters to validate the status of your Azure Stack and resolve any operational issues found, including all warnings and failures. Also review active alerts, and resolve any that require action:

    ```PowerShell
    Test-AzureStack -Include AzsControlPlane, AzsDefenderSummary, AzsHostingInfraSummary, AzsHostingInfraUtilization, AzsInfraCapacity, AzsInfraRoleSummary, AzsPortalAPISummary, AzsSFRoleSummary, AzsStampBMCSummary, AzsHostingServiceCertificates
    ```

- When Azure Stack is managed by System Center Operations Manager (SCOM), make sure to update the [Management Pack for Microsoft Azure Stack](https://www.microsoft.com/download/details.aspx?id=55184) to version 10.0.3.11 before applying 1902.

- The package format for the Azure Stack update has changed from **.bin/.exe/.xml** to **.zip/.xml** starting with the 1902 release. Customers with connected Azure Stack scale units will see the **Update available** message in the portal. Customers that are not connected can now simply download and import the .zip file with the corresponding .xml.

<!-- ## New features -->

<!-- ## Fixed issues -->

## Changes

- The 1902 build introduces a new user interface on the Azure Stack Administrator portal for creating plans, offers, quotas, and add-on plans. For more information, including screenshots, see [Create plans, offers, and quotas](azure-stack-create-plan.md).

## Common vulnerabilities and exposures

This update installs the following security updates:  
- [ADV190005](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/ADV190006)
- [CVE-2019-0595](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0595)
- [CVE-2019-0596](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0596)
- [CVE-2019-0597](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0597)
- [CVE-2019-0598](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0598)
- [CVE-2019-0599](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0599)
- [CVE-2019-0600](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0600)
- [CVE-2019-0601](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0601)
- [CVE-2019-0602](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0602)
- [CVE-2019-0615](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0615)
- [CVE-2019-0616](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0616)
- [CVE-2019-0618](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0618)
- [CVE-2019-0619](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0619)
- [CVE-2019-0621](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0621)
- [CVE-2019-0623](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0623)
- [CVE-2019-0625](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0625)
- [CVE-2019-0626](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0626)
- [CVE-2019-0627](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0627)
- [CVE-2019-0628](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0628)
- [CVE-2019-0630](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0630)
- [CVE-2019-0631](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0631)
- [CVE-2019-0632](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0632)
- [CVE-2019-0633](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0633)
- [CVE-2019-0635](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0635)
- [CVE-2019-0636](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0636)
- [CVE-2019-0656](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0656)
- [CVE-2019-0659](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0659)
- [CVE-2019-0660](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0660)
- [CVE-2019-0662](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0662)
- [CVE-2019-0663](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0663)


For more information about these vulnerabilities, click on the preceding links, or see Microsoft Knowledge Base articles [4487006](https://support.microsoft.com/en-us/help/4487006).

## Known issues with the update process

- When you run [Test-AzureStack](azure-stack-diagnostic-test.md), a warning message from the Baseboard Management Controller (BMC) is displayed. You can safely ignore this warning.

- <!-- 2468613 - IS --> During installation of this update, you might see alerts with the title `Error – Template for FaultType UserAccounts.New is missing.`  You can safely ignore these alerts. The alerts close automatically after the installation of this update completes.

## Post-update steps

- After the installation of this update, install any applicable hotfixes. For more information, see [Hotfixes](#hotfixes), as well as our [Servicing Policy](azure-stack-servicing-policy.md).  

- Retrieve the data at rest encryption keys and securely store them outside of your Azure Stack deployment. Follow the [instructions on how to retrieve the keys](azure-stack-security-bitlocker.md).

## Known issues (post-installation)

The following are post-installation known issues for this build version.

### Portal

<!-- 2930820 - IS ASDK --> 
- In both the administrator and user portals, if you search for "Docker," the item is incorrectly returned. It is not available in Azure Stack. If you try to create it, a blade with an error indication is displayed. 

<!-- 2931230 – IS  ASDK --> 
- Plans that are added to a user subscription as an add-on plan cannot be deleted, even when you remove the plan from the user subscription. The plan will remain until the subscriptions that reference the add-on plan are also deleted. 

<!-- TBD - IS ASDK --> 
- The two administrative subscription types that were introduced with version 1804 should not be used. The subscription types are **Metering subscription**, and **Consumption subscription**. These subscription types are visible in new Azure Stack environments beginning with version 1804 but are not yet ready for use. You should continue to use the **Default Provider** subscription type.

<!-- 3557860 - IS ASDK --> 
- Deleting user subscriptions results in orphaned resources. As a workaround, first delete user resources or the entire resource group, and then delete the user subscriptions.

<!-- 1663805 - IS ASDK --> 
- You cannot view permissions to your subscription using the Azure Stack portals. As a workaround, use [PowerShell to verify permissions](/powershell/module/azs.subscriptions.admin/get-azssubscriptionplan).

<!-- ### Health and monitoring -->

### Compute

- When creating a new Windows Virtual Machine (VM), the following error may be displayed:

   `'Failed to start virtual machine 'vm-name'. Error: Failed to update serial output settings for VM 'vm-name'`

   The error occurs if you enable boot diagnostics on a VM but delete your boot diagnostics storage account. To work around this issue, recreate the storage account with the same name as you used previously.

<!-- 2967447 - IS, ASDK, to be fixed in 1902 -->
- The virtual machine scale set (VMSS) creation experience provides CentOS-based 7.2 as an option for deployment. Because that image is not available on Azure Stack, either select another operating system for your deployment, or use an Azure Resource Manager template specifying another CentOS image that has been downloaded prior to deployment from the marketplace by the operator.  

<!-- TBD - IS ASDK --> 
- After applying the 1902 update, you might encounter the following issues when deploying VMs with Managed Disks:

   - If the subscription was created before the 1808 update, deploying a VM with Managed Disks might fail with an internal error message. To resolve the error, follow these steps for each subscription:
      1. In the Tenant portal, go to **Subscriptions** and find the subscription. Select **Resource Providers**, then select **Microsoft.Compute**, and then click **Re-register**.
      2. Under the same subscription, go to **Access Control (IAM)**, and verify that **Azure Stack – Managed Disk** is listed.
   - If you have configured a multi-tenant environment, deploying VMs in a subscription associated with a guest directory might fail with an internal error message. To resolve the error, follow these steps in [this article](azure-stack-enable-multitenancy.md#registering-azure-stack-with-the-guest-directory) to reconfigure each of your guest directories.

- An Ubuntu 18.04 VM created with SSH authorization enabled will not allow you to use the SSH keys to log in. As a workaround, use VM access for the Linux extension to implement SSH keys after provisioning, or use password-based authentication.

- In build 1902, the memory required by the ERCS infrastructure VM was increased from 8 GB to 12 GB. On an ASDK, this results in a 4 GB increase. On an Azure Stack integrated systems installation, it is a 12 GB increase.

   To make sure the patch and update process results in the least amount of tenant downtime, make sure your Azure Stack stamp has more than 12 GB of available space in the **Capacity** blade. You can see this memory increase reflected in the **Capacity** blade after a successful installation of the update.

### Networking  

<!-- 3239127 - IS, ASDK -->
- In the Azure Stack portal, when you change a static IP address for an IP configuration that is bound to a network adapter attached to a VM instance, you will see a warning message that states 

    `The virtual machine associated with this network interface will be restarted to utilize the new private IP address...`.

    You can safely ignore this message; the IP address will be changed even if the VM instance does not restart.

<!-- 3632798 - IS, ASDK -->
- In the portal, if you add an inbound security rule and select **Service Tag** as the source, several options are displayed in the **Source Tag** list that are not available for Azure Stack. The only options that are valid in Azure Stack are as follows:

  - **Internet**
  - **VirtualNetwork**
  - **AzureLoadBalancer**
  
  The other options are not supported as source tags in Azure Stack. Similarly, if you add an outbound security rule and select **Service Tag** as the destination, the same list of options for **Source Tag** is displayed. The only valid options are the same as for **Source Tag**, as described in the previous list.

- Network security groups (NSGs) do not work in Azure Stack in the same way as global Azure. In Azure, you can set multiple ports on one NSG rule (using the portal, PowerShell, and Resource Manager templates). In Azure Stack however, you cannot set multiple ports on one NSG rule via the portal. To work around this issue, use a Resource Manager template or PowerShell to set these additional rules.

<!-- 3203799 - IS, ASDK -->
- Azure Stack does not support attaching more than 4 Network Interfaces (NICs) to a VM instances today, regardless of the instance size.

- An issue has been identified in which packets over 1450 bytes to an Internal Load Balancer (ILB) are dropped. The issue is due to the MTU setting on the host being too low to accommodate VXLAN encapsulated packets that traverse the role, which as of 1901 has been moved to the host. There are at least two scenarios that you might encounter in which we have seen this issue manifest itself:

  - SQL queries to SQL Always-On that is behind an Internal Load Balancer (ILB), and are over 660 bytes.
  - Kubernetes deployments fail if you attempt to enable multiple masters.  

  The issue occurs when you have communication between a VM and an ILB in the same virtual network but on different subnets. You can work around this issue by running the following commands in an elevated command prompt on the ASDK host:

  ```shell
  netsh interface ipv4 set sub "hostnic" mtu=1660
  netsh interface ipv4 set sub "management" mtu=1660
  ```

<!-- ### SQL and MySQL-->

### App Service

<!-- 2352906 - IS ASDK --> 
- You must register the storage resource provider before you create your first Azure Function in the subscription.


<!-- ### Usage -->

 
<!-- #### Identity -->
<!-- #### Marketplace -->

## Download the update

You can download the Azure Stack 1902 update package from [here](https://aka.ms/azurestackupdatedownload). 

In connected scenarios only, Azure Stack deployments periodically check a secured endpoint and automatically notify you if an update is available for your cloud. For more information, see [managing updates for Azure Stack](azure-stack-updates.md#using-the-update-tile-to-manage-updates).

## Next steps

- For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).  
- For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).
- To review the servicing policy for Azure Stack integrated systems, and what you must do to keep your system in a supported state, see [Azure Stack servicing policy](azure-stack-servicing-policy.md).  
- To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).  
