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

<h1>ICMP</h1>

  Now that we have wireshark set up lets Try out a few protocols to understand how they work. THe first protocol we will use is ICMP this is also known as the ping protocol and doesnt have a port number, in the filter section at the top enter "icmp". To use ping open powershell and locate the Linux machines Private IP address. The ping should work since both virtual machines are in the same subnetwork. You can also ping other websites like Google.com.
  
  Lets try stopping a constant ping to the Linux machine, go into powershell and use the ping command but this time  add "-t". This command will give a constant ping untill told otherwise, we are going to set up a basic firewall. On your main device go into the Linux virtual machine settings find the network tab open network settings and create a port rule. In this port rule change the setting to ICMPv4 notice how the port ranges changes to a *. this happens because ICMP does not use a port. Change the setting from allow to deny and the priority to 290 so the VM knows to run it first. Check back into Powershell and notice how after a while the ping protocol starts to time out. To change the this back go back into your VM and delete the fire wall and notice how after a while it comes back, to stop the constant ping hit Ctrl+C.

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

<h1>SSH</h1>

Next we are going to use SSH. SSH uses port 22 to connect securly to another devices while aslo staying encrypted. Make sure to change your filter from icmp to ssh. when you try to use ssh in powershell it will ask you for the password that we made earlier to sign into the VM. It wont show for security purposes but once you are logged in it should turn green. You can move files, manage servers, and run commands. a few commands I ran to test this out was host name,who am i, and uptime. if you look closely all the information that is givin is congruent to what we set up earlier. Notice the amount of traffic there is in wireshark ever key typed is encrypted and sent to the Linux machine, To log out enter exit.

![a28](https://github.com/user-attachments/assets/0b78b5b6-4af4-465f-93f0-be1c619e605d)
![az29](https://github.com/user-attachments/assets/5922afc8-ad9a-451e-86e4-4850382d33a7)

<h1>DNS</h1>

Next we are going to look at DNS traffic. DNS uses port 53. In simple terms Dns translates human websites into ip addresses so the computer can read it and understand where to go. For this example change the filter in wireshark to dns, then go into powershell and us nslookup and a site of your choice I chose marvel.com. If you look you can see the vm translating with marvels public ip address to find the correct server.

![a30](https://github.com/user-attachments/assets/cc0a88e8-dd25-429b-999e-93de0a6c8b6a)

<h1>RDP/TCP Port 3389</h1>

Next we are going to show the use of tcp port 3389 also known as RDP. Powershell isnt needed for this example because we are currently using RDP for the lab. If you look at wireshark there should be constant feedback.
![a31](https://github.com/user-attachments/assets/0e2ca87e-604a-4619-a2a1-e5d5081e7072)

<h1>HTTP</h1>

For our final protocol we will use http also know as tcp port 80. I already had a browser open and this protocol also showed instant feedback. When in a browser it uses HTTP in the background for automatic updates and when you search thing in the browser aswell.
![a32](https://github.com/user-attachments/assets/0122ce2c-7ec9-48bb-854d-d60433bb434e)

<h1>Clean up</h1>

Now that we are finished with the VM's we can shut them down. Head back to azure and go into your resource group. Go to delete and make sure everything in the resource group is deleted. Refresh and make sure everything was properly deleted.
![atlastz](https://github.com/user-attachments/assets/11da332f-e0f7-44c1-b62f-482684acaf38)
![azure](https://github.com/user-attachments/assets/c8e3d50c-7523-4aa5-abb2-775d1472f6f2)

