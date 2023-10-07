---
title: npm install 的不同方式
date: 2023-08-05 11:13:45
tags:
- npm
- frontend
categories: npm
---

## npm install -g --save ?

<!-- more -->

- `npm install`（在包目录中）
  根据`package.json`文件，将依赖安装到包目录中`node_modules`文件夹
- `npm install "module-name"`
  安装特定依赖到包目录下
- `npm install -g "module-name"`
  `-g`表明将模块安装到全局，将包安装到`prefix`文件夹而不是当前工作目录，`{prefix}/lib/node_modules`
  可通过以下命令查看 npm 相关配置：
  ``` bash
  npm config ls
  ```
  ![](https://blog-1319684755.cos.ap-guangzhou.myqcloud.com/blog-images/202308051125123.png)
- `npm install --save "module-name"`
  `--save`表明模块安装并写入`package.json`的`dependencies`节点。`--save`等同于`-S`。
- - `npm install --save-prod "module-name"`
    包将出现在`dependencies`中，这是默认值
- - `npm install --save-dev "module-name"`
    包将出现在`devDependencies`中，运行`npm install --production`或`NODE_ENV`值为`production`时**不会**自动下载模块。`--save-dev`等同于`-D`。

`npm uninstall "module_name"`删除依赖同理。

## 总结

`devDependencies`节点下模块是开发时需要使用的，如辅助开发的压缩，部署后不需要，所以使用`--save-dev`形式安装。
`dependencies`节点下模块是运行时必备的，故采用`--save`（等同于`--save-prod`）安装。

## 参考

[npm中文网——npm-install](https://npm.nodejs.cn/cli/v9/commands/npm-install)
[NPM install -save 和 -save-dev 傻傻分不清](https://www.cnblogs.com/limitcode/p/7906447.html)