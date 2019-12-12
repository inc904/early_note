## JSX

HTML 语言直接写在 JavaScript 语言中，不写任何引号，这就是 JSX 语法。它允许 HTML和 JavaScript 混写。

### 环境配置

- 非模块化环境
  - `babel-standalone`
  - 执行时编译，比较慢，只适用于开发测试环境
- 模块化环境
  - `babel-prese-react`
  - 结合 webpack 配置相应的工具
  - 浏览器执行的是预编译结果
- Bebal REPL赋值 查看编译结果
  - 适用于在线测试

### 基本语法

- 有且仅有一个根节点
- 多标签写在一个 小括号中
- 遇到 HTML 标签（以`<`开头）就用HTML规则解析
  - 单标签不能省略结束标签
- 遇到代码块（以`{`开头）就用 JavaScript 规则解析
- JSX 允许直接在模版中插入一个 JavaScript 变量
  - 如果这个变量是一个数组，则会展开这个数组的所有成员添加到模版中
- 单标签必须结束`/>`
  - `<img  />`、`<input />`

### 在JSX中嵌入JavaScript 表达式



