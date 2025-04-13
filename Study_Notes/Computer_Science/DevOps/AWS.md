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




# Best-practice EC2 Instance Creation
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



# EBS







# ELB








# Cloud Watch





# EFS






# Autoscaling






# S3








# RDS






