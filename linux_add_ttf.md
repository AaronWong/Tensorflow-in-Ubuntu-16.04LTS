1. 首先获得一套“微软雅黑”字体库（Google一下一大把），包含两个文件msyh.ttf（普通）、msyhbd.ttf（加粗）；   

2. 在/usr/share/fonts目录下建立一个子目录，例如win，命令如下：
    # mkdir /usr/share/fonts/win
    
3. 将msyh.ttf和msyhbd.ttf复制到该目录下，例如这两个文件放在/root/Desktop下，使用命令：
    # cd /root/Desktop
    # cp msyh.ttf msyhbd.ttf  /usr/share/fonts/win/
    
4. 建立字体缓存

    cd /usr/share/fonts/win
    sudo mkfontscale
    sudo mkfontdir
    sudo fc-cache -fv
