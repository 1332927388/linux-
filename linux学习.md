#终端快捷键：
    ctrl+b  光标向前移动
    ctrl+f  光标向后移动
    ctrl+h  删除光标前面的字符
    ctrl+d  删除光标所在字符
    ctrl+u  删除光标前的所有字符
    ctrl+a  光标索引到头部
    ctrl+e  光标索引到尾部
    ctrl+p  上一条命令
    ctrl+n  下一条命令
#目录结构：
    /bin: 是binary的缩写，这个目录存放着最经常使用的命令
    /boot: 存放的启动linux时的核心文件，包括一些文件以及镜像文件
    /dev: 是device的缩写，该目录下存放的都是linux的外部设备，在linux中访问设备的方式和访问文件的方式是相同的
    /etc: 用来存放所有的系统管理所需要的配置文件和子目录
    /home: 用户目录
    /lib: 存放着系统最基本的动态链接共享库，起作用类似于Windows里的dll文件，几乎所有的应用程序都需要用到这些共享库
    /lost+found: 一般是空的，当系统关机后，这里就存放了一些文件
    /opt: 给主机额外安装软件的目录，比如你安装一个Oracle数据库就可以放到这个目录下
    /root: 系统管理员，也称作为超级权限者的用户主目录
#目录快捷指令：
    cd ..   返回上一级目录
    cd -  返回上一个操作目录
    ls -a   列出当前目录的所有文件，包括隐藏文件
    ls -l   列出当前目的所有文件的属性
    ls -la   列出当前目录的所有文件的属性，包括隐藏文件
    mkdir  创建单级目录
    mkdir -p  创建多级目录
    rmdir 删除空目录
    rm    删除文件，但是不会进入回收站
    rm -r  删除目录，不会进入回收站
    rm -ri  删除时会出现提示
    touch   创建文件
    cat    查看文件
    cp    拷贝文件
    cp -r  拷贝目录
    mv   移动文件或改名字
    du -h  查看目录或文件大小
#查看和修改文件权限：
    chmod o+w file   添加写权限
    chmod +x  file   执行权限
#文件查找：
    find <direct> -name file   按名字查找
    find <direct> -size -(+)num   查找小于或大于num的文件
    grep -r(递归) <查找内容> <查找路径>  按文件内容查找
#deb包安装：
    sudo dpkg -i xxx.deb  安装
    sudo dpkg -r xxx  删除
#压缩包管理:

#进程管理:

1) gzip -- .gz格式压缩包，压缩后失去源文件
2) bzip2 -- .bz2格式压缩包，压缩后失去源文件
3) tar -- 不使用z/j参数，该命令只能对文件或目录打包 
    c--创建--压缩
    x--释放--解压缩
    v--显示提示信息--压缩解压缩--可以省略
    z--使用gzip的方式压缩文件--.gz
    j--使用bzip2的压缩方式压缩文件--.bz

    压缩：
        tar zcvf 生成的压缩包的名字(xxx.tar.gz) 要压缩的文件或目录
        tar jcvf 生成的压缩包的名字(xxx.tar.bz2) 要压缩的文件或目录
    解压缩：
        tar zxvf 压缩包名字 -C 解压目录
        tar jxvf 压缩包名字 -C 解压目录
4) rar 
    压缩： a
        rar a 生成的压缩文件的名字(temp) 压缩的文件或目录
    解压缩： x
        rar x 压缩文件名 解压缩目录
5) zip
    压缩： zip 压缩包的名字 压缩的文件或目录
            压缩目录需要加参数  -r
    解压缩: unzip 压缩包的名字
            unzip 压缩包的名字 -d 解压目录
#环境变量：
    env 查看环境变量
    linux下的环境变量的格式： key - value 
        key = value:value:value(可以对应多个value)
#任务管理器：
    top
#网络管理:
    查看ip：ifconfig
    检验是否练的同：ping 也可以ping网站(检验可不可以上网)
#用户管理：
    添加用户：
        sudo adduser + 用户名(why)
    切换用户：
        su 用户名
    删除用户：
        sudo deluser 用户名
#ftp服务器搭建: -- vsftpd
    作用：文件的上传和下载
    1) 服务器端：
        1) 修改配置文件:
         cd /etc 修改 vsftpd.conf 将“write_enable=YES”前面的#取消。


        2) 重启服务:
         sudo service vsftpd restart
    2) 客户端：
        1) 实名用户登录
         ftp + IP(service)
         输入用户名(service)
         输入密码

         文件的上传和下载：
            文件的上传： put file
            文件的下载： get file
            不允许操作目录，如果想操作目录 -- 打包 tar/rar/zip
        2) 匿名用户登录
         ftp + IP
         用户名：anonymous
         密码：  直接回车

         可以在服务器端创建一个专门给匿名用户使用的根目录
         修改配置文件vsftpd.conf 指定目录
        3) lftp客户端访问ftp服务器
         安装：sudo apt-get install lftp
         匿名用户: 1.lftp + IP
                  2.login
         实名用户：1.lftp username@ip 回车
                 2.输入服务器密码
         操作： put 上传文件
               mput 上传多个文件
               get  下载文件
               mget 下载多个文件
               mirror   下载整个目录及其子目录
               mirror -R 上传整个目录及其子目录
#nfs服务器搭建:
    1) 服务器端：
        1）创建共享目录
            mkdir dir
        2）修改配置文件
            /etc/exports
            加上   /home/user/dir *(rw,sync)
            共享dir自己创建，r表示读，w表示写，也可以ro表示只读，sync表示实时将内存中的数据写入到磁盘中
        3）重启服务
            sudo service nfs-kernel-server restart
    2）客户端：
        1）挂载服务器共享目录
            mount serverIP:dir /mnt
#ssh服务器:
    ssh username@IP 登录
    logout 退出
