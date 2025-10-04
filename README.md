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
- <b>Windows App<b>
  
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
