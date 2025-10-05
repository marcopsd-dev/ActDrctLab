<h1>Active Directory Cloud-Based Lab</h1>


<h2>Description</h2>
This is a step to step turorial on how to sep up Active Directroy in a cloud-based environment to simulate a real enterprise network environment using AWS, PowerShell, MacOS, and the RDP protocol.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b>
- <b>AWS Private Clouds</b>
- <b>DHCP Server</b>
- <b>NAT Routing<b>
- <b>Active Directory Domain Setup<b>
- <b>AWS EC2</b>
- <b>AWS Route 53<b>
- <b>Windows Server Management<b>
- <b>Windows App/Parallels Desktop</b>

<h2>Environments Used </h2>

- <b>MacOS Seqouia 15.6.1</b> 
- <b>AWS</b>
  
<h2>Program walk-through:</h2>

<h3 align="center">Creating a VPC in AWS:</h3> <br/>
  <p aling="left">
  <b>1. Go to the AWS console and type in VPC on the searchbar.</b><br>
  <b>2. Once in the VPC dashboard you'll click on "Create VPC".</b>
  <img src="https://i.imgur.com/aGzRHDU.png" height="80%" width="80%" alt="AWS VPC"/>
  <br /><br>
  <b>3.Select "VPC and more" to create a custom VPC. This will allow us to create 1 private subnet for the windows client, and 1 public subnet for the internet facing server. </b><br>
  <img src="https://i.imgur.com/IO19JWY.png" height="80%" width="80%" alt="AWS VPC"/><br>
  <br>
  <b>4. Depending on the size of the lab that you want to create, you can add more AZ's to implement a more complex network with multiple   servers and/or clients. For this lab I'll only create 2 AZ's. Finally click on "Create VPC" at the bottom of the page. </b>
  <img src="https://i.imgur.com/PQyN2K7.png" height="80%" width="80%" alt="AWS VPC"/><br><br>
    
<h3 align="center">Creating an AWS Virtual Machine (aka. AWS Instance):</h3>
    <b>NOTE: On this step we'll need to create 2 AWS Instances, 1 for the external internet facing server, and 1 for the internal Windows client.</b><br><br>
  <b>1. On the AWS console searchbar type in EC2, and click on "Launch Instance".</b><br>
  <img src="https://i.imgur.com/9W6ydMM.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>2. Name your instance, select your OS, and then select the "Microsoft Windows Server 2019 Base" AMI (Amazon Machine Image). We can use the same OS and AMI for the client instance.</b><br>
  <img src="https://i.imgur.com/5b8mqZs.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>3. Select your instance type (For the server we'll use a small sized instance, and for the client we'll use a micro sized instance). We'll also need to create a key pair, name the key pair, select the "RSA" type and the ".pem" file format. (This will donwload a file into our computer that we'll need in order to decrypt the password to connect to either instance).</b><br>
  <img src="https://i.imgur.com/6HUdk69.png" height="80%" width="80%" alt="EC2 console"/><br>
  <img src="https://i.imgur.com/hb7K9Up.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>NOTE: This step will be divided in 2 parts, it's very importat that we check that these settings are correct, otherwise our intances won't be able to communicate with each other.</b><br><br>
  <b>4a. First we need to make sure that the correct VPC and subnets are selected (for the Internet facing server we'll need to be in the public subnet of the AZ [us-east-1b], and for the windows client we'll need to be in the private subnet of the same AZ [us-east-1b]). We also need to make sure that the "Auto-assign public IP" function is enabled (only for the external server).</b><br>
  <img src="https://i.imgur.com/G2WZlwy.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>4b. Next, we need to select "Create security group" (this acts as a firewall for the VPCs and the AWS Instances). For the external server we'll select RDP, HTTPS, and HTTP. For the Windows client we'll only select RDP (this will allow us to connect to the Intance).</b><br><br>   
  <b>5. If you have configured an IAM user for your AWS account we can give it permissions to connect to and modify the instances, if you haven't configure it you can skip this step (keep in mind that is always recommended to use an IAM user instead of the AWS root account for security reasons). You'll find this configuration in "Advanced details". Finally, you can click on "Launch Instance" (remember to create the second instance with the settings for the windows client). </b><br>
   <img src="https://i.imgur.com/6QfuH5V.png" height="80%" width="80%" alt="EC2 console"/><br>
   <b>6a. The last step is to create a second network interface for the internet facing server (this is to be able to connect both instances through their IP addresses). You'll click on "Create Network Interface", add a description, select the subnet in which the external server is located, add the same security group as the instance, and click "Create Network Interface" at the bottom of the page. </b><br>
   <img src="https://i.imgur.com/NErZMc3.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>6b. You'll need to attach the network interface to the VPC and the instance where we'll create the external server. Select the newly created network interface, click on actions, click on attach, and you'll have to select the corect VPC and instance, then attach.</b><br>
  <img src="https://i.imgur.com/HiAkrod.png" height="80%" width="80%" alt="EC2 console"/><br>

<h3 align="center">Connecting to our instances with RDP:</h3><br>
  <b>1. On the EC2 console, select the external server instance and copy the public IPv4 address. Then we'll go to Windows app, click on "Devices", click on the "+" symbol on the upper right corner, click on "Add a PC" then paste the IPv4 address where it says "PC name", click on "Add" and finally double click on the PC to connect to the instance. </b><br><br>
  <img src="https://i.imgur.com/ENym6c1.jpeg" height="80%" width="80%" alt="EC2 console"/><br><br>
  <b>2a. Once you're connecting to the instance it'll ask for your credentials (a username and password). On the EC2 console you'll select the instance, click "Connect", click on "RDP client", copy the username and click on get password"</b><br>
  <img src="https://i.imgur.com/kZ7uYvG.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>2b. You'll click on "Upload private key file" (the .pem file we downloaded in our computer). Once uploaded we'll click on "Decrypt password", then copy the password and use it on the Windows app to connect to our instance. </b><br>
  <img src="https://i.imgur.com/vSsPu3L.png" height="80%" width="80%" alt="EC2 console"/><br>
  <b>NOTE: These next steps are meant after we setup our server on the first instance. To connect to our second instance (the Windows client) we can redo the previous steps and use the Windows app, or we can use our server's RDP protocol to connect to the Windows client (kind of like Inception! a computer inside of a computer inside of another computer!)</b><br><br>
  <b>1. Click on the Windows search bar and type RDP.</b><br><br>
   <img src="https://i.imgur.com/6kgcbe7.png" height="80%" width="80%" alt="EC2 console"/><br><br>
  <b>2. Once the "remote desk connection" is opened, you'll have to paste the public IPv4 address for the second instance on the "Computer name". After clicking on "Connect" you'll have to enter the username and password for the second instance (if you've forgotten how to get these, you can refer back to the previous steps on how to get the username and password).</b><br><br>
  <img src="https://i.imgur.com/Vrds4f5.png" height="80%" width="80%" alt="EC2 console"/><br>
