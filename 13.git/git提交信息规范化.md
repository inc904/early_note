## Git 提交信息规范化
### Git 版本规范
#### 分支
- master 分支为 主分支（保护分支），不能直接在 master 分支上进行代码的修改和提交。
- develop 分支 为 测试分支，所以开发完成需要提交测试的功能合并到该分支。
- feature 分支 为 开发分支，大家根据不同需求创建独立的功能分支，开发完成后合并到 develop 分支。
- fix 分支 为 bug修复分支，需要根据实际情况对已发布的版本进行漏洞修复。

#### Tag 
采用三段式，v 版本.里程碑.序号，如 v1.2.1
- 架构升级或架构重大调整，修改第二位
- 新功能上线或者模块的重大调整，修改第二位
- bug 修复上线，修改第三位

### git提交信息
commit message 一般包括三部分：Header、Body、Footer

#### Header
- type：用于说明 commit 的类别
	- feat：新增功能
	- fix：修复Bug
	- docs： 修改文档
	- refactor： 代码重构，未增加任何新功能和修复任何 bug
	- bulid：该百年构建流程、新增依赖库、工具等（例如 webpack 修改）
	- style：仅仅修改了空格缩进、缩进等，不改变代码逻辑
	- pref：改善性能和体现的修改
	- chore：非 src 和 test 的修改
	- ci：自动化流程配置修改
	- revert： 回滚到上一个版本
- scope： 可选，用于说明 commit 的影响范围
- subject： commit 的简要说明，尽量简短


- 关键字
 - bugfix：表示修复 bug
 - feature：新增功能
 - add：增加类、文件、代码块等
 - delete：对代码块、功能的更新
 - refactor：对代码块、功能重构
 - arch：输出中间版本，用于测试
 - release to v1.0.0 表示打包输出的版本号

#### Body
对本次 commit 的详细描述，可分多行

#### Footer
- 不兼容变动：需要描述相关信息
- 关闭指定 issue：输入issue信息