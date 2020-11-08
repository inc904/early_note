直接使用人家构建好的镜像

下载镜像
```bash
docker pull binaryify/netease_cloud_music_api
```
启动镜像

```bash
docker run -d -p 3000:3000 --restart=always --name netease_cloud_music_api    binaryify/netease_cloud_music_api
```

 

 

下载node镜像 
```bash
docker pull node
```
创建数据卷
```bash
docker volume create node
```
创建文件夹
```bash
mkdir -p /var/lib/docker/volumes/node/_data/MusicApi
```
api服务器的github地址：https://github.com/Binaryify/NeteaseCloudMusicApi

下载zip包：https://github.com/Binaryify/NeteaseCloudMusicApi/releases

解压缩后，通过本地的node执行npm install将对于的模块下载下来，然后将所有文件压缩成zip包，上传服务器，并且解压缩到`/var/lib/docker/volumes/node/_data/MusicApi/MusicApi  `

启动容器 
```bash
docker run -it -d --rm --name musicApi -v node:/usr/src/app  --network=host node node /usr/src/app/MusicApi/app.js
```

[参考](https://blog.csdn.net/qq_41813208/article/details/106031206?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160470655119724838536503%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=160470655119724838536503&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v28-1-106031206.pc_search_result_cache&utm_term=%E7%BD%91%E6%98%93%E4%BA%91%E9%9F%B3%E4%B9%90&spm=1018.2118.3001.4449)