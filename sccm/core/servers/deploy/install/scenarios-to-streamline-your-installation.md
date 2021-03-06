---
title: "Install scenarios | Microsoft Docs"
description: "Learn techniques for installing a new Configuration Manager hierarchy when you are updating or upgrading."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brendunsms.author: brendunsmanager: angrobe

---
# Scenarios to streamline your installation of System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
With the release of update versions for System Center Configuration Manager current branch, there are new scenarios to streamline the install of a new hierarchy to an update version (like update 1602), and to upgrade from Microsoft System Center 2012 Configuration Manager.  

Supported scenarios include:  

**Install a new System Center Configuration Manager current branch hierarchy** that runs an update version:  

-   You only install the top-tier site followed immediately by installing an update to bring that site up to the update version you will use. Then you can install additional sites directly to that update version.  

-   This scenario skips installing additional sites to a baseline level and then having to update them to the update version you want to use.  

-   This scenario skips installing clients to a baseline version, and then having to reinstall them when you update to a later version.  

**Upgrade Microsoft System Center 2012 Configuration Manager** infrastructure to an update version of System Center Configuration Manager:  

-   You manually upgrade your central administration site and each primary site to a baseline version (like 1511) before you can install an update version (like 1602).  

-   You do not upgrade secondary sites from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version you will use.  

-   You do not upgrade clients from Microsoft System Center 2012 Configuration Manager until your primary sites run the update version you will use.  

## Scenario - Install a new hierarchy to an update version  
In this example scenario, you install the first site of a hierarchy using a baseline version of System Center Configuration Manager, version 1511. Then you install the 1602 update before deploying additional sites or clients.  

-   Because you plan to use an update version (like 1602) and not remain at a baseline version (like 1511), you do not need to install additional sites and then upgrade them, or install and then upgrade clients.  

-   You do not install secondary sites with version 1511 and then upgrade them to 1602. Instead, you will install them after your primary sites run 1602.  

**Use the following sequence:**  

1.  **Install a top-level site for your new hierarchy** using the baseline media.  

    -   You can only use baseline media to install the first site of a new hierarchy.  

    -   For example, install a top-level site using the baseline version of 1511. See [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  

    After this step, your top-level site runs version 1511.  

2.  **Use in-console updates to update your top-level site to a later version.**  

    -   Before you install any child sites or clients, update your top-level site to the update version you plan to use.  

    -   For example, you can update your top-level site that runs version 1511 to version 1602. See [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    After this step, your top-level site runs version 1602.  

3.  **Install new child primary sites below a central administration site.**  

    -   Use the installation media from the CD.Latest folder on the central administration site server to install child primary sites.  (See [The CD.Latest folder for System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md))  

        -   This source media is required to ensure that new child primary sites match the version of the central administration site.  

    After this step, your new child primary sites run version 1602.  

4.  **At each primary site, use the in-console option to install new secondary sites.**  

    -   Because you did not install secondary sites while primary sites were at version 1511, you do not need to upgrade secondary sites.  

    -   Instead you install new secondary sites that run version 1602. See *Install a secondary site* in [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  .  

    After this step, new secondary sites are installed and run version 1602.  

5.  **Install new clients at primary site.**  

    -   Because you did not install clients while primary sites were at version 1511, you do not need to upgrade clients from 1511 to 1602.  

    -   Instead, you install new clients that run version 1602. See [Deploy clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    After this step, new clients are installed that run version 1602.  

## Scenario - Upgrade System Center 2012 Configuration Manager to an update version of System Center Configuration Manager current branch  
In this example scenario, you upgrade your Microsoft System Center 2012 Configuration Manager infrastructure to an update version of System Center Configuration Manager, like version 1602.  

-   The central administration site and each primary site must upgrade to the baseline version 1511 before you install the update for version 1602.  

-   Secondary sites and clients do not upgrade or install 1511. Instead they move directly from Microsoft System Center 2012 Configuration Manager to System Center Configuration Manager version 1602.  

**Use the following sequence:**  

1.  **Upgrade your top-level Microsoft System Center 2012 Configuration Manager site** to a baseline version of the current branch by using source media for System Center Configuration Manager (like version 1511). See [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Like traditional upgrade scenarios, you always upgrade the top-level site of a hierarchy first, and then upgrade child sites.  

    After this step, your top-level site runs 1511.  

2.  **Upgrade each child primary site in your hierarchy** to that same baseline version.  

    -   When you upgrade from Microsoft System Center 2012 Configuration Manager, you must manually upgrade each primary site to a baseline version of the current branch.  

    -   You will not upgrade secondary sites at this time.  

    After this step, each primary site runs version 1511.  

3.  **Set maintenance windows on child-primary sites.** After you upgrade all your primary sites to the baseline version, plan to configure maintenance windows  to control when those sites install infrastructure updates. See [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Maintenance windows are called service windows in version 1511.)  

    -   A child primary site automatically installs the same updates that you install at a central administration site.  

    -   Secondary sties do not automatically install new versions and must be upgraded manually from within the console.  

    > [!NOTE]  
    >  If you use version 1511 and want to use service windows, you must first install the hotfix from the [Microsoft Knowledge Base article 3142341](http://support.microsoft.com/kb/3142341). This issue is resolved when you install the 1602 update.  

    After this step, when you install updates at the central administration site, child primary sites will only install that update when allowed by their maintenance window.  

4.  **Install the update version at your top-level site.** This updates your top-level site. After a central administration site installs the update version, each child primary site automatically installs the update unless blocked by a maintenance window.  

    -   For example, you can update your top-level site from version 1511 to version 1602. See [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

    After this step, your central administration site and each primary sites runs version 1602.  

5.  **Upgrade secondary sites.** After a primary site installs the update and runs version 1602, you use the in-console option to upgrade secondary sites.  

    -   This upgrades secondary sites directly from Microsoft System Center 2012 Configuration Manager to the update version you installed at the primary site.  

    -   For information about upgrading a secondary site, see [Upgrade sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) in [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6.  **Upgrade clients.** Use the information in [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   This upgrades clients directly from Microsoft System Center 2012 Configuration Manager to the update version you installed at the primary site.  

    After this step, clients are upgraded to version 1602 without first upgrading to version 1511.
