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
<h2>Actions and Observations</h2>

<p>
First go to Microsoft Azure and create a Resousre group to hold your VM's(Virtual Machines). For this lab I chose to use Canada Central for the region and named it Azure-VM-Lab. Then create those virtual machines under the same resource group, one running Windows 10 while the other runs Linux(Ubuntu 22-24). Make sure to chose a good size so the VM's do not run slow, since this is a lab practice use the same user and password for both VM's. For the Windows VM check the licensing box and for the Linux VM change the dot on SSH key to Password. For fun we will create a new subnet for these vm's which I named Azure-Lab.
  
  ![az1](https://github.com/user-attachments/assets/c337e60c-170a-45e8-989b-866e1cd3e266)
  ![az3](https://github.com/user-attachments/assets/ac4b553f-58ae-4e81-b628-5b5395ff0ae9)
  ![az4](https://github.com/user-attachments/assets/98ad793f-c983-41f0-b702-72c53f74aee0)
![az5](https://github.com/user-attachments/assets/fa81872f-567e-4dda-bacc-eedc0284e0c1)
![subnet fix](https://github.com/user-attachments/assets/5b13c858-3fe9-4439-bc84-2d2755aad109)
![az6](https://github.com/user-attachments/assets/6a07d349-b0bb-4a96-ae5c-a43b038e372f)
![az7](https://github.com/user-attachments/assets/9db869fd-49e6-438a-bd6a-af088fb07706)
 ![az8](https://github.com/user-attachments/assets/a9154785-0b45-48eb-a59b-c9055e3f2b5f)
![az9](https://github.com/user-attachments/assets/496f709b-85f3-4201-abef-cbf57771d1b6)
![subnet fix p2](https://github.com/user-attachments/assets/59cddb22-cca9-4d57-8fc7-4383e50ca377)

Now that we have set up our VM's lets log into one with Remote Desktop. Go to the Windows VM and copy and paste its IPv4 adress. THen sign in using the user and password we made earlier to sign into the VM. After signing in, install wire shark on the VM to capture the protocols in action.

![a12](https://github.com/user-attachments/assets/4aa4299b-69c8-4f96-becb-e24e72af03ca)
![az13a](https://github.com/user-attachments/assets/3ade5c5c-697e-46ed-b2b4-b19e830ee9d5)
![azurep](https://github.com/user-attachments/assets/09679b6a-1ace-4a42-9230-806c9b566096)
![az15](https://github.com/user-attachments/assets/b2c31d49-22d6-4c87-9bbc-19ac8a09e536)
![a16](https://github.com/user-attachments/assets/3b5c108f-0ccb-4218-82f8-d935080f1985)

Now that we have wireshark set up lets Try out a few protocols to understand how they work. THe first protocol we will use is ICMP this is also known as the ping protocol and doesnt have a port number, in the filter section at the top enter "icmp". To use ping open powershell and locate the Linux machines Private IP address. The ping should work since both virtual machines are in the same subnetwork. You can also ping other websites like Google.com.

![az18](https://github.com/user-attachments/assets/2ef620b8-7add-4222-a9f9-a837fbf48501)
![az19](https://github.com/user-attachments/assets/05379269-61e4-418f-9779-52263dac31ab)
![a20](https://github.com/user-attachments/assets/1afe8c5d-f125-4381-becb-52d94f0f7e6f)
![a21](https://github.com/user-attachments/assets/13af7f59-aae6-4e50-a0a6-8c7a8186b63f)


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
