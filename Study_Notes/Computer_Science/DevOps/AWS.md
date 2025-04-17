# Cloud Computing
## AWS Global Infrastructure
> [!important]
> ![](AWS.assets/a2ecdf295ebdac3add7d68e6caad0d55_MD5.jpeg)
> 
> https://infrastructure.aws/
> 
> ![](AWS.assets/32116dcb493c37dba4d081fe6c4570a3_MD5.jpeg)



## Avaibility Zones
> [!important]
> ![](AWS.assets/599a75ab0b64566afbc26fe50dabdde6_MD5.jpeg)![](AWS.assets/image-20250412214031519.png)


# EC2
## What is EC2?
> [!important]
> 
> ![](AWS.assets/bed013dbcd6e0ff6a980bcbcd6b93b24_MD5.jpeg)![](AWS.assets/51a6db1f0177d7284bd1267e102057a0_MD5.jpeg)![](AWS.assets/141ae188a3ac0ca31e2a94a335be818d_MD5.jpeg)![](AWS.assets/0f2fc16180a8f6f8a058fcffeb287020_MD5.jpeg)![](AWS.assets/17fdad2452abba533b23bd3f39c77021_MD5.jpeg)



## EC2 Instance Creation
> [!important]
> ![](AWS.assets/5c2325d9ced0e818fe4aab61afceb6f2_MD5.jpeg)![](AWS.assets/deacf8e9e5ca59e888154e6ef66f4f8a_MD5.jpeg)![](AWS.assets/4fc03e66cf641fe264a761f2c3a555c6_MD5.jpeg)![](AWS.assets/image-20250413153809681.png)![](AWS.assets/c40f20ef0160e84d6ff1945fc678f771_MD5.jpeg)
> 
> 这个时候会把`.pem`保存到本地
> 
> ![](AWS.assets/d59a1406dbc11c71060103d852af2b38_MD5.jpeg)

> [!code] Provisioning
> ![](AWS.assets/0ef981ab401190bc5e69b6f6ea3cb36d_MD5.jpeg)![](AWS.assets/e877626cfb0f6b932140babd39a7413e_MD5.jpeg)
> 
> 这个是用于编写provisioning脚本的地方。
```bash
#!/bin/bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
mkdir /tmp/test1
```

> [!code] Final state
> ![](AWS.assets/140c5b0ec57b8929136dac3e24dc92c7_MD5.jpeg)


## EC2 Instance Connection
> [!important]
> ![](AWS.assets/919c3b49bc664e02b2fda591de7ee8d3_MD5.jpeg)![](AWS.assets/c9c5667212b3214078609f3cef774266_MD5.jpeg)
> 
> We can use `ss -tunlp | grep 80` to check for the processes that are listening on port 80.

> [!code] Visit machine through IP
> ![](AWS.assets/241e23fa65a01097091663285bc2df7a_MD5.jpeg)
> 
> By default, it will visit port 80 on the target IP, but by default(upon instance creation), only port 22 is allowed(which is used for ssh connection). So we need to config for firewall access on port 80.


## Config for EC2 Security Group
### What is Security Group?
> [!important]
> ![](AWS.assets/6b02b1dee9fe7051de0a4226374d2354_MD5.jpeg)![](AWS.assets/image-20250413160003225.png)


### Config Procedures
> [!important]
> ![](AWS.assets/b06152e584419d884f4a0515cd7050fc_MD5.jpeg)![](AWS.assets/09b53f0f79c06ffa39d9a6832be1b335_MD5.jpeg)![](AWS.assets/e05b951fa80f1d86a45929fe4d520cf8_MD5.jpeg)
> 
> Then we should be able to visit:
> 
> ![](AWS.assets/d43810a16a844fd6bf2f605acc9f05ce_MD5.jpeg)




## Requirement Gathering
> [!important]
> ![](AWS.assets/d7db64ac86fdd2c6bfab1cc64c56f281_MD5.jpeg)




# Best-practice EC2 Instance Creation Procedures
## Step 1: Generate Key Pair
> [!code]
> First go to `Network & Security` and create `key pair`, remember to select `.pem` and save the downloaded file(it only contains `private key`) to a safe local place on your local computer.
> 
> ![](AWS.assets/0a161ea4f084fdd0c08d31ddbac36d1a_MD5.jpeg)


