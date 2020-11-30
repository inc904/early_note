## vue中使用swiper出现Can't resolve 'swiper/dist/css/swiper.css'

我遇到的问题，总的来说是找不到css文件。

背景是：时间：2020/11/14,我安装`vue-awesome-swiper`,使用的是：
```bash
npm install  vue-awesome-swiper --save
```
### 缘由：
我查看 package.json 看到`"vue-awesome-swiper": "^4.1.1",`,于是在swiper官网 跳转的github，选择了
`Swiper4`的文档，文档中提供的安装命令就是上面的。

百度的过程中看到有说安装`vue-awesome-swiper`,会自动安装`swiper`,查看package.json后发现，并没有安装
`swiper`。

swiper 官网直接跳转的github和npm.js上有说需要安装两个包。

安装完`swiper`后，引入`swiper.css`失败，引入`swiper-bundle.css`成功。


### 处理
安装`swiper  vue-awesome-swiper`两个。
```bash
npm install swiper  vue-awesome-swiper --save
```

时间原因，没有深入。

### 总结

装包的时候，查看所装包对应的文档。配合npm.js和github两个平台的官方文档，好一些。