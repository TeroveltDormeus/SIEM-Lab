<h1>RDP Attack Monitoring with Azure Sentinel</h1>

Monitored and detected Remote Desktop Protocol (RDP) attack attempts using Microsoft Azure Sentinel. 
<h2>🛠️ Part 1: Create a Honeypot VM in Azure</h2>
<h3>Step 1: Log in and Create the VM</h3>

- Log into the Azure Portal
- Go to Virtual Machines > + Create > Azure virtual machine
- Use a basic name like HoneypotVM, choose a region close to you, and select: Windows 10 Pro Image, Standard B1s should be enough


<h4>Under Inbound port rules, allow:</h4>

- Under Inbound port rules, allow: RDP 3389


  <img src="https://i.imgur.com/2brp24P.png">

<h2>🔐 Part 2: Connect to Microsoft Sentinel</h2>
<h3>Step 1: Set Up Microsoft Sentinel</h3>


- Go to Microsoft Sentinel > + Add and attach it to a Log Analytics workspace
- In the workspace:
- Go to Data Connectors
- For Windows, enable Windows Security Events


<img src="https://i.imgur.com/J3A2sCy.png">


<h3>Step 2: Forward Logs from the Honeypot</h3>


- For Windows: Use the Microsoft Monitoring Agent:
- Download it from Sentinel’s connector page
- Install, enter workspace ID and key
- Ensure Windows logs (Security, Application) are being collected
  

<h2>📊 Part 3: Visualize Alerts in a Graph</h2>
<h3>Step 1: Query Logs in Sentinel</h3>

Go to Logs in your Sentinel workspace. Run a KQL (Kusto Query Language) query like:
<p/>
SecurityEvent
| where Activity contains "success" and Account contains "system"

<p/>
<img src="https://i.imgur.com/ZJm3Ggo.png">

After a couple of hours, I checked my events within Microsoft Sentinel and we got 315 RDP login alerts.
<p/>
<img src="https://i.imgur.com/VqDorfB.png">





