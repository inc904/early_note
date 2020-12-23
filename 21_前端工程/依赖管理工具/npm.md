## npm使用

### node package manager 包管理工具

- (npm官方网站)[www.npmjs.com]
- 命令行工具 npm

#### 常用命令

- npm init 生成 package.json 文件。 -y 可以跳过向导，快速生成
- npm install package 下载包文件 --save 下载并保存依赖项，保存在 dependencies 对象 --save  简写 -S  install 简写 i
- npm install 下载恢复 包描述文件中的所有包文件
- npm uninstall package 删除包文件，但是依赖信息会被保存
- npm un --S package 删除包，并且删除依赖信息
- npm help 查看使用帮助
- npm i jquery@1.8.3 
  `@`标识安装指定版本 
- 参数
  + `-S`,`--save` 安装包信息将加入到 dependencies（生产阶段的依赖）
  + `-D`,`--save-dev` 安装包信息将加入到	devDependencies(开发阶段的依赖)，所以开发阶段一般使用它

### package.json & package-lock-json

npm5 之后才加入的lock文件。保存有依赖信息，和所有包的下载地址，重新下载安装的时候会更快。

npm5 之后 不用加 --save 参数，他自动会保存依赖文件

注意：
	package.json 文件中的版本号 都有一个 `^` 

	表示向后（新的）兼容，它只能锁住大版本，就是版本号的第一位，表示会下载当前大版本下最新的文件。
	
	package-lock.json 文件中，包的版本就是第一次装包的版本，完全一样，不会升级包。

### 换淘宝源

`$ npm install -g cnpm --registry=https://registry.npm.taobao.org`

### nrm 修改安装源

```shell
# 1.安装
npm i nrm -g
# 2.查看 源地址
nrm ls
# 3.使用/切换 源
nrm use xxx
```

### 常用命令

```shell
 -S, --save 安装包信息将加入到dependencies（生产阶段的依赖）
 -D, --save-dev 安装包信息将加入到devDependencies（开发阶段的依赖），所以开发阶段一般使用它
```

#### 单个包的管理
```shell	
# 查看 包的 信息
npm view testpackage versions
# 升级包
npm update testpackages
```