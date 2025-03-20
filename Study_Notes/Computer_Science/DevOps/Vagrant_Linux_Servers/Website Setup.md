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





## Step 1: Install Dependencies
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
                 php-zip -y
```


## Step 2: Install WordPress
> [!code]
> 创建wordpress的安装目录`/src/www`, 设置ownership, 并且从https://wordpress.org/ 下载文件
```
sudo mkdir -p /srv/www
sudo chown www-data: /srv/www
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```


## Step 3: Configure Apache for WordPress
> [!code]
> 首先创建`WordPress`配置文件, `linux`系统种配置文件一般在`/etc/`目录下，我们创建`/etc/apache2/sites-available/wordpress.conf`
```
<VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```
> [!code]
> 之后执行三个命令激活
```bash
sudo a2ensite wordpress  # Enable the site
sudo a2enmod rewrite   # Enable URL rewriting， setting redirect rule
sudo a2dissite 000-default  # Disable the default "It works" site
```
> [!code]
> 最后`reload` apache 服务
```
sudo service apache2 reload
```


## Step 4: Configure Database
> [!code]
> 执行下列命令, 其中：
> - `wordpress@localhost` 表示 user wordpress 只能从相同主机连接到数据库，不能从external IP连接
> - `show databases;` 展示所有创建的数据库
> - `DROP USER wordpress@localhost;` 可用于删除用户
```bash
sudo mysql -u root # Login to mysql as root user

mysql> CREATE DATABASE wordpress;

mysql> CREATE USER wordpress@localhost IDENTIFIED BY '<your-password>'; # 这里密码可以任意

mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wordpress.* TO wordpress@localhost; # Make sure it is single line

mysql> FLUSH PRIVILEGES;

mysql> quit
```



## Step 5: Configure Wordpress to connect to MySQL
> [!code]
> 首先初始化配置`wordpress`后端php服务器的`wp-config.php`
```
sudo -u www-data cp /srv/www/wordpress/wp-config-sample.php /srv/www/wordpress/wp-config.php
```
> [!code]
> 设置`wordpress`连接数据库的密钥, 翻译一下这三个指令在做什么:
> - `sudo -u www-data`表示以`www-data`用户的身份运行这个指令
> - `sed`是替换指令，表示在`srv/www/wordpress/wp-config.php`中将`database_name`为`wordpress`
> - 后面两个同理
> - `vim /srv/www/wordpress/wp-config.php`的第23~32行查看修改是否生效
>
```bash
sudo -u www-data sed -i 's/database_name_here/wordpress/' /srv/www/wordpress/wp-config.php   # 不要替换database_name_here
sudo -u www-data sed -i 's/username_here/wordpress/' /srv/www/wordpress/wp-config.php        # 不要替换username_here
sudo -u www-data sed -i 's/password_here/<your-password>/' /srv/www/wordpress/wp-config.php  # 不要替换password_here, 但需将<your-password>替换成admin123
```
> [!code]
> 编辑`wp-config`进行数据库配置第51~58行, 将其全部删除，在`command-line`模式下运行`dd`即可删除当前光标所在行
```
sudo -u www-data vim /srv/www/wordpress/wp-config.php

define( 'AUTH_KEY',         'put your unique phrase here' );
define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
define( 'NONCE_KEY',        'put your unique phrase here' );
define( 'AUTH_SALT',        'put your unique phrase here' );
define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
define( 'NONCE_SALT',       'put your unique phrase here' );
```
> [!code]
> 将下列内容复制到原来的位置, 保证服务器不会受到`known secrets`的攻击
```
define('AUTH_KEY',         '7|>&9!ngBN*9-+<Kl)RT`Um-<b]sHDMfdgNu?A|]=}H;w),>t) `Q[#>k*MULBx^');
define('SECURE_AUTH_KEY',  '[e!6^1roC+;7A~-^r+&W[Mvi(C]P%b{;5zfwXrSy0yfNOO?OLKYCD-~BZy|EAc2g');
define('LOGGED_IN_KEY',    'Y8xt4jcI|1x-h-D8h_j8=O7Di@&1BB]G|:[%|+N::cb Pl@Lot.4=Sm(yY[U*DH3');
define('NONCE_KEY',        '9uWJ0 -lAi)XQ= O5d-4iC0(.o;`@O|BWp3xw-S`1-V?w1ts7kxxMm*@KR$]|u/;');
define('AUTH_SALT',        '[x|FEW}<yX-[C|[t5!bG,$M$;,I,m?!=b5KQ#no`rN=|I2+w| =2RF&pI3A2xj=,');
define('SECURE_AUTH_SALT', '1xFKa;=}tExR5Y5ox5|]X1P<11~,LKypyi8,l-`B@pw*- srcxa/+=_rEOCXm8@.');
define('LOGGED_IN_SALT',   'M6OsY.lGE~[)|oR:u+C->m7a&Nrn;!S@h`KH6bty]58?~^S*T-:24RCz`~Ya?e{t');
define('NONCE_SALT',       '|Faeii_NV;~A(K0t/NkwZ~tq&XnL/tsoA/{YxAEb(,o{0Q8tirRnaN{hcTm2>+=n');
```


## Step 6: Configure WordPress Visit 
> [!code]
> 输入`ip addr show`查看当前服务器的private network ip. 是`192.168.56.26`, 在主机上打开，正常应当会出现`wp-admin/install.php`的界面
> 
> ![](Website%20Setup.assets/946209e16c41da809553742a962a0455_MD5.jpeg)
> 
> 按照步骤设置注册用户信息，全部配置好之后会得到:
> 
> ![](Website%20Setup.assets/c0f39ac6fed47e3933e1eae953c017d6_MD5.jpeg)



