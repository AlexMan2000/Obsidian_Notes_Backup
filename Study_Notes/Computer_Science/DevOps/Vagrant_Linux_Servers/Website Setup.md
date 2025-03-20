# Centos - httpd
## Static and Manual Setup
> [!info]
> 首先需要安装`httpd`服务，他是web server得以顺利运行的依赖包: `sudo -i; yum install httpd wget vim unzip zip -y`，其中`-y`表示非`interactive`模式且所有问题的回答均为`yes`。

> [!important]
> 服务器渲染`html`的入口文件储存在`var/www/html`下的`index.html`。




## Automate Setup


# Ubuntu - Wordpress Steup
> [!info]
> **WordPress** 是一个基于 **PHP** 和 **MySQL** 的 **开源内容管理系统（CMS，Content Management System）**，主要用于创建和管理网站、博客、企业官网、电商平台等。

> [!important]
> 具体配置步骤:
> 访问https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview查看

## Install Dependencies
> [!important]
```
sudo apt update
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip
```


## Install WordPress
> [!code]
> 创建wordpress的安装目录`/src/www`并且从https://wordpress.org/ 下载文件
```
sudo mkdir -p /srv/www
sudo chown www-data: /srv/www
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```


## Configure Apache for WordPress
> [!code]




## Setup Vagrant file
> [!important]
> Search for the vagrant box you want to use here:
>`https://portal.cloud.hashicorp.com/vagrant/discover`
>
>In this example, we search for `ubuntu 20` and select `ubuntu/focal64`(if your vm provider is virtualbox for windows) or search for `spox/ubuntu-arm` (if your vm provider is macos), click into it and look for the name shown in the green box:
>
>![](Website%20Setup.assets/39c60f4f7ae228c78618a2b008df9ddc_MD5.jpeg)
> 
> In your host machine, create a folder `wordpress`, and `cd wordpress`, execute `vagrant init` to generate a vagrantfile template.
> 
>



### Windows
> [!code]
>  Modify the line (15) containing `config.vm.box="base"` to `config.vm.box="ubuntu/focal64"`
> 
> - Uncomment the line (35) `config.vm.network "private_network", ip: "192.168.56.26"`
> 
> - Uncomment the line (40) `config.vm.network "public_network"`
> 
> - Uncomment the line (59) `config.vm.provider "virtualbox" do |vb|`
> 
> - Uncomment the line (64) and set to `vb.memory="1600"`
> 
> - Uncomment the line (65) `end` to make the syntax of vagrantfile valid.






### MacOS
> [!code]
>
>  Modify the line (15) containing `config.vm.box="base"` to `config.vm.box="spox/ubuntu-arm"`
> 
> - Uncomment the line (35) `config.vm.network "private_network", ip: "192.168.56.26"`
> 
> - Uncomment the line (40) `config.vm.network "public_network"`
> 
> - Uncomment the line (59) `config.vm.provider "virtualbox" do |vb|`
> 
> - Uncomment the line (64) and set to `vb.memory="1600"`
> 
> - Uncomment the line (65) `end` to make the syntax of vagrantfile valid.
> 
> - Add `config.vm.box_version = "1.0.0"` after line (15) 
> - Modify the config.vm.provider to be 
```
config.vm.provider "vmware_desktop" do |vmware|
	vmware.ssh_info_public = true
	vmware.gui = true
end
```
