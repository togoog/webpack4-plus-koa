# Webpack4 plus koa

> 使用webpack4.8+、koa2构建的 Node服务端渲染项目，集成react和vue.

## 打包构建

### 配置项

实际运行的配置为`config.default.js` + `config.${process.env.APP_ENV}.js`

### 多页面入口

页面入口为`src/page/**/index.js`

html入口为`src/page/**/index.html` 或者 `src/entry/layout.html`

## Node服务模块

借鉴egg的 `约定优于配置` 设计思想，
`app/core`为微框架核心，定制了一整套服务模块规范，可参见server源码，示例如下

### Extend

`app/extend`目录下的模块用于扩展ctx对象
调用方式示例：`ctx.validate.isMobile.apply(ctx)`

### Middleware

中间件和 Koa 的中间件写法是一模一样的
core里内置了一些常用中间件，并且可以通过配置开启中间件(包括内置中间件)

由于中间件的加载顺序会影响到应用的运行，所以配置增加了`config.preMiddleware`和`config.postMiddleware`,
实际中间件加载顺序为: 

```javascript
config.middleware = config.preMiddleware.concat(config.coreMiddleware).concat(config.postMiddleware)
```

## Start

```bash
# install with taobao registry
npm run ii
# 本地开发
npm run dev
# 打包构建
npm run build
# 生产运行
npm run start
```