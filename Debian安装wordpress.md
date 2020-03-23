# Debian 安装 wordpress

获取 root 权限

```shell
sudo -i
```

安装 yum 和 wget

```shell
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install yum
sudo apt-get install wget
```

屏幕监视程序

```shell
screen -S lnmp
```

* 如果提示`screen: command not found` 命令不存在可以执行：`yum install screen` 或 `apt-get install screen`安装，如果VPS连接中断，可以使用命令`screen -R lnmp`返回会话窗口。

安装 lnmp 一键脚本

```shell
wget http://soft.vpser.net/lnmp/lnmp1.6.tar.gz -cO lnmp1.6.tar.gz && tar zxf lnmp1.6.tar.gz && cd lnmp1.6 && ./install.sh lnmp
```

* 选择配置见lnmp[教程](https://lnmp.org/install.html)
* 安装完成后运行`killall screen`关闭监视窗口

创建虚拟主机

```shell
lnmp vhost add
```

* 选项配置见[lnmp教程](https://lnmp.org/faq/lnmp-vhost-add-howto.html)或[搬瓦工教程](https://www.banwagongzw.com/17.html)

下载解压 wordpress 并移动文件至网站根目录

```shell
wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
cd wordpress
mv * /home/wwwroot/www.databian.com/
```

* 以上命令可以用 && 连接为一整个脚本

* ```shell
  wget https://wordpress.org/latest.tar.gz && tar -xzvf latest.tar.gz && cd wordpress && mv * /home/wwwroot/www.databian.com/
  ```

配置文件权限

```shell
chown www:www -R /home/wwwroot/www.databian.com
```

* 提示`chown: changing ownership of /home/wwwroot/www.baidu.com/.user.ini': Operation not permitted` 执行以下命令. `sed -i 's/,scandir//g' /usr/local/php/etc/php.ini && lnmp php-fpm restart` 

将域名解析到服务器，输入域名即可开始配置。

参考链接**

lnmp一键安装 https://lnmp.org/install.html

搬瓦工搭建 WordPress https://www.banwagongzw.com/17.html
