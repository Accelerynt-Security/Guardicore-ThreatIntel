# Integrating Latest Guardicore Threat Intelligence into Azure tiIndicator

Author: Arbala Security

For any technical questions, please contact info@arbalasystems.com.

This playbook will pull the domain names and IPs from the threat intelligence that Guardicore shares every Sunday. It will create Azure Sentinel Threat Intelligence Indicators with the information by posting to the tiIndicators collection.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FArbala-Security%2FGuardicore-ThreatIntel%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="https://aka.ms/deploytoazurebutton""/>
</a>
  
 # 
Open your browser and ensure you are logged into your Azure Sentinel workspace. In separate tab, open the link to our playbook on the Arbala Security GitHub Repository:

https://github.com/Arbala-Security/Guardicore-ThreatIntel

From there, click the “Deploy to Azure” button at the bottom and it will bring you to the Custom Deployment Template.

![Deploy](Images/)

In the **BASICS** section:  

* Select the “**Subscription**” and “**Resource Group**” from the dropdown boxes you would like the playbook deployed to.  

In the **SETTINGS** section:   

* **Playbook Name**: This can be left as “Guardicore-ThreatIntel” or you may change it.  

Towards the bottom ensure you check the box accepting the terms and conditions and then click on “Purchase”. 

![template](Images/template.png)

The playbook should take less than a minute to deploy. Return to your Azure Sentinel workspace and click on “Playbooks.” Next, click on your newly deployed playbook. Don’t be alarmed to see that the status of the playbook shows failed. We still need to edit the playbook to set up a valid connection on our Microsoft Graph Security connectors.  

![playbookclick](Images/)

Click on the “Edit” button. This will bring us into the Logic Apps Designer.

![editbutton](Images/)

Click on the bottom left bar labeled “For Each - GC Data: Malicious Domains 1”. 

![Logicapp1](Images/)

Click on the bar labeled “Condition - Check Valid Data 1”. 

![Logicapp2](Images/)

Click on “Connections”.  

![Logicapp3](Images/)

Click on the circled exclamation point under the word "Invalid". 

![Logicapp4](Images/)

This will prompt you to sign in with your credntials.

![Logicapp5](Images/)

You should see the that the “Create tiIndicator 2” box has updated and displays “Connected to GCTI.”

![Logicapp6](Images/)

You will need to repeat this process for the right hand branch. 

The branching for the same outer loops is necessary because not all Guardicore domains and ips are in a format Microsoft Graph will accept as valid. 
The branching allows a domain name and it's associated ips to be ingested separately.
This way, an invalid domain name will not negate its associated valid ip addresses, or vice versa.

Collapse the bar labled “For Each - GC Data: Malicious Domains 1” that you previously expanded. 

Click on the bottom right bar labeled “For Each - GC Data: Malicious Domains 2”. 

![](Images/)

Click on the bar labeled “Condition - Check Valid Data 2”. 

![](Images/)

Click on the bottom right bar labeled “For Each - GC Data: Malicious Domains IPs”. 

![](Images/)

Click on “Connections”.  

![](Images/)

Click on the circled exclamation point under the word "Invalid". 

![](Images/)

You should not need to enter your credentials a second time.

You should see the that the “Create tiIndicator” box has updated and displays “Connected to GCTI.” Click the X to close the Logic App Designer. There is no need to click a save button.  

For any technical questions, please contact info@arbalasystems.com.

