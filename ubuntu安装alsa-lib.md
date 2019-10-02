#ubuntu安装ALSA库-alsa-lib
###1. 在编译讯飞的语音识别代码时候，发现缺少alsa库，编译报错如下： 
linuxrec.c:12:28: fatal error: alsa/asoundlib.h: 没有那个文件或目录 #include <alsa/asoundlib.h> 
###2. 由于录音是采用linux的ALSA库，因此需要安装该库。 
###3. 安装方法： 
3.1、到ALSA的官网下载库文件，ALSA库下载链接 
3.2、下载完放到ubuntu下进行解压缩，进入alsa-lib-1.1.5文件夹，按照linux安装三步曲进行安装即可。
3.3、首先执行 ./configure 进行配置 
3.4、执行 make 进行编译，编译成功之后执行 make install 进行安装。