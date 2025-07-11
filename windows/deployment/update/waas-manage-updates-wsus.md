---
title: Deploy updates using Windows Server Update Services
description: WSUS allows companies to defer, selectively approve, choose when delivered, and determine which devices receive updates.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: bpardi
ms.collection:
  - highpri
  - tier2
ms.localizationpriority: medium
appliesto:
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
- ✅ <a href=https://learn.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus > WSUS </a>
ms.date: 06/17/2025
---

# Deploy Windows client updates using Windows Server Update Services (WSUS)

> **Looking for consumer information?** See [Windows Update: FAQ](https://support.microsoft.com/help/12373/windows-update-faq)


WSUS is a Windows Server role available in the Windows Server operating systems. It provides a single hub for Windows updates within an organization. WSUS allows companies not only to defer updates but also to selectively approve them, choose when they're delivered, and determine which individual devices or groups of devices receive them. WSUS provides additional control over Windows Update client policies but doesn't provide all the scheduling options and deployment flexibility that Microsoft Configuration Manager provides.

When you choose WSUS as your source for Windows updates, you use Group Policy to point Windows client devices to the WSUS server for their updates. From there, updates are periodically downloaded to the WSUS server and managed, approved, and deployed through the WSUS administration console or Group Policy, streamlining enterprise update management. If you're currently using WSUS to manage Windows updates in your environment, you can continue to do so in Windows 11.

> [!NOTE]
> WSUS is deprecated and is no longer adding new features. However, it continues to be supported for production deployments, and receives security and quality updates as per the product lifecycle. For more info, see [Features removed or no longer developed in Windows Server](/windows-server/get-started/removed-deprecated-features-windows-server).

## Requirements for Windows client servicing with WSUS

To be able to use WSUS to manage and deploy Windows feature updates, you must use a supported WSUS on a supported operating system version:
- WSUS role in Windows Server 2016
- WSUS role in Windows Server 2019
- WSUS role in Windows Server 2022
- WSUS role in Windows Server 2025

For more information about deploying the WSUS role, see [Windows Server Update Services (WSUS) overview](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).

## WSUS scalability

To use WSUS to manage all Windows updates, some organizations may need access to WSUS from a perimeter network, or they might have some other complex scenario. WSUS is highly scalable and configurable for organizations of any size or site layout. For specific information about scaling WSUS, including upstream and downstream server configuration, branch offices, WSUS load balancing, and other complex scenarios, see [Deploy Windows Server Update Services](/windows-server/administration/windows-server-update-services/deploy/deploy-windows-server-update-services).


## Configure automatic updates and update service location

When using WSUS to manage updates on Windows client devices, start by configuring the **Configure Automatic Updates** and **Intranet Microsoft Update Service Location** Group Policy settings for your environment. Doing so forces the affected clients to contact the WSUS server so that it can manage them. The following process describes how to specify these settings and deploy them to all devices in the domain.

**To configure the Configure Automatic Updates and Intranet Microsoft Update Service Location Group Policy settings for your environment**

1. Open Group Policy Management Console (gpmc.msc).

2. Expand *Forest\Domains\\*Your_Domain**.

3. Right-click **Your_Domain**, and then select **Create a GPO in this domain, and Link it here**.

   ![Create a GPO in this domain example in the UI.](images/waas-wsus-fig3.png)

   >[!NOTE]
   >In this example, the **Configure Automatic Updates** and **Intranet Microsoft Update Service Location** Group Policy settings are specified for the entire domain. This isn't a requirement; you can target these settings to any security group by using Security Filtering or a specific OU.

4. In the **New GPO** dialog box, name the new GPO **WSUS - Auto Updates and Intranet Update Service Location**.

5. Right-click the **WSUS - Auto Updates and Intranet Update Service Location** GPO, and then select **Edit**.

6. In the Group Policy Management Editor, go to Computer Configuration\Policies\Administrative Templates\Windows Components\Windows Update.

7. Right-click the **Configure Automatic Updates** setting, and then select **Edit**.

   ![Configure Automatic Updates in the UI.](images/waas-wsus-fig4.png)

8. In the **Configure Automatic Updates** dialog box, select **Enable**.

9. Under **Options**, from the **Configure automatic updating** list, select **3 - Auto download and notify for install**, and then select **OK**.

   ![Select Auto download and notify for install in the UI.](images/waas-wsus-fig5.png)

   >[!IMPORTANT]
   > - Use Regedit.exe to check that the following key isn't enabled, because it can break Windows Store connectivity: Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\DoNotConnectToWindowsUpdateInternetLocations
   > - There are three other settings for automatic update download and installation dates and times. This is simply the option this example uses. For more examples of how to control automatic updates and other related policies, see [Configure Automatic Updates by Using Group Policy](/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates).

10. Right-click the **Specify intranet Microsoft update service location** setting, and then select **Edit**.

11. In the **Specify intranet Microsoft update service location** dialog box, select **Enable**.

12. Under **Options**, in the **Set the intranet update service for detecting updates** and **Set the intranet statistics server** options, type `http://Your_WSUS_Server_FQDN:PortNumber`, and then select **OK**.

    ![Set the intranet statistics server in the UI.](images/waas-wsus-fig6.png)

    >[!NOTE]
    > - The URL `http://Your_WSUS_Server_FQDN:PortNumber` in the following image is just an example. In your environment, be sure to use the server name and port number for your WSUS instance.
    > - The default HTTP port for WSUS is 8530, and the default HTTP over Secure Sockets Layer (HTTPS) port is 8531. (The other options are 80 and 443; no other ports are supported.)

As Windows clients refresh their computer policies (the default Group Policy refresh setting is 90 minutes and when a computer restarts), computers start to appear in WSUS. Now that clients are communicating with the WSUS server, create the computer groups that align with your deployment rings.

## Create computer groups in the WSUS Administration Console

You can use computer groups to target a subset of devices that have specific quality and feature updates. These groups represent your deployment rings, as controlled by WSUS. You can populate the groups either manually by using the WSUS Administration Console or automatically through Group Policy. Regardless of the method you choose, you must first create the groups in the WSUS Administration Console.

**To create computer groups in the WSUS Administration Console**

1. Open the WSUS Administration Console.

2. Go to *Server_Name*\Computers\All Computers, and then select **Add Computer Group**.

    ![Add Computer Group in the WSUS Administration UI.](images/waas-wsus-fig7.png)

3. Type **Ring 2 Pilot Business Users** for the name, and then select **Add**.

4. Repeat these steps for the **Ring 3 Broad IT** and **Ring 4 Broad Business Users** groups. When you're finished, there should be three deployment ring groups.

Now that the groups have been created, add the computers to the computer groups that align with the desired deployment rings. You can do this through [Group Policy](#wsus-gp) or manually by using the [WSUS Administration Console](#wsus-admin).

<span id="wsus-admin"/>

## Use the WSUS Administration Console to populate deployment rings

Adding computers to computer groups in the WSUS Administration Console is simple, but it could take much longer than managing membership through Group Policy, especially if you have many computers to add. Adding computers to computer groups in the WSUS Administration Console is called *server-side targeting*.

In this example, you add computers to computer groups in two different ways: by manually assigning unassigned computers and by searching for multiple computers.

### Manually assign unassigned computers to groups

When new computers communicate with WSUS, they appear in the **Unassigned Computers** group. From there, you can use the following procedure to add computers to their correct groups. For these examples, you use two Windows 10 PCs (WIN10-PC1 and WIN10-PC2) to add to the computer groups.

**To assign computers manually**

1. In the WSUS Administration Console, go to *Server_Name*\Computers\All Computers\Unassigned Computers.

    Here, you see the new computers that have received the GPO you created in the previous section and started communicating with WSUS. This example has only two computers; depending on how broadly you deployed your policy, you'll likely have many computers here.

2. Select both computers, right-click the selection, and then select **Change Membership**.

    ![Select Change Membership in the UI.](images/waas-wsus-fig8.png)

3. In the **Set Computer Group Membership** dialog box, select the **Ring 2 Pilot Business Users** deployment ring, and then select **OK**.

    Because they were assigned to a group, the computers are no longer in the **Unassigned Computers** group. If you select the **Ring 2 Pilot Business Users** computer group, you'll see both computers there.

### Search for multiple computers to add to groups

Another way to add multiple computers to a deployment ring in the WSUS Administration Console is to use the search feature.

**To search for multiple computers**

1. In the WSUS Administration Console, go to *Server_Name*\Computers\All Computers, right-click **All Computers**, and then select **Search**.

2. In the search box, type **WIN10**.

3. In the search results, select the computers, right-click the selection, and then select **Change Membership**.

    ![Select Change Membership to search for multiple computers in the UI.](images/waas-wsus-fig9.png)

4. Select the **Ring 3 Broad IT** deployment ring, and then select **OK**.

You can now see these computers in the **Ring 3 Broad IT** computer group.


<span id="wsus-gp"/>

## Use Group Policy to populate deployment rings

The WSUS Administration Console provides a friendly interface from which you can manage Windows quality and feature updates. When you need to add many computers to their correct WSUS deployment ring, however, it can be time-consuming to do so manually in the WSUS Administration Console. For these cases, consider using Group Policy to target the correct computers, automatically adding them to the correct WSUS deployment ring based on an Active Directory security group. This process is called *client-side targeting*. Before enabling client-side targeting in Group Policy, you must configure WSUS to accept Group Policy computer assignment.

**To configure WSUS to allow client-side targeting from Group Policy**

1. Open the WSUS Administration Console, and go to *Server_Name*\Options, and then select **Computers**.

     ![Select Comptuers in the WSUS Administration Console.](images/waas-wsus-fig10.png)

2. In the **Computers** dialog box, select **Use Group Policy or registry settings on computers**, and then select **OK**.

    >[!NOTE]
    >This option is exclusively either-or. When you enable WSUS to use Group Policy for group assignment, you can no longer manually add computers through the WSUS Administration Console until you change the option back.

Now that WSUS is ready for client-side targeting, complete the following steps to use Group Policy to configure client-side targeting:

**To configure client-side targeting**

>[!TIP]
>When using client-side targeting, consider giving security groups the same names as your deployment rings. Doing so simplifies the policy-creation process and helps ensure that you don't add computers to the incorrect rings.

1. Open Group Policy Management Console (gpmc.msc).

2. Expand Forest\Domains\\*Your_Domain*.

3. Right-click *Your_Domain*, and then select **Create a GPO in this domain, and Link it here**.

4. In the **New GPO** dialog box, type **WSUS - Client Targeting - Ring 4 Broad Business Users** for the name of the new GPO.

5. Right-click the **WSUS - Client Targeting - Ring 4 Broad Business Users** GPO, and then select **Edit**.

    ![Select the WSUS ring 4 and edit in group policy.](images/waas-wsus-fig11.png)

6. In the Group Policy Management Editor, go to Computer Configuration\Policies\Administrative Templates\Windows Components\Windows Update.

7. Right-click **Enable client-side targeting**, and then select **Edit**.

8. In the **Enable client-side targeting** dialog box, select **Enable**.

9. In the **Target group name for this computer** box, type *Ring 4 Broad Business Users*. This is the name of the deployment ring in WSUS to which these computers will be added.

    ![Enter the WSUS deployment ring name.](images/waas-wsus-fig12.png)

> [!WARNING]
> The target group name must match the computer group name.

10. Close the Group Policy Management Editor.

Now you're ready to deploy this GPO to the correct computer security group for the **Ring 4 Broad Business Users** deployment ring.

**To scope the GPO to a group**

1. In GPMC, select the **WSUS - Client Targeting - Ring 4 Broad Business Users** policy.

2. Select the **Scope** tab.

3. Under **Security Filtering**, remove the default **AUTHENTICATED USERS** security group, and then add the **Ring 4 Broad Business Users** group.

    ![Remove the default AUTHENTICATED USERS security group in group policy.](images/waas-wsus-fig13.png)

The next time the clients in the **Ring 4 Broad Business Users** security group receive their computer policy and contact WSUS, they'll be added to the **Ring 4 Broad Business Users** deployment ring.

## Automatically approve and deploy feature updates

For clients that should have their feature updates approved as soon as they're available, you can configure Automatic Approval rules in WSUS.

>[!NOTE]
>WSUS respects the client device's servicing branch. If you approve a feature update while it's still in one branch, such as Insider Preview, WSUS will install the update only on devices that are in that servicing branch. When Microsoft releases the build for the [General Availability Channel](waas-overview.md#general-availability-channel), the devices in that will install it. Windows Update client policies branch settings don't apply to feature updates through WSUS.


**To configure an Automatic Approval rule for Windows client feature updates and approve them for the Ring 3 Broad IT deployment ring**
This example uses Windows 10, but the process is the same for Windows 11.

1. In the WSUS Administration Console, go to Update Services\\*Server_Name*\Options, and then select **Automatic Approvals**.

2. On the **Update Rules** tab, select **New Rule**.

3. In the **Add Rule** dialog box, select the **When an update is in a specific classification**, **When an update is in a specific product**, and **Set a deadline for the approval** check boxes.

     ![Select the update and deadline check boxes in the WSUS Administration Console.](images/waas-wsus-fig14.png)

4. In the **Edit the properties** area, select **any classification**. Clear everything except **Upgrades**, and then select **OK**.

5. In the **Edit the properties area**, select the **any product** link. Clear all check boxes except **Windows 10**, and then select **OK**.

    Windows 10 is under All Products\Microsoft\Windows.

6. In the **Edit the properties** area, select the **all computers** link. Clear all the computer group check boxes except **Ring 3 Broad IT**, and then select **OK**.

7. Leave the deadline set for **7 days after the approval at 3:00 AM**.

8. In the **Step 3: Specify a name** box, type **Windows 10 Upgrade Auto-approval for Ring 3 Broad IT**, and then select **OK**.

    ![Enter the ring 3 deployment name.](images/waas-wsus-fig15.png)

9. In the **Automatic Approvals** dialog box, select **OK**.

    >[!NOTE]
    >WSUS doesn't honor any existing month/week/day [deferral settings](waas-configure-wufb.md#configure-when-devices-receive-feature-updates). That said, if you're using Windows Update client policies for a computer for which WSUS is also managing updates, when WSUS approves the update, it will be installed on the computer regardless of whether you configured Group Policy to wait.

Now, whenever Windows client feature updates are published to WSUS, they'll automatically be approved for the **Ring 3 Broad IT** deployment ring with an installation deadline of 1 week.

> [!WARNING]
> The auto approval rule runs after synchronization occurs. This means that the *next* upgrade for each Windows client version will be approved. If you select **Run Rule**, all possible updates that meet the criteria will be approved, potentially including older updates that you don't actually want--which can be a problem when the download sizes are very large.

## Manually approve and deploy feature updates

You can manually approve updates and set deadlines for installation within the WSUS Administration Console, as well. It might be best to approve update rules manually after your pilot deployment has been updated.

To simplify the manual approval process, start by creating a software update view that contains only Windows 10 (in this example) updates. The process is the same for Windows 11 updates.

> [!NOTE]
> If you approve more than one feature update for a computer, an error can result with the client. Approve only one feature update per computer.

**To approve and deploy feature updates manually**

1.	 In the WSUS Administration Console, go to Update Services\\*Server_Name*\Updates. In the **Action** pane, select **New Update View**.

2. In the **Add Update View** dialog box, select **Updates are in a specific classification** and **Updates are for a specific product**.

3. Under **Step 2: Edit the properties**, select **any classification**. Clear all check boxes except **Upgrades**, and then select **OK**.

4. Under **Step 2: Edit the properties**, select **any product**. Clear all check boxes except **Windows 10**, and then select **OK**.

    Windows 10 is under All Products\Microsoft\Windows.

5. In the **Step 3: Specify a name** box, type **All Windows 10 Upgrades**, and then select **OK**.

     ![Enter All Windows 10 Upgrades for the name in the WSUS admin console.](images/waas-wsus-fig16.png)

Now that you have the **All Windows 10 Upgrades** view, complete the following steps to manually approve an update for the **Ring 4 Broad Business Users** deployment ring:

1. In the WSUS Administration Console, go to Update Services\\*Server_Name*\Updates\All Windows 10 Upgrades.

2. Right-click the feature update you want to deploy, and then select **Approve**.

      ![Approve the feature you want to deploy in WSUS admin console.](images/waas-wsus-fig17.png)

3. In the **Approve Updates** dialog box, from the **Ring 4 Broad Business Users** list, select **Approved for Install**.

      ![Select Approve for install in the WSUS admin console.](images/waas-wsus-fig18.png)

4. In the **Approve Updates** dialog box, from the **Ring 4 Broad Business Users** list, select **Deadline**, select **One Week**, and then select **OK**.

      ![Select a one week deadline in the WSUS admin console.](images/waas-wsus-fig19.png)

5. If the **Microsoft Software License Terms** dialog box opens, select **Accept**.

    If the deployment is successful, you should receive a successful progress report.

    ![A sample successful deployment.](images/waas-wsus-fig20.png)

6. In the **Approval Progress** dialog box, select **Close**.



