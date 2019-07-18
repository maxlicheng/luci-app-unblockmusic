### 20190718更新说明
- 同步UnblockNeteaseMusic v0.16.0版本
#### 更新内容：
- 增加咪咕高音质音源 
- 增加 zlib 异常捕获 
- 补全搜索关键词 ，排列改回 歌名 - 歌手 
- 不再强制使用 package，默认情况音源不用通过服务器转发 
- 修复使用上游代理时泄露请求 body 的安全问题
- 修复 hosts 模式被代理认证限制的 
- 补全并完善 error handler，反正意外崩溃
- 具体可移步：https://github.com/nondanee/UnblockNeteaseMusic/releases
- 当前插件版本号：v1.37

# 说明
- 使用源码前，先检测自己的路由器主控芯片型号是否支持FPU,不支持FPU的是无法运行node.js的，插件依赖于node.js。
- 用于解锁网易云灰色歌曲的OpenWRT/LED路由器 Luci 插件
- 核心功能github地址：https://github.com/nondanee/UnblockNeteaseMusic.git 
- 自己编写luci插件，使源项目代码更方便的在路由器上运行
- 注：已知斐讯K3 OP不支持node.js，故无法使用此插件，请知悉。具体见 issues.

## 原理
- 其原理是采用  [网易云旧链/QQ/虾米/百度/酷狗/酷我/咕咪/JOOX]等音源 替换网易云变灰歌曲链接，
- 通俗地理解就是通过脚本，将主流客户端的音乐链接汇集到一个客户端上。

## 编译
- 插件依赖node.js，OpenWRT/LEDE源码默认是v8.10.0版本，编译过程中下载会比较慢，可以提前将node-v8.10.0下载好上传到dl目录。
- 下载链接(17.5M)：http://nodejs.org/dist/v8.10.0/node-v8.10.0.tar.xz  
```Brash
    #进入OpenWRT/LEDE源码package目录
    cd package
    #克隆插件源码
    git clone https://github.com/maxlicheng/luci-app-unblockmusic.git
    #返回上一层目录
    cd ..
    #配置
    make menuconfig
    #在luci->application选中插件,编译
    make package/luci-app-unblockmusic/compile V=99
```

## Releases中现有ipk
- 斐讯N1：n1-op-luci-app-unblockmusic-ipk.zip       4.6 MB
- 新三D2：newifi-d2-luci-app-unblockmusic_ipk.zip       4.32 MB
- 网件4300：wndr4300-luci-app-unblockmusic-ipk.zip       4.38 MB
- 软路由x86-64：x86-64-luci-app-unblockmusic_ipk.zip       5.07 MB
- 以上是适用于openwrt/lede系统的ipk插件，并已通过测试，安装即可使用，先安装node.ipk，再安装luci-app-unblockmusic.ipk。详见：https://github.com/maxlicheng/luci-app-unblockmusic/releases
- 现有ipk基于L大openwrt源码编译而成，注意内核版本要与插件编译时源码内核版本一致，否则无法正常使用。若无法正常使用，则需要找到与你当前系统内核版本相同的openwrt源码，自行编译插件。
```Brash
    #内核版本查看方式
    cat /proc/version
```

## 使用方法
### 1.路由器web界面插件配置
- a.在路由器web界面服务选项中找到“解锁网易云灰色歌曲”；
- b.勾选启用解锁；
- c.音源选择默认即可，其他音源暂时不起作用；
- d.设置你想要的端口号，默认5200；
- e.点击“保存&应用”

### 2.PC端
- a.打开网易云客户端；
- b.进入设置，找到工具；
- c.选择 自定义代理；
- d.服务器填入路由器ip，端口为你设定的端口号，默认5200。
- e.保存并重启；
- f.搜索“周杰伦”进行测试，歌曲正常并能正常播放，完成PC端设置。
 ![Image text](http://www.maxlicheng.com/wp-content/uploads/2019/06/luci-1.jpg)

### 3.移动端
- a.网络设置，找到连入的wifi；
- b.进入参数设置，找到HTTP PROXY；
- c.进入Configure Proxy，选择Automatic；
- d.在URL中填入http://192.168.10.1:5200/proxy.pac
- e.其中192.168.10.1为路由器IP，端口为你设定的端口号，默认5200；
- f.保存；
- g.打开网易云app，搜索“周杰伦”进行测试，歌曲正常并能正常播放，完成移动端设置。
 ![Image text](http://www.maxlicheng.com/wp-content/uploads/2019/06/Luci-3.jpg)

## 效果图
### luci界面
  ![Image text](https://raw.githubusercontent.com/maxlicheng/luci-app-unblockmusic/master/views/views1.jpg)
### PC网易云客户端
  ![Image text](https://raw.githubusercontent.com/maxlicheng/luci-app-unblockmusic/master/views/views2.jpg)
  
## 其他
更详细的使用方法，可移步个人博客：https://www.maxlicheng.com/github/232.html
