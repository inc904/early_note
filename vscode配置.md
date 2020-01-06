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
      "prettier.singleQuote": true,
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
    "prettier.singleQuote": true,
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
        "editor.defaultFormatter": "esbenp.prettier-vscode",
    },
    "prettier.semi": false,
    "prettier.singleQuote": true,
    "window.zoomLevel": 0,
    "editor.formatOnSave": true,
    "workbench.iconTheme": "material-icon-theme",
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
        "editor.defaultFormatter": "esbenp.prettier-vscode",
    },
    "prettier.semi": false,
    "prettier.singleQuote": true,
    "window.zoomLevel": 0,
    "editor.formatOnSave": true,
    "workbench.iconTheme": "material-icon-theme",
    "open-in-browser.default": "Chrome",
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
    "editor.formatOnSave": true,
}
```

### 2020-01-02最舒服的配置

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
    "editor.fontFamily": "'Source Code Pro','Fira Code',Consolas, 'Courier New', monospace",
}
```