## Step 2: Security Groups
> [!important]
> ![](AWS.assets/aca32408923758fc350473dbe0043b93_MD5.jpeg)
> 
> The security group would better follow the naming convention:
> 
> ![](AWS.assets/4011915dd00ac0439ff3b3ae6e948749_MD5.jpeg)
> 
> For rules, remember don't touch anything in the outbound rules, only modify the inbound rules:
> 
> ![](AWS.assets/5a7844b0f110e2c23583864a2475863f_MD5.jpeg)



## Step 3: Launch Instance
> [!important]
> ![](AWS.assets/4aefa62a62171b8bef054b917a1dd5ef_MD5.jpeg)


### Name and Tags
> [!code] Name and Tags
> ![](AWS.assets/3f26bfbee5f40daffee378843b86ca70_MD5.jpeg)



### OS Image
> [!code] OS Image - Ubuntu
> ![](AWS.assets/f8b7d7d7caead476ed4c34126a490025_MD5.jpeg)
> 
> For Instance type, we can just select the free tier one.
> 
> ![](AWS.assets/e2f23de926e11b15ab8cace627492dac_MD5.jpeg)


### Key Pair
> [!important]
> Select the key pair we've created in step 1, as you see, proper tagging can speed up our searching.
> 
> ![](AWS.assets/2302417f4229495851bc4906134c52f4_MD5.jpeg)
> 
> The best practice is to divide your key pair based on the environment(dev or prod).



### Network Settings
> [!important]
> ![](AWS.assets/9a0c0ddce0f7bf51826f40f7653aca0c_MD5.jpeg)



### Storage Configurations
> [!important]
> ![](AWS.assets/983b6d68ecda78b38d2a43c410b93b92_MD5.jpeg)
> 
> gp2 would be better in terms of pricing.


### Advanced Details
> [!important]
> If you want provisioning, you can add it in the User data section.



### Connect to the Instance
> [!important]
> ![](AWS.assets/149c242a65cc985baddacdcf192e6e8c_MD5.jpeg)![](AWS.assets/1ba6f46dfc1b60c2084e60f673614d8e_MD5.jpeg)
> 
> Then follow the instructions:
> 
> ![](AWS.assets/e9bdb68ca0c30463d650f49c624d0229_MD5.jpeg)



