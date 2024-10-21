<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Preparing Active Directory Infrastructure in Azure</h1>


<h2>Description</h2>
In this project, I set up two virtual machines (VMs): one running Windows Server to function as a Domain Controller, and the other as a client, running Windows 10, which will join the domain. In future projects, I will deploy Active Directory, execute a script to create users in the domain (allowing me to log in from the client VM), and manage the accounts and update group policies, all to simulate a real-world IT environment.  <br/>
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walk-through:</h2>

<p align="center">
Go to Microsoft Azure and create a resource group: <br/>

![image](https://github.com/user-attachments/assets/d2e51487-03a0-4397-8260-ff68d76d4562)

Next is to create a virtual network : <br/>

![image](https://github.com/user-attachments/assets/885fb59e-1f3c-4d1d-97ef-35a312470216)



After creating the resource group and network, I’ll set up the virtual machine that will serve as the Domain Controller. Be sure to select Windows Server for the image.<br/>

![image](https://github.com/user-attachments/assets/53818eda-9fee-4c9b-b0c2-8b0218218a3f)


 In the Networking tab of the VM setup, ensure it is configured to connect to the virtual network you just created. Leave all other settings as default, then proceed to create the VM. br/>



![image](https://github.com/user-attachments/assets/2d8b6df8-9071-48c8-b8b0-9be3ab990ad6)



Next, create another VM to serve as the client. For this machine, select a Windows 10 image, not Windows Server as you did for the previous VM.<br/>


![image](https://github.com/user-attachments/assets/ab7b425b-1f98-44e3-bd30-b49392abbd60)



![image](https://github.com/user-attachments/assets/3b23650f-128e-4680-a24c-44264a45a468)





 In the Networking tab of this VM, ensure it connects to the same virtual network as the previously created machine. Leave the remaining settings as default and create the VM. br/>


![image](https://github.com/user-attachments/assets/d24490c8-3fe1-47b7-bc43-0b60ef98b794)


Now, you need to change the Domain Controller's (DC) private IP address from its default "dynamic" setting to "static." This is necessary because the DC will also function as a DNS (Domain Name System) server, which you'll later configure the client to use. If the IP allocation remains dynamic, the IP address could change, making the DNS settings on the client invalid. To prevent this, go to the network settings of the DC and set the IP allocation to static.<br/>

![image](https://github.com/user-attachments/assets/4252fd45-b559-4192-a98a-eca8d43130e7)




![image](https://github.com/user-attachments/assets/d19cdc8a-92d5-46ce-b14c-961f38e04e60)




Next, use Remote Desktop Connection or Windows App on Mac to connect to the Domain Controller (DC) by entering its public IP address and the login credentials you created during the machine's setup.<br/>


![image](https://github.com/user-attachments/assets/78037840-d4d9-4bc4-a474-a4438c9bbf7a)





Once logged in, you should see the Server Manager open on the screen. If you're seeing a regular Windows desktop instead, you might have connected to the client VM by mistake or selected the wrong image when creating the Domain Controller. <br/>



![image](https://github.com/user-attachments/assets/9d12df68-6b57-4b58-a752-cea031674eb3)





Next, you'll disable the firewall (while this isn't something you'd typically do in a real-world scenario, it's fine for this lab since there's no risk involved). To disable the firewall, right-click the Start button, select Run, and type "wf.msc."<br/>




![image](https://github.com/user-attachments/assets/4beeea7d-6dc2-40f5-8789-d1f7a64fb3c5)




Click on Windows Defender Firewall Properties, then select the Domain Profile, Private Profile, and Public Profile tabs to turn off the firewall state for each. <br/>




![image](https://github.com/user-attachments/assets/73e7d278-31cf-45a0-8053-1e4dd83267fa)




You should see that all the firewall settings are disable:  <br/>



![image](https://github.com/user-attachments/assets/76720272-f9c1-4893-8cef-b8ff7db47932)


Next, you need to configure the client's DNS settings to point to the Domain Controller (DC). To begin, go back to Azure and retrieve the DC's private IP address.<br/>


![image](https://github.com/user-attachments/assets/049c2255-3f25-43a3-9dc5-143db7c115c1)


Then, navigate to the network settings of the client machine. Click on the NIC (Network Interface Card), go to Settings, then DNS servers, and change the option from Inherit from virtual network to Custom. Enter the DC's private IP address here and save the changes. <br/>


![image](https://github.com/user-attachments/assets/6998096d-e48a-40f9-8cc9-2a2f03317d4f)



After that's saved, restart the client machine:  <br/>





![image](https://github.com/user-attachments/assets/35e4c24e-2d4e-45f4-8eaa-e13e0433a3e6)





<h2>Active Directory Infrastructure is Now Prepared! </h2>

