### Linux 目录
- **/** 根目录
- **/etc** 系统配置文件存放目录
- **/usr** 应用程序存放目录
- **/root** 系统管理员root的家目录 

### Linux 命令
- 目录
    - **ls** 查看目录下文件
        - **-a** 查看隐藏文件
        - **-l** 详细列表 开头: d 目录,-普通文件,l链接
        - **-h** 友好显示列表
        - **-t** 
        - **-r** 
    - **ll** 查看详细详细
- **mkdir** 创建文件夹
    - **-p** 父目录不存在先创建父目录
- 查看文件
    - **head -2 [file]** 查看一个文件的前两行 
    - **tail -2 [file]** 查看一个文件的最后两行 
    - **tail -f [file]** 实时查看被添加到一个文件中的内容
    - **cat [file]** 从第一个字节开始正向查看文件的内容，直接输出文件所有内容
    - **tac [file]** 从最后一行开始反向查看一个文件的内容，直接输出文件所有内容
    - **more [file]** 查看一个长文件的内容
    - **less [file]** 查看一个长文件的内容，允许在文件中和正向操作一样的反向操作
        - **-m** 显示百分比
        - **-N** 显示行号
        - **/[string]** 向下查找匹配字符串,**n** 向下查找下一个匹配字符串,**N**向上查找上一个匹配字符串
        - **?[string]** 向上查找匹配字符串,**n**向上查找上一个匹配字符串,**N**向下查找下一个匹配字符串
        - **g** 跳到首页
        - **G** 跳到尾页
- **cp -r** 复制目录
- **find [目录] -name [文件名]**
- **grep**
    - **-i** 忽略大小写
    - **[命令] | grep [参数]** 对前面命令的结果进行搜索
    - **-v** 反向搜索 不包含某字符串
- **tar** 压缩
    - **-zxvf []** 压缩
    - **-zcvf []** 解压
    - **-zcvf [] -C []** 解压到目录
