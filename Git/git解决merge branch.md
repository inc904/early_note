

[git解决merge branch -- csdn](https://blog.csdn.net/wm5920/article/details/79731983)

[Git push 时如何避免出现 "Merge branch 'master' of ..."](https://www.cnblogs.com/Sinte-Beuve/p/9195018.html)

#### 项目结构：

README.md

t.js

#### 操作人：

用户 a 和用户 b

### 场景一：没有冲突文件

1. a 修改了 t.js， commit（msg 为 a1 ）, push成功

2. b 修改了 README.md ， commit （msg 为 b1 ）成功， push 失败，pull 成功，此时 git 记录会多出现 `merge branch` 记录，如下图

![这里写图片描述](https://img-blog.csdn.net/20180328183239561?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![这里写图片描述](https://img-blog.csdn.net/2018032818330340?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

#### 如何解决merge branch ？

b在push失败的时候，先pull，然后 `force rebase` 即可解决

##### Git rebase详细解析  ：

#####   https://blog.csdn.net/wangnan9279/article/details/79287631

![这里写图片描述](https://img-blog.csdn.net/20180328183312811?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180328183324789?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![这里写图片描述](https://img-blog.csdn.net/20180328183334896?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 场景二： 存在冲突文件

1.a修改了t.js和README.md,commit(commit msg 为 a3),push成功
2.b修改了t.js,commit成功(commit msg 为 b3)，push失败，pull失败，本地解决冲突文件（windows下，pull失败会提示修改冲突部分如下图一，然后点击yes出现下图二或者commit，查看冲突,出现下图二，非相关代码README.md不用处理，不要revert或者resolve conflict using mine，否则会覆盖别人代码），再commit,push即可
此时服务器有两次commit记录

![这里写图片描述](https://img-blog.csdn.net/20180328183344109?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180328183353898?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180328183405392?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180328183720697?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

服务器记录如下

![这里写图片描述](https://img-blog.csdn.net/20180328183727427?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dtNTkyMA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)