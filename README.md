<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 - Create Azure Resources:
  1. Resource Groups

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/07fee134-b253-48b2-8550-11ec9b9c2dcb)

  2. Azure Virtual Networks and Subnets (automatically made for you)
 
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/9377aa00-4c54-4b49-a25e-72d480a872b9)
  
  3. Azure Virtual Machines (Windows and Linux (Ubuntu))
  
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/035130a3-bc49-46e1-9054-a803b568b3da) 
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/d8447394-7f1f-4deb-9c44-ae0c922850a8)
 
  
  4. Azure Network Security Groups (Firewall Resource)

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/1bcda21a-e872-4080-8cea-3ba3b13895f7)

- Step 2 - Login into VM1 using Remote Desktop (Windows Machine)
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/08b61e71-a3ad-4ebe-b5b2-72f1a93ca773)

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/35eb51e8-b8d9-43e0-8f23-113e37636726)

- Step 3 - Install and download Wireshark on Virtual Maching (VM1)
   1. Google "download wireshark", click Windows Installer (64bit)
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/c4b70b1d-8819-4a6b-9131-1905a83abbdc)

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/1d9475b9-6c6e-4172-ab14-11fa03ebbeab)

- Step 4 - Open Wireshark
  1. Select Ethernet Adapter and click blue shark fin to start capturing packets

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/c9cf9d7f-08e3-473f-b6d8-f9a1afec8de4)

- Step 5 - Apply Filter by typing ICMP in search bar

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/4e4ffe60-d71d-412f-a875-9db980abb6bc)

   1. Find Private IP address in Azure
 
![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/d9154a84-5955-4d6f-aaf2-20f3d6d3957b)
 
  2. Open Windows Powershell and ping VM2 with the private IP address and observe traffic in Wireshark as a result

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/52b82fa1-d45e-4ffe-a838-70bebbf317e6)

- Step 6 - Initiate a perpetual (nonstop) ping from VM1 to VM2

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/e2e19b7e-8276-440a-87d7-a688701fa080)

- Step 7 - Go to VM2 in Azure and block ICMP traffic in the Virtual Firewall
  1. Search Network Security Group

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/bbec4e36-f429-43d1-ab42-ddc2978a9b0b)

  2. Select VM2 -> Select Inbound Security Rules -> Add new rule -> Deny ICMP

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/c613f36e-9a3b-4017-ab8c-b07093f4ea2e)

- Step 8 - Go back to VM1 to view the results ex: request timed out

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/bd7cc714-378a-4b52-9394-08a60b11a9b7)

- Step 9 - Go back to Deny ICMP rule we just created and change it Allow

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/25502138-55ac-4b79-b172-22e9f2d35c64)

  1. Go back to VM1 to view the results ex: Reply from..

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/094ac039-2acc-4ffc-b91b-2870fe501f9b)

- Step 10 - Type in SSH in search bar to filter traffic in Wireshark

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/fb335be2-1491-4451-994d-740d89d05b92)

  1. Connect to VM2 through SSH (SecureShell) in Windows Powershell on VM1 by typing ssh username then "@", then private ip address of VM2, then the password when prompted (it wont show you the keystrokes for security)

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/0eb7134e-069e-44d3-9557-2fc29a93d65e)

- Step 11 - Create a new file by typing touch hi.txt in Windows Powershell and observe the traffic created

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/dd4538a9-2326-4e04-b256-f664b29cc55b)

  2. Type exit to get back to VM1 shell

![image](https://github.com/WesGough/azure-network-protocols/assets/150361198/513b51f7-9a57-43dd-8db4-f573df119d0e)

You can play around on your own typing in different commands in the command shell or filter by different ports in Wireshark and see the results! Have fun!
