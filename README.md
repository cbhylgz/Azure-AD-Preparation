<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure in Azure</h1>


<h2>Description</h2>
In this tutorial will show you how to Active Directory works through the use of two VMs (Virtual Machines), with one running a Windows server to be used as the DC (Domain Controller), and the other being the 'client' that joins said domain.
<br/>
<br />

<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Steps to Take:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group and virtual network. As you can see below, I have already made one (Active-Directory-Lab) and its virtual network, located within the resources (Active-Directory-VN): <br/>
<img src="https://i.imgur.com/h0szaMG.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/jf5GWl6.png" height="80%" alt="80%" alt="Setting Up in Azure"/>
<br />
<br />
Then, create and set up the virtual machine to play the role of Domain Controller. Choose Windows Server as the image, NOT Windows 10 Pro. When you get to the Networking tab, name the virtual network whatever you please while leaving everything else default:  <br/>
<img src="https://i.imgur.com/Mgr7gRs.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next up, make the second VM. This one will play the role of client. This time, the image for this machine should be Windows 10 Pro instead of Windows Server:  <br/>
<img src="https://i.imgur.com/dogP9JP.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Before you make this VM, make sure it's on the same virtual network as the first:  <br/>
<img src="https://i.imgur.com/pIpsLCb.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now, set the DC (Domain Controller) private IP address from "static" to "dynamic". The reason for this is because the DC will double as a DNS (Domain Name System) server that the client will make use of. Leaving the IP allocation setting dynamic may cause the IP address to change.  <br/>
<img src="https://i.imgur.com/AWU2FQN.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/XCAWb6X.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, open the Remote Desktop Connection window to connect to the DC using its public IP and username/password made when making the VM. Once connected, you should see a screen like this: <br/>
<img src="https://i.imgur.com/haya0ms.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Disable the firewall. A quick way to do this would be to right click on the "Start" button and select "Run", and type "wf.msc" in the search bar. DISCLAIMER: Doing this in a real life IT setting is not advised. This is simply for demonstratory purposes.  <br/>
<img src="https://i.imgur.com/vRynwZF.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Click on "Windows Defender Firewall Properties", then on the "Domain Profile", "Private Profile, and "Public Profile" tabs, turn the firewall state off:  <br/>
<img src="https://i.imgur.com/TK0aFlG.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/PuBHPeK.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/KAFlXri.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now, configure our client's DNS settings to the DC. To do this, identify and copy the DC's private IP address:  <br/>
<img src="https://i.imgur.com/X6LJPdX.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Go to the network setting of the client machine, click on the NIC (Network Interface Card), go to settings, then DNS servers and switch from "Inherit from virtual network" to "Custom". Input the DCs private IP here and save:  <br/>
<img src="https://i.imgur.com/l0Q8BWh.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Restart the client machine afterwards:  <br/>
<img src="https://i.imgur.com/Dh5fBbm.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After it's done restarting, use Remote Desktop Connection to connect to the client VM using its public IP and username/password. Then, open Powershell within the client VM and ping the DC using the ping command and its private IP address: <br/>
<img src="https://i.imgur.com/LUt8CRg.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
You can also run a prompt to see if the DNS server settings are connected to the DC. Run "ipconfig /all" in PowerShell. The "DNS Servers" category should contain the private IP of our DC:  <br/>
<img src="https://i.imgur.com/F8R6QMU.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />

<h2>Preparation Completed! </h2>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
