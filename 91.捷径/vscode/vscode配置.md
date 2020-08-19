## 安装插件：

- atom one dark theme
- atom one light theme
- Chinese
- css formatter
- document this
- ESLint
- live server
- open in browser
- prettier -Code formatter
- vetur
- vue 2 Snippets

## 安装字体：

`Fira Code`

## 编辑器配置文件
参考网址：`https://www.cnblogs.com/RandyField/p/12873538.html`

```json
{
  "javascript.format.semicolons": "remove",
  "typescript.format.semicolons": "remove",
  "prettier.semi": false,
  "prettier.singleQuote": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  // vscode默认启用了根据文件类型自动设置tabsize的选项
  "editor.detectIndentation": false,
  "editor.tabSize": 2,
  "eslint.autoFixOnSave": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "vue",
      "autoFix": true,
      "prettier.semi": false,
      "prettier.singleQuote": true
    }
  ],

  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force-aligned"
    },
    "prettier": {
      "semi": false,
      "singleQuote": true
    }
  },
  "editor.fontFamily": "'Fira Code',Consolas, 'Courier New', monospace",
  "editor.fontSize": 16,
  "editor.lineHeight": 32,
  "workbench.colorTheme": "Atom One Dark"
}
```

```json
{
  "prettier.semi": false,
  "prettier.singleQuote": true
}
```

### new config 20191221

```json
{
  "workbench.colorTheme": "One Dark Pro",
  "editor.fontFamily": "'Fira Code', Consolas, 'Courier New', monospace",
  "editor.fontLigatures": true, // 启用连体字
  "editor.fontSize": 16,
  "editor.tabSize": 2,
  "editor.lineHeight": 28,
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "prettier.semi": false,
  "prettier.singleQuote": true,
  "window.zoomLevel": 0,
  "editor.formatOnSave": true,
  "workbench.iconTheme": "material-icon-theme"
}
```

```json
{
  "workbench.colorTheme": "One Dark Pro",
  "editor.fontFamily": "'Fira Code', Consolas, 'Courier New', monospace",
  "editor.fontLigatures": true,
  "editor.fontSize": 16,
  "editor.tabSize": 2,
  "editor.lineHeight": 28,
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "prettier.semi": false,
  "prettier.singleQuote": true,
  "window.zoomLevel": 0,
  "editor.formatOnSave": true,
  "workbench.iconTheme": "material-icon-theme",
  "open-in-browser.default": "Chrome"
}
```

### 20191224

```json
{
  "javascript.format.semicolons": "remove",
  "typescript.format.semicolons": "remove",
  "prettier.semi": false,
  "prettier.singleQuote": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.detectIndentation": false,
  "editor.tabSize": 2,
  // "eslint.autoFixOnSave": true,
  // "eslint.validate": [
  //     "javascript",
  //     "javascriptreact",
  //     {
  //         "language": "vue",
  //         "autoFix": true,
  //         "prettier.semi": false,
  //         "prettier.singleQuote": true,
  //     }
  // ],
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force-aligned"
    },
    "prettier": {
      "semi": false,
      "singleQuote": true
    }
  },
  "editor.fontFamily": "'Fira Code',Consolas, 'Courier New', monospace",
  "editor.fontSize": 16,
  "editor.lineHeight": 32,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.formatOnSave": true
}
```

### 2020-01-02 最舒服的配置

```json
{
  "javascript.format.semicolons": "remove",
  "typescript.format.semicolons": "remove",
  "prettier.semi": false,
  "prettier.singleQuote": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.detectIndentation": false,
  "editor.tabSize": 2,
  "javascript.format.insertSpaceBeforeFunc  tionParenthesis": true,
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force-aligned"
    },
    "prettier": {
      "semi": false,
      "singleQuote": true
    }
  },
  "editor.fontSize": 18,
  "editor.lineHeight": 34,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.formatOnSave": true,
  "window.zoomLevel": 0,
  "editor.minimap.enabled": true,
  "editor.renderControlCharacters": false,
  "editor.renderWhitespace": "none",
  "editor.fontLigatures": true,
  "terminal.integrated.rendererType": "dom",
  "workbench.colorTheme": "One Monokai",
  "editor.fontFamily": "'Source Code Pro','Fira Code',Consolas, 'Courier New', monospace"
}
```

