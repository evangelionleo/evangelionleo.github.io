# vue ui命令没反应

## 原因：版本太低

版本低于3时没有ui功能
查看版本号
```vue -V```

查看是否有ui功能
```vue -h```

解决方法：

```
卸载老版本：
npm uninstall vue-cli -g

下载新版本，vue-cli的3.0+以后使用的不是vue-cli了，如果用以上的安装命令安装的并不是最新版的3.0+的，而如果安装3.0的话就需要使用新的
npm install @vue/cli -g

```




到此，解决！欢迎评论

