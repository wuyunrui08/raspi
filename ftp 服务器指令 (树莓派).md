
# ftp 服务器指令 (树莓派)

---

## 简介
- [安装服务器](#install)
- [配置服务器](#profile)
- [设置静态ip](#setstaticip)
- [部分选项的注释](#explain)


---

<h2 id="install"></h2>

### 安装服务器

首先是在树莓派上面配置ftp服务器,根据以下指令执行

- ``sudo apt-get update``更新系统
- ``sudo apt-get install vsftpd``安装``ftp``服务
- ``sudo service vsftpd start``启动``ftp``服务
- ``sudo nano /etc/vsftpd.conf``修改``ftp``属性文件

---

<h2 id="profile"></h2>

### 配置服务器

属性文件修改,首先找到该属性:

```
找到以下行,删除注释
anonymous_enable=NO  
表示:不允许匿名访问
local_enable=YES   
设定本地用户可以访问。
write_enable=YES
设定可以进行写操作
local_umask=022
设定上传后文件的权限掩码。

```

---

<h2 id="setstaticip"></h2>

### 修改静态ip

修改为静态ip地址,我们只需要进行以下的设置:

- 使用``sudo vim/etc/dhcpcd.conf``修改或增加以下的配置项

> ``interface <接口名字>``指定接口
> ``static ip_address=192.168.<需和routers相同>.?/24``静态ip,需要和路由器/网关部分相同
> ``static routers=192.168.<需和ip相同>.?``路由器/网关IP地址
> ``static domain_name_servers=114.114.114.114``手动自定义DNS服务器
> 修改完成之后,使用重启便可修改完成


---

<h2 id="explain"></h2>

### 部分选项的注释

- ``anonymous_enable=YES`` 支持匿名帐号
- ``local_enable=YES ``支持本地帐号
- ``write_enable=YES ``允许使用任何可以修改文件系统的FTP的指令
- ``local_umask=022 ``屏蔽权限即本地用户上传的文件权限
- ``anon_upload_enable=YES``允许匿名用户上传文件
- ``anon_mkdir_write_enable=YES``允许匿名用户创建新目录
- ``dirmessage_enable=YES ``允许为目录配置显示信息,显示每个目录下面的``message_file``文件的内容
- ``xferlog_enable=YES ``开启日记功能
- ``connect_from_port_20=YES ``使用标准的20端口来连接ftp
- ``chown_uploads=YES``所有匿名上传的文件的所属用户将会被更改成``chown_username``
- ``chown_username=whoever``匿名上传文件所属用户名
- ``xferlog_file=/var/log/xferlog``日志文件位置
- ``xferlog_std_format=YES ``使用标准的日志格式
- ``idle_session_timeout=600``空闲连接超时
- ``data_connection_timeout=120``数据传输超时
- ``nopriv_user=ftpsecure``当服务器运行于最底层时使用的用户名
- ``async_abor_enable=YES``允许使用\"async ABOR\"命令,一般不用,容易出问题
- ``ascii_upload_enable=YES``管控是否可用ASCII 模式上传。默认值为NO
- ``ascii_download_enable=YES``管控是否可用ASCII 模式下载。默认值为NO
- ``ftpd_banner=Welcome to blah FTP service `` login时显示欢迎信息.如果设置了banner_file则此设置无效
- ``deny_email_enable=YES``如果匿名用户需要密码,那么使用``banned_email_file``里面的电子邮件地址的用户不能登录
- ``banned_email_file=/etc/vsftpd/banned_emails``禁止使用匿名用户登陆时作为密码的电子邮件地址
- ``chroot_list_enable=YES``如果启动这项功能,则所有列在chroot_list_file中的使用者不能更改根目录
- ``chroot_list_file=/etc/vsftpd/chroot_list``定义不能更改用户主目录的文件
- ``ls_recurse_enable=YES`` 是否能使用ls -R命令以防止浪费大量的服务器资源
- ``listen=YES ``绑定到listen_port指定的端口,既然都绑定了也就是每时都开着的,就是standalone模式(独立的sftpd服务器)
- ``pam_service_name=vsftpd ``定义PAM 所使用的名称,预设为vsftpd
- ``userlist_enable=YES ``若启用此选项,userlist_deny选项才被启动
- ``tcp_wrappers=YES ``开启tcp_wrappers支持

---

- 开启vnc远程控制可以使用通过``sudo raspi-config``进行设置
- 进入ftp服务器之后,需要定义本地的路径,使用``lcd``指令``lcd <目录>``
- 外接设备可以在``/media/pi/<设备名称>``里面寻找,使用路径打开之后便可以进行文件下载

---





