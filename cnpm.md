# cnpm是神器的国度的npm的替代品,对于不知道npm是什么的网络来说可以使用cnpm来替代

- cnpm安装命令:

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

- 如果不幸安装失败：

```
$ npm set registry https://registry.npm.taobao.org # 注册模块镜像
$ npm set disturl https://npm.taobao.org/dist # node-gyp 编译依赖的 node 源码镜像
$ npm cache clean # 清空缓存
```
