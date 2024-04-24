# **Access-EC2-instance-private-IP-from-the-external-network-using-VPN-AWS-OpenVPN-AWS-Security**

![1_oah2o6up-klyynaK_Tv0EA](https://github.com/Pavithra1640/Deploying-a-Portfolio-on-AWS-S3-using-GitHub-Actions-/assets/165140491/adf78d82-48b6-4547-aa63-2ad09c805757)

let's start ....
**What is VPN?**
VPN(Virtual Private Network). it is allow to access the internet with more security and privacy. When we use the VPN, Your devices send your internet traffic to the internet data is encrypted, so even if someone intercepts it, they can't read it.your ip address is hidden, making it is diffcult for the websites and Advertisers and internet service provider(ISP) to track our online activities.when we connect your public Wi-Fi network, a VPN add extra layer of security.
**What is ec2 instance?**
ec2 is nothimg but a virtual machine
**what is difference between the public and private?**
- public ip - we can connect to the outside of the internet with help internet gateway(IGW).
- private ip - we can't connecting to the outside of the internet. we can connect the internet with help of NAT gateway.
**How to setup VPN**
  - **Step1: Launch the EC2 instances**
    ![1](https://github.com/Pavithra1640/Deploying-a-Portfolio-on-AWS-S3-using-GitHub-Actions-/assets/165140491/e17e39ea-2dd8-453b-ada0-7ed764ca5f2d)
  - **Step2: Choose An Amazon Machine Image**
    For Step 1 “Select” the OpenVPN Access Server image, seen first below.
  - **Step3: Choose An EC2 Instance Type**
    Next, for Step , you will choose your EC2 instance type. Since I am the only person using my VPN, I selected the t2.micro instance, which is the free 12 month tier offered to new 
    users.
  - **Step4: Configure The Instance Details**
    we make some modifications to the instance that guard our VPN against accidental deletion. To do this, select the “Protect against accidental termination” option
  - **Step 5: Naming The Instance With Tags**
    Okay okay, were almost done creating the instance for our VPN to run on in the cloud
    You can tag it however you’d like, but I’d recommend keeping OpenVPN in the tag value. YourNameOpenVPN, MyOpenVPN, or OpenVPN all should work fine.
  - **Step 6: Configure The Instance’s Security Groups**
  - **Step 7: Review And Launch The EC2 Instance**
  - **Step 8: Configure Your OpenVPN Installation**
    At the moment, your VPN is public.This means that any one is able to access your server through the IP address.
    make some changes now that add some layers of security to your instance and the VPN you just installed.creating a permanent IP and private IP address.creating a user account to 
    manage and access the VPN with, and turning off settings on the server which disable public connections.
  - **Step 9: Create An Elastic IP For Your Instance**
    As soon as the instance is shut down, a new public IP gets assigned for the same instance. This means if we set up the VPN server with the default IP, we wont be able to access the 
    VPN if the instance is shut down. Elastic IP solves this issue and assigns a permanent IP address.
    Inside Elastic IPs, we are going to **“Allocate A New Address”** and select this our OpenVPN instance.
  -**Step 10: SSH Into Your Instance To Initialize OpenVPN**
    ssh -i YourKey.pem openvpnas@YourElasticIP
    or
    you can use the putty
   - sudo chmod 600 ~/YourKey.pem
  - **Step 11: Complete Initial OpenVPN Configuration Settings**
  - **Step 12: Create A New User Account For Managing OpenVPN**
    sudo passwd <your password>
  - **Step 13: Download OpenVPN Application For Your Computer**
    In your browser, open a new tab and type http://YourPublicIP and hit enter.
    image
    In my case, I named my user openvpn. When you’re done, hit “Go”.
  - **Step 7: Logging Into Your New VPN**
  - **Step 8: Disable Public Access To The VPN**
    https://YourElasticIP:943/admin
    Login with your username and password. You should see this notification. Hit accept to access the admin portal for the VPN.

    Scroll down the bottom of the page and toggle off the admin and client web server options
    image
    After this is done, hit save at the bottom. The page will update at the top to include this message. Hit “Update Running Server.”
    image
    When you hit the button, the page will break. This is a good sign, because we just successfully disabled the usage thru the public IP.
  -**Step 10: Accessing The Admin Portal With The Private IP**
    https://YourPrivateIP:943/admin
  - **Lastly — Disable SSH Access**
  - Returning to your AWS EC2 Console, select your instance. On the left side navigation panel, under “Network & Security,” select “Security Groups.”
  - image
  - Under the instance, there now should be a tab labeled “Inbound.” Select this tab and hit the edit button. You should now be able to delete SSH as a type by clicking the X on the 
    right. Hit save to keep the changes.
    image
    



