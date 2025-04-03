<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this lab I use Azure to create 2 separate virtual machines to test various protocols between them to understand how networking works between 2 computers. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH/RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04
<h2>Virtual Machine Setup</h2>

<p>
First, go to Microsoft Azure and create a Resource Group to hold your VMs (Virtual Machines). For this lab, I chose Canada Central as the region and named it Azure-VM-Lab.

---

![az1](https://github.com/user-attachments/assets/c337e60c-170a-45e8-989b-866e1cd3e266)

  ---

Next, create two virtual machines under the same Resource Group—one running Windows 10 and the other running Linux (Ubuntu 22-24).

For the Windows VM, check the licensing box, and for the Linux VM, change the authentication method from SSH key to Password.

Make sure to choose a good size so the VMs do not run slowly. 

Since this is a lab practice, use the same username and password for both VMs.

---

  ![az3](https://github.com/user-attachments/assets/ac4b553f-58ae-4e81-b628-5b5395ff0ae9) 
 ![az4](https://github.com/user-attachments/assets/98ad793f-c983-41f0-b702-72c53f74aee0)
  ![az7](https://github.com/user-attachments/assets/9db869fd-49e6-438a-bd6a-af088fb07706)  
 ![az8](https://github.com/user-attachments/assets/a9154785-0b45-48eb-a59b-c9055e3f2b5f)
  ![az5](https://github.com/user-attachments/assets/fa81872f-567e-4dda-bacc-eedc0284e0c1)
  ![az6](https://github.com/user-attachments/assets/6a07d349-b0bb-4a96-ae5c-a43b038e372f)
![az9](https://github.com/user-attachments/assets/496f709b-85f3-4201-abef-cbf57771d1b6)
  
---

For fun, we will create a new subnet for these VMs, which I named Azure-Lab.

---
 ![subnet fix](https://github.com/user-attachments/assets/5b13c858-3fe9-4439-bc84-2d2755aad109)
![subnet fix p2](https://github.com/user-attachments/assets/59cddb22-cca9-4d57-8fc7-4383e50ca377)

---

Now that we have set up our VMs, let’s log into one using Remote Desktop.

---

![a12](https://github.com/user-attachments/assets/4aa4299b-69c8-4f96-becb-e24e72af03ca)

---

Go to the Windows VM and copy its IPv4 address. 

Then, use the username and password we created earlier to sign into the VM.

---

![az13a](https://github.com/user-attachments/assets/3ade5c5c-697e-46ed-b2b4-b19e830ee9d5)

---

After signing in, install Wireshark on the VM to capture network protocols in action.

---

![azurep](https://github.com/user-attachments/assets/09679b6a-1ace-4a42-9230-806c9b566096)
![az15](https://github.com/user-attachments/assets/b2c31d49-22d6-4c87-9bbc-19ac8a09e536)
![a16](https://github.com/user-attachments/assets/3b5c108f-0ccb-4218-82f8-d935080f1985)

---

<h1>ICMP</h1>

Now that we have Wireshark set up, let’s try out a few protocols to understand how they work.

The first protocol we will use is ICMP, also known as the ping protocol. ICMP does not have a port number. In Wireshark, enter “icmp” in the filter section at the top.

To use ping, open PowerShell and locate the Linux machine’s private IP address. The ping should work since both virtual machines are in the same subnet. You can also ping other websites like Google.com.

Stopping a Constant Ping

Now, let’s try stopping a constant ping to the Linux machine. Open PowerShell and use the ping command, but this time, add ”-t” at the end. This command will send a continuous ping until manually stopped.

Next, we are going to set up a basic firewall. On your main device, go to the Linux virtual machine settings, find the network tab, open network settings, and create a port rule.

In this port rule:
	•	Change the setting to ICMPv4 (notice how the port range changes to ”*”—this happens because ICMP does not use a port).
	•	Change the rule action from Allow to Deny.
	•	Set the priority to 290 so the VM knows to apply this rule first.

Now, check PowerShell again. After a short time, the ping requests will begin to time out, indicating that the firewall rule is working.

To revert this change, go back into your VM, delete the firewall rule, and notice how the ping starts working again after a while. To stop the constant ping, press Ctrl + C.

---

  ![az18](https://github.com/user-attachments/assets/2ef620b8-7add-4222-a9f9-a837fbf48501)
![az19](https://github.com/user-attachments/assets/05379269-61e4-418f-9779-52263dac31ab)
![a20](https://github.com/user-attachments/assets/1afe8c5d-f125-4381-becb-52d94f0f7e6f)
![a21](https://github.com/user-attachments/assets/13af7f59-aae6-4e50-a0a6-8c7a8186b63f)
![az22](https://github.com/user-attachments/assets/86414e7d-f156-4628-a8f0-5a5098b6b86d)
![az23](https://github.com/user-attachments/assets/7a430916-cde4-42f5-9c0c-807742af5557)
![az24](https://github.com/user-attachments/assets/719c95d4-1f52-44a8-89b7-0ce91aa75c70)
![a25m](https://github.com/user-attachments/assets/0d992c6c-90c3-42ef-8d0f-3bce3f504733)
![a25](https://github.com/user-attachments/assets/90590901-22e8-45a6-835a-71df746beaa2)
![az23m2](https://github.com/user-attachments/assets/75218d96-51c4-404d-b142-406bfc97052c)
![a26](https://github.com/user-attachments/assets/ffdbe26d-9f7f-4a6b-85d7-2e3b1ec8c6e7)
![a27](https://github.com/user-attachments/assets/02d561aa-4a00-4384-8b3b-fcafcb53b331)

---

<h1>SSH</h1>

Next, we are going to use SSH. SSH uses port 22 to securely connect to another device while keeping the connection encrypted.

First, change your Wireshark filter from ICMP to SSH.

When you try to use SSH in PowerShell, it will prompt you for the password we created earlier to sign into the Linux VM. The password won’t be visible for security purposes, but once you are logged in, the terminal should turn green.

With SSH, you can move files, manage servers, and run commands. A few commands I ran to test this out were:
	•	hostname – Displays the name of the machine.
	•	whoami – Shows the currently logged-in user.
	•	uptime – Displays how long the system has been running.

If you look closely, all the information displayed matches what we set up earlier.

Also, take note of the amount of traffic in Wireshark—every keystroke is encrypted and sent to the Linux machine.

To log out, enter “exit”.

---

![a28](https://github.com/user-attachments/assets/0b78b5b6-4af4-465f-93f0-be1c619e605d)
![az29](https://github.com/user-attachments/assets/5922afc8-ad9a-451e-86e4-4850382d33a7)

---

<h1>DNS</h1>

Next, we are going to examine DNS traffic. DNS uses port 53 and, in simple terms, translates human-readable website names into IP addresses so that computers can understand where to go.

For this example, change the Wireshark filter to DNS, then open PowerShell and use the nslookup command followed by a website of your choice. I chose marvel.com.

If you look at the Wireshark capture, you can see the VM querying Marvel’s public IP address to find the correct server.

---

![a30](https://github.com/user-attachments/assets/cc0a88e8-dd25-429b-999e-93de0a6c8b6a)

---

<h1>RDP/TCP Port 3389</h1>

Next, we are going to look at the use of TCP port 3389, also known as RDP (Remote Desktop Protocol). PowerShell isn’t needed for this example because we are currently using RDP for the lab.

If you look at Wireshark, you should see constant feedback as RDP traffic is being exchanged between the client and the server.

---

![a31](https://github.com/user-attachments/assets/0e2ca87e-604a-4619-a2a1-e5d5081e7072)

---

<h1>HTTP</h1>
For our final protocol, we will use HTTP, which runs over TCP port 80. HTTP is the protocol used by web browsers to communicate with web servers and load websites. When you access a webpage, your browser sends HTTP requests to the server to retrieve content such as text, images, and other resources. This protocol also shows instant feedback in Wireshark.

In addition to loading pages, HTTP is used for background tasks like submitting search queries and fetching resources such as scripts and stylesheets. It also plays a role in automatic updates, with the browser continuously using HTTP to request new content, like when you search in the browser. While HTTP is commonly used, HTTPS (port 443) is often used for secure communication.

---

![a32](https://github.com/user-attachments/assets/0122ce2c-7ec9-48bb-854d-d60433bb434e)

---

<h1>Clean up</h1>
Now that we are finished with the VMs, we can shut them down. Head back to Azure and go into your Resource Group. Click on Delete and make sure everything in the resource group is deleted. Refresh the page to ensure everything was properly deleted.

---

![atlastz](https://github.com/user-attachments/assets/11da332f-e0f7-44c1-b62f-482684acaf38)
![azure](https://github.com/user-attachments/assets/c8e3d50c-7523-4aa5-abb2-775d1472f6f2)

---
