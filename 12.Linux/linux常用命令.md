windows下和Linux下命令行常用命令明细

| Linux          | Windows | 用途               | 备注             |
| -------------- | ------- | ------------------ | ---------------- |
| ls -l          | dir     | 查看当前目录中文件 | ls可查看文件属性 |
| cp             |         | 复制文件到制定路径 |                  |
| which、whereis | where   |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |
|                |         |                    |                  |

### 下面是red hat/CentOs7关闭防火墙的命令!

1:查看防火状态

systemctl status firewalld

service iptables status

2:暂时关闭防火墙

systemctl stop firewalld

service iptables stop

3:永久关闭防火墙

systemctl disable firewalld

chkconfig iptables off

4:重启防火墙

systemctl enable firewalld

service iptables restart

## 编辑

vi有两个模式：一个是编辑一个是命令。我们从命令进入编辑为：i，o，a。一般使用的是i：因为这个我是最熟悉的。退出点击esc键，就进入命令模式。

我们需要删除文件的当前行和后一行，命令为：2dd，一般我们使用的是单个字符的删除为：x。我们一般进入编辑模式，来进行添加，修改，删除。

但是当我们删除和修改的内容过多的时候，我们使用命令行模式，进行修改，这样方便，快捷，而命令行中，最常用到的是x，dd，u，p这四个命令：

x:删除当前字符;

dd：删除当前行;

u:恢复前一步操作;

p:复制之前删除的行。





vi是Linux终端下或控制台下常用的编辑器，基本的操作方式为：vi /路径/文件名

　　例如，vi /etc/saikik表示显示/etc/saikik文件的内容。使用键盘上的Page Up和Page Down键可以上下翻页;按下Insert键，可以见到窗口左下角有“Insert”字样，表示当前为插入编辑状态，这时从键盘输入的内容将插入到光标位置;再按下Insert键，左下角将有“Replace”字样，表示当前为替换编辑状态，这时从键盘输入的内容将替换光标位置的内容。编辑完内容后，按下Esc键，并输入“:wq”，然后回车就可以保存退出。

　　如果不想保存而直接退出，则按下Esc键后，输入“:q!”，然后回车即可。“wq”表示Write和Quit，即保存退出;“q!”表示忽略修改强行退出。





## 11

通过命令查看当前监听的端口及状态：

netstat -na|grep 8080