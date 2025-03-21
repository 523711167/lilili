# create react app

## FAQ

###### create react app使用dart-sass

```shell
# npm > 6.9
npm install node-sass@npm:dart-sass
yarn add node-sass@npm:dart-sass
```

###### 解决The legacy JS API is deprecated and will be removed in Dart Sass 2.0.0

```json
#craco.config.js文件中添加配置
  style: {
    sass: {
      loaderOptions: {
        api: "modern"
      }
    }
  }
```

> [!CAUTION]
>
> 💡 配置后 webpack配置的别名使用无效。

###### webpack的调试测试

```
 # package.json文件中新增 --inspect-brk 表示启动调试模式，并且在启动首行自动打上断点
 "scripts": {
    "debug": "node --inspect-brk ./node_modules/webpack/bin/webpack.js --config ./webpack.config.js"
  }
  # 执行 yarn debug
  # 打开浏览器F12 ，点击左上角绿色图标，开启node.js调试
```

###### create react app配置代理服务



> [!CAUTION]
>
> 💡 如果通过引入@craco/craco，官网的参考方法失效，需要在craco.config.js文件中新增
>
>   devServer: {
>     proxy: {
>       '/api': {
>         target: 'http://localhost:28888',
>         changeOrigin: true,
>         pathRewrite: {
>           "^/api": ''
>         }
>       }
>     },
>   }