- **setup** 网络设置
- **chmod** 给文件修改权限
![image](//note.youdao.com/yws/res/2051/WEBRESOURCEdb0b4177ce452af7f28736b27826f26d)
    - **+** 添加某个权限
    - **-** 取消某个权限
    - **=** 赋予给定权限并取消其他所有权限(如果有的话)
    - **r** 可读
    - **w** 可写
    - **x** 可执行,只有目标文件对某些用户是可执行的或该目标文件是目录时才追加x 属性
    - **s** 在文件执行时把进程的属主或组ID置为该文件的文件属主。方式“u＋s”设置文件的用户ID位，“g＋s”设置组ID位
    - **t** 保存程序的文本到交换设备上
　　- **u** 与文件属主拥有一样的权限,所属用户 eg. chmod u=rwx [文件名]
    - **g** 与和文件属主同组的用户拥有一样的权限,所属组
    - **o** 与其他用户拥有一样的权限
- xargs 命令
    > 捕获一个命令的输出，然后传递给另外一个命令
- awk 打印
    > awk '{print $2}'   一行一行的读取指定的文件，以空格作为分隔符，打印第二个字段
- 安装sz,rz 
    - wget http://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
    - tar zxvf lrzsz-0.12.20.tar.gz && cd lrzsz-0.12.20
    - ./configure && make && make install
    - 上面安装过程默认把lsz和lrz安装到了/usr/local/bin/目录下，现在我们并不能直接使用，下面创建软链接，并命名为rz/sz：
    - cd /usr/bin
    - ln -s /usr/local/bin/lrz rz
    - ln -s /usr/local/bin/lsz sz
    - yum 安装 yum install lrzsz
- 安装vim
    > yum -y install vim*

    - 设置vim编辑环境有两种形式：
        - 一种是在/etc/vimrc进行设置，这种设置方法会作用与所有登录到Linux环境下的用户，一般情况下我们不提倡这种方式，因为Linux是多用户的，每个人都有自己的编程习惯与环境，因此我们提倡下面一种设置方式。
        - 另一种：是在用户登录的~目录下创建一个 .vimrc文件，在其中进行自己习惯的编程环境的设置，这样当别的用户使用时并不相互影响。
        > - 具体方法：  
        >   - cd ~
        >   - touch .vimrc
        >   - vim .vimrc
        >   - 在文件中输入:
        
```
set nu // 这是设置显示行号
set showmode // 设置在命令行界面最下面显示当前模式等。
set ruler // 在右下角显示光标所在的行数等信息
set autoindent // 设置每次单击Enter键后，光标移动到下一行时与上一行的起始字符对齐
syntax on // 即设置语法检测，当编辑C或者Shell脚本时，关键字会用特殊颜色显示
```
- vim 命令
    > 1. 删除包含something的所有行<br>
    > :g/something/d <br />
    > 2. 去除高亮 <br />
    > :noh
    > 3. 替换光标所在行的第一个匹配串<br />
    > :s/old/new
    > 4. 替换光标所在行的所有匹配串<br />
    > :s/old/new/g
    > 5. 替换指定行区间的匹配串，其中#,#代表的是替换操作的若干行中首尾两行的行号<br />
    > :#,#s/old/new/g
    > 6. 替换整个文件中每行的第一个匹配串<br />
    > :%s/old/new
    > 7. 替换整个文件中的每个匹配串<br />
    > :%s/old/new/g
    > 8. 会找到整个文件中的每个匹配串，并且对每个匹配串提示是否进行替换<br />
    > :%s/old/new/gc
- 安装python
    - 可利用linux自带下载工具wget下载，如下所示：wget http://www.python.org/ftp/python/3.3.0/Python-3.3.0.tgz
    - 解压 **tar -xzvf Python-3.3.0.tgz**
    - 进入解压缩后的文件夹 **cd Python-3.3.0**
    - 在编译前先在/usr/local建一个文件夹python3（作为python的安装路径，以免覆盖老的版本）**mkdir /usr/local/python3**
    - **./configure --prefix=/usr/local/python3**
    - 上一步如果报错
        > 1. **configure: error: no acceptable C compiler found in $PATH**
        > 2. 说明没有安装合适的编译器。这时，需要安装/升级 gcc 及其它依赖包
        > 3. yum install make gcc gcc-c++
    - **make** 编译
    - **make install** 安装
    - 此时没有覆盖老版本，再将原来/usr/bin/python链接改为别的名字**mv /usr/bin/python /usr/bin/python_old2**
    - 再建立新版本python的链接**ln -s /usr/local/python3/bin/python3 /usr/bin/python**
    - 解决yum不能用的问题
    > 修改/usr/bin/yum的第一行为：**#!/usr/bin/python_266**就可以了

- shadowsocks 安装
    - wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
    - chmod +x shadowsocks.sh
    - ./shadowsocks.sh 2>&1 | tee shadowsocks.log
    - 输入密码端口等
    - shadowsocks 启动,关闭
    - shadowsocks.json **eg.**
```
{
    "server":"0.0.0.0", // 监听ip
    "server_port":10454, // 链接端口
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"password",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false
}
```
    > ssserver -c /etc/shadowsocks.json -d start
    > ssserver -c /etc/shadowsocks.json -d stop

- 锐速加速安装
    - 使用锐速的前提条件：
    > 1. 服务器的虚拟化架构必须是KVM或者是XEN的，如果是OPENVZ架构则不支持使用锐速
    > 2. 锐速的安装使用需要匹配Linux的内核版本，其中多数CentOS版本需要重新安装适合的内核
    > 3. 关于虚拟化架构的问题如果你不知道自己服务器使用的是什么架构那么可以使用检测工具
    > 4. 如果CentOS版本遭遇内核问题无法安装还可以进行更换内核以便于适用于锐速的安装和使用
```
// 通过SSH连接服务器后执行上述命令即可显示你的服务器虚拟化架构是什么
wget -c https://dl.lancdn.com/landian/tools/vm_check/vm_check.sh && bash vm_check.sh

// 先更新下然后安装网络工具包（不论什么版本都必须安装工具包）
yum install upgrade
yum install net-tools

// 如果你是 CentOS 6.x 版本请在SSH连接服务器后执行以下命令：
rpm -ivh https://dl.lancdn.com/landian/Kernel/CentOS/6.x/kernel-firmware-2.6.32-504.3.3.el6.noarch.rpm
rpm -ivh https://dl.lancdn.com/landian/Kernel/CentOS/6.x/kernel-2.6.32-504.3.3.el6.x86_64.rpm --force

// 如果你是 CentOS 7.x 版本请在SSH连接服务器后执行以下命令：
rpm -ivh https://dl.lancdn.com/landian/Kernel/CentOS/7.x/kernel-3.10.0-229.1.2.el7.x86_64.rpm --force

//执行完成后请执行以下命令查看内核是否安装成功：
//若安装成功则会在输出的所有内核版本里显示我们刚刚安装的2.6或者3.1版
rpm -qa | grep kernel

//如果已经显示安装成功则重启服务器然后再次查看是否正常：
reboot
uname -r

//通过SSH连接服务器后执行以下命令进行自动化安装：
wget http://dl.lancdn.com/landian/tools/serverspeeder.sh && bash serverspeeder.sh
```

- 常用命令
    - service serverSpeeder status     <==检查锐速状态
    - service serverSpeeder stop       <==停止锐速
    - service serverSpeeder start      <==开启锐速
    - service serverSpeeder restart    <==重启锐速
- 卸载
> chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f

### 防火墙
- 新增端口开放
> OS 6 <br>
> **iptables -I INPUT -m state --state NEW -m tcp -p tcp --dport ${port} -j ACCEPT**<br>
> **iptables -I INPUT -m state --state NEW -m udp -p udp --dport ${port} -j ACCEPT**<br>
> **/etc/init.d/iptables save**<br>
> **/etc/init.d/iptables restart**<br>
> OS 7<br>
> **firewall-cmd --permanent --zone=public --add-port=${port}/tcp**<br>
> **firewall-cmd --permanent --zone=public --add-port=${port}/udp**<br>
. **firewall-cmd --reload**<br>
- 开放的端口位于 **/etc/sysconfig/iptables** 中

### 设置
- 操作系统默认 240 秒后，才会关闭处于 time_wait 状态的连接，在高并发访问下，服
务器端会因为处于 time_wait 的连接数太多，可能无法建立新的连接，所以需要在服务器上
调小此等待值。
> 在 linux 服务器上请通过变更 /etc/sysctl.conf 文件去修改该缺省值（秒）：  
> net.ipv4.tcp_fin_timeout = 30

### 定时任务 **crontab**
> crontab –e : 修改 crontab 文件.如果文件不存在会自动创建<br /> 
> crontab –l : 显示 crontab 文件<br />
> crontab -r : 删除 crontab 文件<br />
> crontab -ir : 删除 crontab 文件前提醒用户