# vscode 报错，不符和 eslint 规范，保存时单引号变双引号，代码尾部分号和逗号自动去除

在项目根目录下新建.prettierrc（prettier 插件的配置文件）文件，在文件中写入

```json
{
  "semi": true, //在代码尾部添加分号
  "singleQuote": true, //把双引号换成单引号
  "trailingComma": "es5" //在代码尾部添加逗号
}
```

在.eslintrc.js（eslint 插件的配置文件）文件中的 rules 属性中添加

```js
'no-unused-vars': 'warn',//把该条提示信息转换成警告信息
```

## 2020年7月15日 配置
```json
{
  // VScode主题配置
  "editor.tabSize": 2,
  "editor.lineHeight": 24,
  "editor.renderLineHighlight": "all",
  "editor.renderWhitespace": "none",
  "editor.fontFamily": "Fira code",
  "editor.fontSize": 15,
  "editor.cursorBlinking": "smooth",
  "editor.multiCursorModifier": "ctrlCmd",
  "editor.wordWrap": "off", // 永不换行
  "editor.wordWrapColumn": 400, // 当一行的字符超过400个，进行换行
  "prettier.semi": false, // prettier 设置语句末尾加分号 true 加分号 false 不加分好
  "prettier.singleQuote": true,
  // 主题
  "workbench.iconTheme": "vscode-great-icons",
  "workbench.startupEditor": "newUntitledFile",
  "workbench.colorTheme": "Atom One Dark",
  "workbench.colorCustomizations": {
    "editorIndentGuide.activeBackground": "#1cb9ac" // 设置guide线高亮颜色,可以改为自己喜欢的颜色
  },
  "editor.snippetSuggestions": "top", // 代码提示。许多插件都有代码提示，代码缩写提示优先显示在最上方。
  "editor.quickSuggestions": {
    // 是否显示可能用到的示例代码.安装插件过多，建议选项也会非常多
    "other": true,
    "comments": true,
    "strings": false
  },
  "editor.formatOnPaste": true, // 粘贴的内容, 是否自动格式化
  "editor.formatOnSave": true, // 保存文件时，则自动格式化 （注意：如果此条规则开启，那么 { codeActionsOnSave source.fixAll }则应该设置为关闭，否则在文件保存时，会被自动格式化两次,没有必要）
  "editor.codeActionsOnSave": {
    "source.organizeImport": true,
    "source.fixAll": false, // 对所有文件，保存时自动格式化
    "source.fixAll.eslint": false, // 定制. 也可以在文件保存时，禁用eslint规则生效
    "source.fixAll.tslint": false,
    "source.fixAll.stylelint": false
  },
  // css2rem插件: 书写css时，px单位自动提示转换为rem单位
  // 此处根字体大小设置为100（默认为16）
  // "cssrem.rootFontSize": 100,
  // 设置终端的命令工具，比如我用到了 cmder，那么可以把这里的地址改为电脑cmder的安装位置
  // 强烈推介终端启动快捷键:  ctrl + C
  "terminal.integrated.shell.windows": "C:\\windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  "workbench.editor.limit.enabled": true, // 是否限制每一个VSCODE窗体内显示的编辑器窗体数量（默认为关闭）。
  "workbench.editor.limit.perEditorGroup": true, // 是对打开的所有VSCODE窗体进行限制还是只对当前VSCODE窗体限制
  "workbench.editor.limit.value": 8, // 打开的编辑器的最大数量（默认为10个）
  "javascript.updateImportsOnFileMove.enabled": "always", // 移动文件或者修改文件名时，是否自动更新引用到自此文件的所有文件。
  "javascript.implicitProjectConfig.experimentalDecorators": true, // 对于非js文件，是否自动启用一份默认的ts配置
  "[html]": {
    // 对html文件，使用 vscode.html-language-features(HTML语言功能) 进行格式化
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[vue]": {
    // 对vue文件，使用 vetur插件内置的默认风格 进行格式化
    "editor.defaultFormatter": "octref.vetur"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[less]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[scss]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    // 对json文件，使用 JSON语言功能 进行格式化
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "[markdown]": {
    // 对md文件，使用 Prettier 进行格式化
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "breadcrumbs.enabled": true, // 启用/禁用顶部面包屑导航（可以直接跳转文件）
  "open-in-browser.default": "chrome", // 配置打开html文件的默认浏览器
  "search.exclude": {
    // VScode进行文件搜索时，不搜索这些区域。注意：vs已经贴心默认设置了 node_modules 和 bower_components 文件夹，所以这里没有加进去
    "**/.git": true,
    "**/.gitignore": true,
    "**/.svn": true,
    "**/.DS_Store": true,
    "**/.idea": true,
    "**/.vscode": false,
    "**/yarn.lock": true,
    "**/tmp": true,
    "**/dist": true,
    "**/build": true
  },
  // 配置文件关联
  "files.associations": {
    // 比如小程序中的 .wxss 这种文件，会把它作为css文件来处理，提供对应的css的语法提示，css的格式化等。
    "*.wxss": "css",
    "*.cjson": "jsonc",
    "*.wxs": "javascript",
    "*.ts": "typescript",
    "*.vue": "vue",
    "*.dart": "dart"
  },
  // vscode已经内置了emmet。配置emmet是否启用tab展开缩写
  // 这一设置最大作用是：当输入的文本不属于Emmet定义的缩写规则时，依然允许使用Tab键进行缩进。此时会提示我自定义的缩写语句，以及各插件自定义的缩写语句.
  "emmet.triggerExpansionOnTab": true,
  "emmet.showSuggestionsAsSnippets": true, // 是否启用emmet代码提示
  "emmet.syntaxProfiles": {
    // 配置emmet对哪种文件类型支持
    "vue-html": "html",
    "vue": "html",
    "javascript": "javascriptreact",
    "xml": {
      "attr_quotes": "double"
    }
  },
  "emmet.includeLanguages": {
    "wxml": "html",
    "vue-html": "html",
    "javascript": "javascriptreact",
    "jsx-sublime-babel-tags": "javascriptreact", // 在 react 的jsx中添加对emmet的支持
  },
  // 介格式化快捷键: shirt+alt+F，有时可能需要多按几次
  // 使用 shirt+alt+F进行格式化时，先执行编辑器的格式化规则，然后才会按照 eslint 和 tslit 等其他插件去格式化。
  // 是否 开启 eslint代码规范检测 (与后面的tslint选择开启一种即可)
  "eslint.enable": true,
  "eslint.format.enable": true, // 是否 根据自己配置的 eslint配置文件, 对代码进行格式化
  "eslint.options": {
    // eslint配置文件 ,修改为你自己电脑上的文件位置，或者直接删除
    "configFile": "D:/worksapce/youxiang-mobile-master/.eslintrc.js",
    "plugins": [
      "html"
    ]
  },
  "eslint.validate": [
    // eslint规则对以下几种后缀文件生效
    "javascript",
    "javascriptreact",
    "html",
    "typescript",
    "typescriptreact"
  ],
  "typescript.validate.enable": false, // 是否开启 tslint代码规范检测
  "[typescript]": {
    // 对ts文件进行格式化时，使用哪一种风格 (此处使用的是vscode中安装的ts插件默认风格进行格式化)
    "editor.defaultFormatter": "vscode.typescript-language-features"
  },
  "git.autofetch": true, // 在push代码时，是否先自动从远端拉取代码
  "debug.openDebug": "openOnDebugBreak", // 断点调试时，遇到断点，自动显示调试视图。（全局的，不可为每种语言单独配置）
  "minapp-vscode.disableAutoConfig": true,
  "[jsonc]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  // vetur 的自定义设置
  "vetur.format.defaultFormatterOptions": {
    "prettier": {
      "singleQuote": true,
      "semi": false
    }
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```