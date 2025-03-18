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

