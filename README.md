# 说明
用于解锁网易云灰色歌曲的OpenWRT/LED路由器 Luci 插件

## 使用方法
### 1.编译插件
```Brash
    #进入OpenWRT/LEDE源码package目录
    cd package
    #克隆插件源码
    git clone https://github.com/maxlicheng/luci-app-unblockmusic.git
    #返回上一层目录
    cd ..
    #配置
    make menuconfig
    #在luci->application选中插件
    #编译
    make package/luci-app-unblockmusic/compile V=99
```
### 2.路由器web界面插件配置

- a.在路由器web界面服务选项中找到“解锁网易云灰色歌曲”；
- b.勾选启用解锁；
- c.设置你想要的端口号；
- d.点击“保存&应用”

### 3.PC端

- a.打开网易云客户端；
- b.进入设置,找到工具；
- c.选择 自定义代理；
- d.服务器填入路由器ip,端口为你设定的端口号，默认5200。
- e.保存并重启；
- f.搜索“周杰伦”，歌曲正常并能正常播放，完成PC端设置。

### 4.移动端

- a.网络设置，找到连入的wifi；
- b.进入参数设置,找到HTTP PROXY;
- c.进入并选择静态IP；
- d.服务器填入路由器ip,端口为你设定的端口号，默认5200。
- e.保存；
- f.打开网易云app,搜索“周杰伦”，歌曲正常并能正常播放，完成移动端设置。

## 其他
更详细的使用方法，可移步个人博客：www.maxlicheng.com

