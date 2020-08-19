Linux 常用命令：

yum install lrzsz 安装 rz 命令

yum install -y unzip zip 安装 zip 命令

yum install fonts-chinese 安装中文包

rz 本机上传到服务器

rz -y 上传到服务器并覆盖

sz 服务器上文件下载到本地

解压：unzip FileName.zip

压缩：zip -r FileName.zip DirName

压缩当前的文件夹：zip -r ./FileName.zip ./\*

mv /data/html/3g-test.tuyoo.com/statics/images/4g/img/\_ . 移动 img 下所有文件到当前目录

mv /usr/lib/\_ /zone 是将 /usr/lib/下所有的东西移到/zone/中

mkdir DirName 创建文件夹

rm DirName 删除文件

rm -r 删除文件夹

rm -rf 直接删除文件夹及其下属内容

history | grep mysql
/后跟查找的字符串。vim 会显示文本中第一个出现的字符串。
?后跟查找的字符串。vim 会显示文本中最后一个出现的字符串
find / -name ajax\*newlist.php 全盘查找某个文件的位置，从根目录开始查
find / -name mysql -type d 查找文件夹 mysql
ll -t 查看文件按时间排序

mv /文件夹名/\* /新文件夹名

mv \_ 新文件夹路径 移动当前文件夹下所有到新目录下

mv 需要修改的名称 修改后的名称（用于单个文件名）

rename 修改多个文件名

vim /etc/nginx/conf.d/fx.ddzshare.conf 查看 Linux Nginx 配置
