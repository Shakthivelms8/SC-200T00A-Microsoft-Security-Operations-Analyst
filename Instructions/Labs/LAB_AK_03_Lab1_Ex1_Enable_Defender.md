---
lab:
    title: 'Exercise 1 - Enable Microsoft Defender for Cloud'
    module: 'Learning Path 3 - Mitigate threats using Microsoft Defender for Cloud'
---

# Learning Path 3 - Lab 1 - Exercise 1 - Enable Microsoft Defender for Cloud

## Lab scenario

![Lab overview.](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing cloud workload protection with Microsoft Defender for Cloud.  In this lab you will enable Microsoft Defender for Cloud.


### Task 1: Access the Azure portal and set up a Subscription

In this task, you will set up an Azure Subscription required to complete this lab and future labs.

1. Log in to **WIN1** virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the Microsoft Edge browser or open a new tab if already open.

1. In the Edge browser, navigate to the Azure portal at (https://portal.azure.com).

1. In the **Sign in** dialog box, copy, and paste in the tenant Email account for the admin username provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy, and paste in the admin's tenant password provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Subscription*, then select **Subscriptions**. 

1. If the *"Azure Pass - Sponsorship"* subscription is shown (or equivalent name in your selected language), proceed to Task #2. Otherwise, ask your instructor on how to create the Azure subscription with your tenant admin user credentials. **Note:** The subscription creation process could take up to 10 minutes. 

    >**Important:** These labs have been designed to use less than USD $10 of Azure services during the class.


### Task 2: Create a Log Analytics Workspace

In this task, you will create a Log Analytics workspace for use with Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type *Log Analytics workspaces*, then select the same service name.

1. Select **+Create** from the command bar.

1. Select **Create new** for the Resource group.

1. Enter *RG-Defender* and select **Ok**.

1. For the Name, enter something unique like: *uniquenameDefender*.

1. Select **Review + Create**.

1. Once the workspace validation has passed, select **Create**. Wait for the new workspace to be provisioned, this may take a few minutes.


### Task 3: Enable Microsoft Defender for Cloud

In this task, you will enable and configure Microsoft Defender for Cloud.

1. In the Search bar of the Azure portal, type *Defender*, then select **Microsoft Defender for Cloud**.

1. On the **Getting started** page, under the **Upgrade** tab, make sure your subscription is selected, and then select the **Upgrade** button at the bottom of the page. Wait for the *Trial started* notification to appear, it takes about 2 minutes. **Hint:** You can click the bell button on the top bar to review your Azure portal notifications.

1. In the left menu for Microsoft Defender for Cloud, under the Management, select **Environment settings**.

1. Select the **"Azure Pass - Sponsorship"** subscription (or equivalent name in your Language). 

1. Review the Azure resources that are now protected with the Defender for Cloud plans.

1. Select the **Settings & monitoring** tab from the Settings area (next to Save).

1. Review the monitoring extensions. Confirm that **Log Analytics agent/Azure Monitor agent** is **Off**. Close the Settings & monitoring page by selecting the 'X' on the upper right of the page.

1. Close the settings page by selecting the 'X' on the upper right of the page to go back to the **Environment settings** and select the '>' to the left of your subscription.

1. Select the Log analytics workspace you created earlier *uniquenameDefender* to review the available options and pricing.

1. Select **Enable all** (to the right of Select Defender plan) and then select **Save**. Wait for the *"Microsoft Defender plan for workspace uniquenameDefender were saved successfully!"* notification to appear.

    >**Note:** If the page is not being displayed, refresh your Edge browser and try again.

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**

### Task 4: Install Azure Arc on an On-Premises Server

In this task, you will install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to **WINServer** virtual machine as Administrator with the password: **Passw0rd!** if required.  

1. Open the Microsoft Edge browser and navigate to the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Arc*, then select **Azure Arc**.

1. In the navigation pane under **Infrastructure** select **Servers**

1. Select **+ Add**.

1. Select **Generate script** in the "Add a single server" section.

1. Select **Next** to get to the Resource details tab.

1. Select the Resource group you created earlier. **Hint:** *RG-Defender*
1. Select the Region **East US** 

    >**Note:** If you haven't already created a resource group, open another tab and create the resource group and start over.

1. Review the *Server details* and *Connectivity method* options. Keep the default values and select **Next** to get to the Tags tab.

1. Select **Next** to get to the Download and run script tab.

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select **Keep**. 

1. Right-click the Windows Start button and select **Windows PowerShell (Admin)**.

1. Enter *Administrator* for "Username" and *Passw0rd!* for "Password" if you get a UAC prompt.

1. Enter: cd C:\Users\Administrator\Downloads

    >**Important:** If you do not have this directory, most likely means that you are in the wrong machine. Go back to the beginning of Task 4 and change to WINServer and start over.

1. Type *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* and press enter.

1. Enter **A** for Yes to All and press enter.

1. Type *.\OnboardingScript.ps1* and press enter.  

    >**Important:** If you get the error *"The term .\OnboardingScript.ps1 is not recognized..."*, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for *".\OnboardingScript (1).ps1"* or other file numbers in the running directory.

1. Enter **R** to Run once and press enter (this may take a couple minutes).

1. The setup process will open a new Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message "Authentication complete" and then go back to the Windows PowerShell window.

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Servers** page.

1. Select **Refresh** until WINServer server name appears and the Status is *Connected*.

    >**Note:** This could take a couple of minutes.

### Task 5: Protect an On-Premises Server

In this task, you will manually install the required agent on the **WINServer** virtual machine.

1. Go to **Microsoft Defender for Cloud** and select the **Getting Started** page.

1. Select the **Get Started** tab.

1. Scroll down and select **Configure** under the *Add non-Azure servers* section.

1. Select **Upgrade** next to the workspace you created earlier. This might take a few minutes, wait until you see the notification *"Azure Defender plan for workspace uniquenameDefender were saved successfully!"*.

1. Select **+ Add Servers** next to the workspace you created earlier.

1. Select **Log Analytics agent instructions**

1. Select **Download Windows Agent (64 bit)**.

1. Select **Open file** to run the downloaded *MMASetup-AMD64.exe* file.

1. Select **Next** until the wizard page for **Agent Setup Options** appears; select **Connect the Agent to Azure Log Analytics (OMS)**, then select **Next**.

1. Copy and paste the **Workspace ID** and **Primary Key** value in the **Workspace Key** text box from the Azure portal into the wizard page fields as appropriate and select **Next**.

1. Continue with the Install. Select **Finish** when complete.

1. Go to the "Microsoft Defender for Cloud" portal and select **Inventory**.

1. The **WINServer** virtual machine will appear after at least 5 minutes. You may have to select **Refresh** to see it. **Hint:** If you see the number 1 under *Total resources* remove the filter to show the *WINServer* virtual machine.

1. You can move on to the next lab and return later to review the **Inventory** section of **Microsoft Defender for Cloud**.

## Proceed to Exercise 2
