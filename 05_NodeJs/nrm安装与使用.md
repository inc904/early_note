## 一、什么是nrm

nrm 是一个 npm 源管理器，允许你快速地在 npm源间切换。

什么意思呢，npm默认情况下是使用npm官方源（使用npm config ls命令可以查看），在国内用这个源肯定是不靠谱的，一般我们都会用淘宝npm源：https://registry.npm.taobao.org/，修改源的方式也很简单，在终端输入：



```
npm set registry https://registry.npm.taobao.org/
```

再npm config ls查看，已经切换成功。

那么，问题来了，如果哪天你又跑去国外了，淘宝源肯定是用不了的，又要切换回官网源，或者哪天你们公司有自己的私有npm源了，又需要切换成公司的源，这样岂不很麻烦？于是有了[nrm](https://github.com/Pana/nrm)。

##  二、nrm安装



```
npm install -g nrm
```

## 三、nrm使用

### 1、查看可选源（带\*号即为当前使用源）



```
nrm ls
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117094827805-1993749254.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117094827805-1993749254.png)

### 2、查看当前使用源**



```
nrm current
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117094941998-2072280887.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117094941998-2072280887.png)

### 3、切换源**



```
nrm use <registry>
```

其中，registry为源名。

比如：切换为taobao源



```
nrm use taobao
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117095208151-1320241377.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117095208151-1320241377.png)

### 4、添加源**



```
nrm add <registry> <url>
```

其中，registry为源名，url为源地址。

比如：添加一个公司私有的npm源，源地址为：http://192.168.22.11:8888/repository/npm-public/，源名为cpm（随意取）。



```
nrm add cpm http://192.168.22.11:8888/repository/npm-public/
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100125123-1616690533.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100125123-1616690533.png)

然后，查看是否添加成功

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100220997-1674826452.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100220997-1674826452.png)

### 5、删除源**



```
nrm del <registry>
```

其中，registry为源名。

比如：删除刚才添加的cpm源



```
nrm del cpm
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100608225-1693739675.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117100608225-1693739675.png)

### 6、测试源速度（即响应时间）



```
nrm test <registry>
```

其中，registry为源名。

比如：测试官方源和淘宝源的响应时间



```
nrm test npm
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117101055360-1808995045.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117101055360-1808995045.png)



```
nrm test taobao
```

[![img](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117101134977-239814426.png)](https://img2018.cnblogs.com/blog/1244179/201901/1244179-20190117101134977-239814426.png)

 