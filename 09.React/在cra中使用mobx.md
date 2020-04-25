创建mobx 的demo，使用cra脚手架创建一个先项目后，然后安装mobx官网的步骤，报错`装饰器无法识别`。

[外文博客](https://swizec.com/blog/mobx-with-create-react-app/swizec/7158) 



### 安装装饰器解释器：

- 安装

  `npm install @babel/plugin-proposal-decorators`

- 配置，在 package.json 文件中

  ```json
    "babel": {
      "plugins": [
        [
          "@babel/plugin-proposal-decorators",
          {
            "legacy": true
          }
        ]
      ],
      "presets": [
        "react-app"
      ]
    },
  ```

  直接写不管用

  先git提交一次

  然后执行`npm run eject`

  之后再配置，🆗！

  参考CSDN 博客 ： https://blog.csdn.net/weixin_44369568/article/details/90270290