## Step 4: Installing packages
> [!code]
> Remind that for ubuntu system, we use `apache2` instead of `httpd` service for web service.
```bash
# This is for ubuntu
sudo apt update
sudo apt install apache2 wget unzip -y
wget https://www.tooplate.com/zip-templates/2128_tween_agency.zip
unzip 2128_tween_agency.zip
cp -r 2128_tween_agency/* /var/www/html/
systemctl restart apache2

# This is for centos
sudo yum update
sudo yum install httpd wget unzip -y
wget https://www.tooplate.com/zip-templates/2128_tween_agency.zip
unzip 2128_tween_agency.zip
cp -r 2128_tween_agency/* /var/www/html/
systemctl restart httpd
```
> [!code]
> Then visit the public IP address(you get a new one each time you stop and start the instance server, rebooting won't change the public IP though) of the server and we should get the tween web page.


## Step 5: Static Public IP
> [!code]
> ![](AWS.assets/a9ceb16c1536177440025d209635109e_MD5.jpeg)![](AWS.assets/84efba09db4324e1906e76c381e42285_MD5.jpeg)
> 
> This public IP is reserved for you. Then you can associate your instance to this public IP.
> 
> ![](AWS.assets/49fcf4cdae5b0aa31c073f3c2c429f3d_MD5.jpeg)![](AWS.assets/d0b85a54b4c17278c73af7e3380fd922_MD5.jpeg)



# AWS-CLI
> [!code]
> https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html


## Config for AWS CLI
### Add IAM User
> [!important]
> Search for IAM service and click for `Users` under `Access management` tab, click `Create User`
> 
> ![](AWS.assets/335742afd189d2bd8aa82340e368e4fd_MD5.jpeg)
> 
> Then in the `Permission policies`, click for `AdministratorAccess`
> 
> ![](AWS.assets/35db301af6fdd1eb978b244303c14f73_MD5.jpeg)


### Config IAM User
> [!important]
> Click the newly created user, and click for `Security credentials` tab:
> 
> ![](AWS.assets/405af80bb527ce0ab27e23c73a5c5ca3_MD5.jpeg)
> 
> Scroll for `Access keys` section, hit `Create access key`:
> 
> ![](AWS.assets/6eeba8d5fa56c40a4d1577ac5e931ae7_MD5.jpeg)
> 
> Then click next till the end, remember don't review your access key to anyone else.
> 
> ![](AWS.assets/bd2a30911560ad0fb1aca029d3aea6af_MD5.jpeg)


### Config AWS CLI
> [!code]
> Copy the access key id and access key you just created as required.
```bash
aws configure
```
> [!code] 
> Now you can open a git bash and browse for the configuration through these commands:
```bash
ls ~/.aws/
# config credentials
cat ~/.aws/config
# [default]
# region = us-east-1
# output = json
cat ~/.aws/credentials
# your access key id
# your access key
```
> [!code]
> Run the following command to get the user id information:
> 
> ![](AWS.assets/8369d2aaf3c00df0fc475d4e769d7c2b_MD5.jpeg)
```bash
aws sts get-caller-identity
```
> [!code]
> Run the following command to get the ec2 regions
```bash
aws ec2 describe-instances
```



## Use AWS CLI to create instance
> [!important]
> You can use the following prompt to let LLM generate the commands to create and configure for new ec2 instances:
```txt
aws command to create key pair, security group allows port 22 from my ip and launch ec2 instance with ami amazon linux in us-east-1 region
```


## AWS commands documentations
> [!code]
> https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html



# EBS(Elastic Block Storage)
## What is EBS?
> [!important]
> ![](AWS.assets/3b53c1df232494b0241481985b1b6ddd_MD5.jpeg)![](AWS.assets/b01ae120160709d4451fab2d3fb3d15a_MD5.jpeg)![](AWS.assets/f754f3635fc3d2565150746a9bb897d0_MD5.jpeg)![](AWS.assets/8f1dd12344f6975bcf517c8dfe039f29_MD5.jpeg)![](AWS.assets/709aab897bccc3d1b80262a4ab4d17e5_MD5.jpeg)



## How to create EBS
> [!important]
> Hit `Create Volume` to create volume.
> 
> Be sure to align the availablility zone of the volume to be the same as the availability zone of the target instance.
> 
> ![](AWS.assets/fb26df108066f58f07a32532372c472c_MD5.jpeg)![](AWS.assets/8da7aecc6d52ccb7c45b47a7db29d0f8_MD5.jpeg)
> 
> Then we get:
> 
> ![](AWS.assets/1a9046ae6b18353665b0efec44ec43be_MD5.jpeg)




## Attach Volumes
> [!important]
> ![](AWS.assets/99f1f81257f5e40acb89d9d0bf958086_MD5.jpeg)![](AWS.assets/4e69c8fee886170172feee401791e080_MD5.jpeg)![](AWS.assets/eaaccaf73f6beb87470e4e900fb51d82_MD5.jpeg)
> 
> We can see that the 5GB volume is attached.
```bash
# We can see the disk storage through
df -h
# And
fdisk -l
```


## Partition Volumes
> [!important]
> ![](AWS.assets/a82d1ba328e60493fe6b19b74347f89f_MD5.jpeg)
```bash
# First execute the following command:
sudo -i
fdisk /dev/xvdf

# Search for n "add a new partition"
```
> [!important]
> ![](AWS.assets/9ffea397f2a9d476b86b6596cb5d4967_MD5.jpeg)
> 
> Or you can input `+3G` for the size of current partition.
> 
> ![](AWS.assets/322569710714f9cc37df5362fcb8cc5f_MD5.jpeg)
> 
> Then hit `w` to alter the partition.
> 
> We can see the new partition.



## Formatting Partition
> [!important]
```bash
# See the disk storage format extensions that are supported on the machine
mkfs

# Or if it shows, no specified devices, you can try the following:
ls /sbin/mkfs.*

# Apply the format to the partition(e.g. mkfs.ext4)
mkfs.ext4 /dev/xvdf1
```
> [!example] Output
> ![](AWS.assets/91b2e471db38cd30f3bada23b625b469_MD5.jpeg)


## Mount/Unmount Partition
> [!code]
> ![](AWS.assets/960be3c4747909789b25e7aa5ec1ac55_MD5.jpeg)
```bash
# This is only temporary mount, after reboot, this mount is gone
mount /dev/xvdf1 /var/www/html
```
> [!example] Output
> ![](AWS.assets/91137bc4a5839dd8ef0cefc4198d9af9_MD5.jpeg)
```bash
umount /var/www/html
```



## Permanent Mount/Unmount
> [!code]
> Append `/dev/xvdf1 /var/www/html/images ext4 0 0` to the configuration file opened by the following command:
```bash
vi /etc/fstab
```
> [!important]
> ![](AWS.assets/9d0daabaf75eec0dbbfb535f55e87879_MD5.jpeg)![](AWS.assets/f3c37fb9b31e9e01e8ebe1d7cb9e0adc_MD5.jpeg)
> 
> The first 0 means no dumping.
> 
> The second 0 means no filesystem check.

> [!code]
> 
```bash
# Some system may ask you to execute the following first:
systemctl daemon-reload

# Make sure /etc/fstab takes effect
mount -a
```
> [!important]
> ![](AWS.assets/e8462825eec0a88f82f024da9a463a24_MD5.jpeg)
> 
> Then you can see that the new filesystem is mounted.
> 
> ![](AWS.assets/image-20250414192325044.png)



## Configure for MySQL
> [!important]
```bash
# install dependencies for mysql
yum install mariadb-server -y

systemctl start mariadb

# Then you should see the data in /var/lib/mysql
ls /var/lib/mysql
```
> [!important]
> ![](AWS.assets/0762e477ef4bf09a30672e81c0da2fba_MD5.jpeg)



# EBS Backup
## Volume Storage
> [!important]
> ![](AWS.assets/f1710a99a0a050dd0e63e55cdc97e848_MD5.jpeg)![](AWS.assets/a802542cc7b0e5180b48d71977dcfa4a_MD5.jpeg)![](AWS.assets/33247d25e7e06933d783dd5acec8703f_MD5.jpeg)


## Snapshot Creation
> [!important]
> ![](AWS.assets/5de4d6f0c070299b940f363f11af4fec_MD5.jpeg)![](AWS.assets/58fcd85066ccf070b2df7a17e32f79b5_MD5.jpeg)
> 
> Then in the Snapshots tab we will see:
> 
> ![](AWS.assets/62a5021b68abe6ebeee84607bddb890a_MD5.jpeg)



## Example: Restore volumes from snapshot
> [!example] Important Example
> Suppose by accident, our database is corrupted(`/var/lib/mysql/` is accidentally deleted). The first thing we should do is to detach the current active volume from the machine. (Detached state of `fdisk -l`, we see `/dev/xdvf` is gone)
> 
> ![](AWS.assets/4a136bd5a23df3d7d46a3727a015af75_MD5.jpeg)
> 
> The steps are:
> - On the machine, `umount /var/lib/mysql`.
> - On the AWS volumes, detach the corrupted volume.
> - Create a new volume based on the uncorrupted snapshot.

> [!code] Create volume from snapshot
> ![](AWS.assets/d5ac453f1423f0134afcce142b42a1e2_MD5.jpeg)![](AWS.assets/c52fa5f4419bc32245a4b7bce557804d_MD5.jpeg)

> [!important]
> After that, you can attach the newly created volume onto the machine, now execute `fdisk -l` again, we should see the `3G` partition back again.
> 
> ![](AWS.assets/ad0952c93208c4867727640687b788f3_MD5.jpeg)



# ELB(Elastic Load Balancer)
## What's Load Balancer?
> [!def]
> ![](AWS.assets/4e5b4b88794c0eb9572494d225d95ce0_MD5.jpeg)![](AWS.assets/c376f34cc0b57608e11ae9c99d395738_MD5.jpeg)![](AWS.assets/8cb8d68f34c9525d9d356d708b9ba6cf_MD5.jpeg)![](AWS.assets/718c9bc7d8781f490a02942790c2d406_MD5.jpeg)



### Classic Load Balancer
> [!def]
> ![](AWS.assets/d90103c45af284db303d477c33584fdf_MD5.jpeg)![](AWS.assets/77fef0b6f808be612ef294e320291d95_MD5.jpeg)![](AWS.assets/708c4e3cb0f602b73125301904aec303_MD5.jpeg)



### Application Load Balancer
> [!important]
> ![](AWS.assets/995e524f160712510338cc6ef63d997e_MD5.jpeg)



### Network Load Balancer
> [!important]
> ![](AWS.assets/fb317dc7acc5d8d0c9997aa72226b469_MD5.jpeg)




## Create Servers from Image
> [!important]
> The first step is to create a bunch of servers, the provisioning file is attached below.
> 
```bash
#!/bin/bash

# Variable Declaration
#PACKAGE="httpd wget unzip"
#SVC="httpd"
URL='https://www.tooplate.com/zip-templates/2098_health.zip'
ART_NAME='2098_health'
TEMPDIR="/tmp/webfiles"

yum --help &> /dev/null

# See if it is a centos system
if [ $? -eq 0 ]
then
   # Set Variables for CentOS
   PACKAGE="httpd wget unzip"
   SVC="httpd"

   echo "Running Setup on CentOS"
   # Installing Dependencies
   echo "########################################"
   echo "Installing packages."
   echo "########################################"
   sudo yum install $PACKAGE -y > /dev/null
   echo

   # Start & Enable Service
   echo "########################################"
   echo "Start & Enable HTTPD Service"
   echo "########################################"
   sudo systemctl start $SVC
   sudo systemctl enable $SVC
   echo

   # Creating Temp Directory
   echo "########################################"
   echo "Starting Artifact Deployment"
   echo "########################################"
   mkdir -p $TEMPDIR
   cd $TEMPDIR
   echo

   wget $URL > /dev/null
   unzip $ART_NAME.zip > /dev/null
   sudo cp -r $ART_NAME/* /var/www/html/
   echo

   # Bounce Service
   echo "########################################"
   echo "Restarting HTTPD service"
   echo "########################################"
   systemctl restart $SVC
   echo

   # Clean Up
   echo "########################################"
   echo "Removing Temporary Files"
   echo "########################################"
   rm -rf $TEMPDIR
   echo

   sudo systemctl status $SVC
   ls /var/www/html/

else
    # Set Variables for Ubuntu
   PACKAGE="apache2 wget unzip"
   SVC="apache2"

   echo "Running Setup on CentOS"
   # Installing Dependencies
   echo "########################################"
   echo "Installing packages."
   echo "########################################"
   sudo apt update
   sudo apt install $PACKAGE -y > /dev/null
   echo

   # Start & Enable Service
   echo "########################################"
   echo "Start & Enable HTTPD Service"
   echo "########################################"
   sudo systemctl start $SVC
   sudo systemctl enable $SVC
   echo

   # Creating Temp Directory
   echo "########################################"
   echo "Starting Artifact Deployment"
   echo "########################################"
   mkdir -p $TEMPDIR
   cd $TEMPDIR
   echo

   wget $URL > /dev/null
   unzip $ART_NAME.zip > /dev/null
   sudo cp -r $ART_NAME/* /var/www/html/
   echo

   # Bounce Service
   echo "########################################"
   echo "Restarting HTTPD service"
   echo "########################################"
   systemctl restart $SVC
   echo

   # Clean Up
   echo "########################################"
   echo "Removing Temporary Files"
   echo "########################################"
   rm -rf $TEMPDIR
   echo

   sudo systemctl status $SVC
   ls /var/www/html/
fi 

```
> [!code] Create image(AMI) from instance
> Once we have the instance running successfully and show the website, we can create the image from that instance so that we can replicate instances.
> 
> ![](AWS.assets/a99c7d4e243bfcbcc6eb669347485bcf_MD5.jpeg)
> 
> Then create image:
> 
> ![](AWS.assets/43863acb0cba053580b1567cfdf86f70_MD5.jpeg)
> 
> Wait for sometime until the status of the image changed to `Available`



## Create Launch Template
> [!important]
> Go to `Launch Template` section. We can create launch template from ami(which can be created from instance). 
> 
> Once we created the launch template, we can launch the instance from the template.
> 
> ![](AWS.assets/ba3f3350a3056e95914eb390fb8e5c82_MD5.jpeg)



## Create Load Balancer
> [!important] Step 1: Create Target Groups
> Go to `Target Groups`(group of instances with health checks) first, and `Create target group`:
> 
> ![](AWS.assets/265d3f4324aa628ebcc32822902e0032_MD5.jpeg)![](AWS.assets/8169198d47e50033dc814dd29e777884_MD5.jpeg)![](AWS.assets/c7e8599b94a3c74141393899f323f598_MD5.jpeg)
> 
> Here health check path means `http://<ipv4>:80/`, if you have a different port, you can specify it in the `Advanced health check settings`.
> 
> - **Healthy Threshold**: It is the number of times it will check whether the port is healthy until final verdict.
> - **Unhealthy threshold:**  Number of times of unhealth response until classifying the system as unhealthy.

> [!important] Step 2: Register Targets
> ![](AWS.assets/501065da17794f61090f9e854429ec73_MD5.jpeg)
> 
> Click `Include as pending below` first, then you should see both targets move to the `Review targets` section:
> 
> ![](AWS.assets/9305eaff5d2476d3dc1031212d6234cc_MD5.jpeg)
> 
> Then hit `Create target group`.

> [!important] Step 3: Create Load Balancer
> Go to `Load Balancers` section, hit `Create load balancer`:
> 
> ![](AWS.assets/df4f616d25e4c84c44137c1355c878f9_MD5.jpeg)
> 
> We will go with **Application Load Balancer** with HTTP/HTTPS routing.
> 
> ![](AWS.assets/24234dba4ede4cb945ce11ef54b16d45_MD5.jpeg)
> 
> Select all availability zones:
> 
> ![](AWS.assets/8dc854eeb84a83103778732c0eb5a0da_MD5.jpeg)
> 
> For load balancer, we have to create a new security group, different from those for instances, adjusting the inbound rules as shown(many mobile phones use IPv6 so we have to include that), then hit `Create security group`:
> 
> ![](AWS.assets/bc884ee719dadeea83253bde5b46647f_MD5.jpeg)
> 
> Then back to load balancer creator, refresh and select the security group we have just created:
> 
> ![](AWS.assets/0c6c7a460ad71d0a64776a5493946f50_MD5.jpeg)
> 
> Then set the listener to route the incoming traffic on the frontend port 80 to the specified target group(backend at port 80), then hit `Create load balancer`:
> 
> ![](AWS.assets/658192db03787b22fff5d52eba8dc56a_MD5.jpeg)
> Then in your `Load Balancers` section, wait for the status from **provisioning** to **active**. 



## Configure for Access
> [!bug]
> Typically, you find the DNS name of the server, paste that into the browser and you should access the web page, but if there is problem(most often 504 gateway time-out), please follow the steps.
> 
> ![](AWS.assets/87051e74a7b7bc87d706e7ff679225d1_MD5.jpeg)

> [!important] Step 1: Find the problems
> If you try directly visiting the IP of the individual servers, the website is accessible. So the problem lies in between the load balancer and the individual servers, which is **security group**.
> 
> The problem is that in the **inbound rules** of **individual servers**, they are not allowing the traffic from the **load balancer**.
> 
> Here if we go to `Target Groups` section, we see that the health check for instances didn't pass:
> 
> ![](AWS.assets/b3cdf0d9db309664e993c76835230c5c_MD5.jpeg)

> [!important] Step 2: Adjust the Security Group
> Since both `web01` and `web02` instance use the same the security group, we add the security group of the **load balancer** to the individual server:
> 
> ![](AWS.assets/4ba70b65deae316f912e7b9ed140159b_MD5.jpeg)
> 
> So that anything inside this security group(like the load balancer) can access the port 80 of the individual server. Wait for sometime until the healthy check pass in the **Target Groups**:
> 
> ![](AWS.assets/a4505ba04d4db2555eefbd32816580a3_MD5.jpeg)

> [!success]
> Then we should be able to access `health-elb-968074153.us-east-1.elb.amazonaws.com` from the browser.
> 
> ![](AWS.assets/3ae5df67addb3785406151d500afa488_MD5.jpeg)

> [!tip]
> Remember we you are doing maintanence on the instance of a target group, you should deregister it first, modify your instance, then register it back to run the health check.


## Destroy the load balancer
> [!important]
> When you delete the load balancer, you do it in the reverse order as we create one. 
> 
> Load balancer -> Target group -> Instances




# Cloudwatch
## What is Cloudwatch?
> [!def] Introduction
> ![](AWS.assets/5af4cb53e7a8e45861fbb658d9f5e196_MD5.jpeg)![](AWS.assets/e8b4652321342a3e62482baf20cd852a_MD5.jpeg)![](AWS.assets/aece712e27bfa94d5cb910f782f4c252_MD5.jpeg)![](AWS.assets/f001a1184de47cd0caf5a811ff915593_MD5.jpeg)
> 
> When you start an instance, the cloudwatch is automatically on and it will check all of the following metrics every 5 minutes:
> 
> ![](AWS.assets/40b128635df70c5c3ee3370ef1a7380e_MD5.jpeg)



## Detailed Monitoring
> [!important]
> ![](AWS.assets/2d29689c7b83849aed01f4735738de05_MD5.jpeg) 
> 
> Warning: it is not free.


## Stress CPU
> [!code] Install dependencies
```bash
# Install the dependencies(Before Amazon Linux 2023, otherwise not needed)
cat /etc/os-release
sudo amazon-linux-extras install epel -y 
sudo yum install stress -y

# After 2023, just one command
sudo yum install stress -y
```

> [!code] Stress CPUs
```bash
# This command will create 4 processes simultaneously and stress the CPU for 300 seconds, and it will run at the background
nohup stress -c 4 -t 300 &

# See all the running processes
top
```
> [!example] Output
> ![](AWS.assets/a2dbc052202cac62376c8879f1fbb555_MD5.jpeg)





# EFS(Elastic File System)
## What is EFS?
> [!def]
> https://us-east-1.console.aws.amazon.com/efs/home?region=us-east-1#/get-started


## Create EFS 
> [!important] Step 1: Create security group
> Since EFS is a **network-based file system**, so we have to create a security group before creating the EFS. Be careful you should not modify the outbound group. Only modify the inbound group. This settings mean to let your EFS to access your instance's file system.
> 
> 
> ![](AWS.assets/c5462e781cb8ceca76086cdc8b30feae_MD5.jpeg)![](AWS.assets/3aa9dafe2aea0cea149547c972c1c22a_MD5.jpeg)

> [!important] Step 2: Create file system
> ![](AWS.assets/620ae55c2b0a1c09c9bf0883d7bb0a71_MD5.jpeg)![](AWS.assets/2a70ad8b62101a0f23f3850b11e9e09c_MD5.jpeg)![](AWS.assets/861e5b5d2e6245994b9609240daa7afa_MD5.jpeg)![](AWS.assets/c31eee7895336fb9fc81238ecd8ded05_MD5.jpeg)

> [!important] Step 3: Create Access Point
> ![](AWS.assets/2187021a4724d1ca671a2177e0aaa21b_MD5.jpeg)

> [!important] Step 4: Install Amazon EFS Client Helper
> https://docs.aws.amazon.com/efs/latest/ug/mounting-fs.html
> 
> ![](AWS.assets/2c9d55b3da9a4ea94da1db5978c72152_MD5.jpeg)![](AWS.assets/55d8059756b803c9aedd2567412beb22_MD5.jpeg)![](AWS.assets/bde430d9c722cf5fcae5ea423faa6850_MD5.jpeg)
> 
> You should choose different way of installing EFS Helper based on your system.(e.g. Ubuntu, centos， amazon linux)
```bash
# For amazon linux, just execute the following
sudo yum install amazon-efs-utils -y
```

> [!important] Step 5: Mounting EFS File Systems
> With client helper installed, we can mount efs file system automatically.
> 
> ![](AWS.assets/ed114b798441b4bf0086d14df2a4818b_MD5.jpeg)![](AWS.assets/d7b67fbee62e00a032b656eca3ad2be3_MD5.jpeg)![](AWS.assets/f347cef88b3de8d41fd6f75368d0836e_MD5.jpeg)
```bash
# We have to replace the file-system-id, efs-mount-point and access-point-id with the one we have created
file-system-id:/ efs-mount-point efs _netdev,noresvport,tls,accesspoint=access-point-id 0 0

# Execute this
vi /etc/fstab
# Copy the following command to append to the EOF
fs-02c9704d6debb01e9:/ /var/www/html/images efs _netdev,noresvport,tls,accesspoint=fsap-00a1a1eed2eb4d623 0 0
# After you save the /etc/fstab, run the following to mount
mount -fav
```
> [!example] Output
> If everything is good, you should see the following:
> 
> ![](AWS.assets/f1fb7e6b1aa0cefaef502429fdfc4705_MD5.jpeg)


# Autoscaling
## What is Autoscaling?
> [!def]
> ![](AWS.assets/3c4c8fca416bbbc82a07225176f7768c_MD5.jpeg)![](AWS.assets/6d32f347d64bb30d23c053a4e976fc34_MD5.jpeg)![](AWS.assets/2c38be2ce93a2a9c40cbee7bc6bcf179_MD5.jpeg)![](AWS.assets/286a069c4e62894a2afd93881eb244ab_MD5.jpeg)



## Create Autoscaling Group
### Step 1: Create a target group
> [!important] Step 1: Create a target group
> Create an empty target group is fine. Since autoscaling group wil dynamically add instances to this target group depending on the usage.


### Step 2: Create a load balancer
> [!important] Step 2: Create an application load balancer
> Just remember to select all the regions and set the inbound rules of the security group to be the following:
> 
> ![](AWS.assets/1bc0c2b0059283fbeed1e4c16bb6c0cb_MD5.jpeg)
> 
> Also in the `Listener and routing` section, forward the request to the load balancer to the target group we have just created.
> 
> ![](AWS.assets/9cdb4e43d9a79e474fca172d7b8f9b7d_MD5.jpeg)


### Step 3: Create auto-scaling group
> [!important] Step 3: Create auto-scaling group
> ![](AWS.assets/7a4f53d1f05fb5dbe5f28e30effed261_MD5.jpeg)![](AWS.assets/f7bfdb7ea69b20121dbb9512772f29d4_MD5.jpeg)![](AWS.assets/526a10d539ea0b2de57db4ef5d8761d5_MD5.jpeg)
> 
> For **integration with other services**:
> - Need to attach to an existing load balancer since we want to autoscale
> - Health checks need to include `ELB health check` and `EC2 instance health check`, 
> 	- EC2 checks will only test port accessibilty, and flag the instance as unhealthy if connection attempt failed.
> 	- ELB checks will make sure if one instance is unhealthy in the target group, it will launch a new one and replace that one.
> 
> ![](AWS.assets/f72bda8441406df898cc8323fb215bcf_MD5.jpeg)![](AWS.assets/9c1873a1a4dcb26321cc5189cec934f4_MD5.jpeg)
> 
> Here at the bottom we see `Disable scale in to crate only scale-out policy`, if disabled, you are saying that I don't want the unhealthy instances to be automatically terminated(since I may have important data stored on it). But if you are using shared storaged like EFS or you don't care about data recovery, you can uncheck it.
> 
> ![](AWS.assets/f24beab4fa9bb186d4faf840d511d4fa_MD5.jpeg)![](AWS.assets/f799f2e15a85a4c6b702567e382fe14b_MD5.jpeg)
> 
> Finally we create an autoscaling group!
> 
> ![](AWS.assets/2554c47a6a58179d18a6d0617f0b8214_MD5.jpeg)
> 
> Once done initialization, we can see in the instance management tab the status of the newly created instances:
> 
> ![](AWS.assets/c304f2dc7457751bf3d7407b2d63b614_MD5.jpeg)
> 
> Here you can `Set scale-in protection` for the instance that you don't want to be automatically terminated by the autoscaling group.
> 
> ![](AWS.assets/32bf5a7454d18ddf8483c5ff009661f6_MD5.jpeg)



## Active instance refresh
> [!important]
> Here for the `Instance Refresh`
> 
> ![](AWS.assets/b6496a64fb8f7ee3f22b8929d8f9096b_MD5.jpeg)![](AWS.assets/06bf3223ceeef65293a1455d843e200d_MD5.jpeg)
> 
> Basically you can make changes to the launch template of this autoscaling group and when you refresh, it will replace the current older-version instances gradually with new-version ones.



## Testing Autoscaling Features
> [!code]
> You can terminate the instances created by ASG to simulate unhealthy instance status to see if ASG is replacing the instances with healthy ones. 
> 
> You will get email notification if you have configured that before.
> 
> You have to delete the autoscaling group first otherwise you cannot delete up your instances.




# S3(Simple Storage Service)
## What is S3?
> [!def]
> ![](AWS.assets/50b174c0191d0b6a14265ab2aeaf8273_MD5.jpeg)![](AWS.assets/82865b18f7e120e8118a58a7552da727_MD5.jpeg)![](AWS.assets/4c3d878d818a58806c5d40f22b76765a_MD5.jpeg)![](AWS.assets/60cbe0dadda3895023cbfcca71f0758b_MD5.jpeg)![](AWS.assets/image-20250417185104706.png)


## S3 Storage Classes
> [!def]
> ![](AWS.assets/db6dbd32a2c017d6d98813a16c56dd5f_MD5.jpeg)![](AWS.assets/f3f2dd2846ba26cecaf76a812cabf430_MD5.jpeg)


## S3 Lifecycle Policies
> [!def]
> ![](AWS.assets/14a9dd76dceae164d1c58eeabac7d403_MD5.jpeg)![](AWS.assets/c39c53646b4f85feabd2a3e51c04c4a8_MD5.jpeg)![](AWS.assets/49ca17b9e785b5dfdc4196dc5655c0d4_MD5.jpeg)





![](AWS.assets/784f3748e67d71edbb9d72d156404ed6_MD5.jpeg)










# RDS
## What is RDS?
> [!def]







