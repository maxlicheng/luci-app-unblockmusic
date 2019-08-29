## v2.2.0更新说明
### 源码更新
- 合并 [[Lean]](https://github.com/coolsnowwolf) 对本插件二次优化后的源码
- 同步 [UnblockNeteaseMusic-0.18.1](https://github.com/nondanee/UnblockNeteaseMusic/releases/tag/v0.18.1) 源码

### 功能更新
- 缺省默认"酷我音乐"高品质音源
- 简化插件，勾选“启用解锁”后即可自动代理
- 优化自动代理，提高解锁成功率，苹果端自动代理URL留空即可进行解锁
- 简化日志显示
- 修复与其他插件冲突问题 
- 注：插件已取消端口设置，但后台仍占用5200端口及5201端口，请保证此俩端口未被路由器其他程序占用。

## 说明
- luci-app-unblockmusic是用来解锁网易云灰色歌曲的OpenWRT/LEDE路由器插件
- 安装插件后可 免费 下载/播放 网易云付费歌曲 及 无版权音乐
- 核心功能：[nondanee/UnblockNeteaseMusic](https://github.com/nondanee/UnblockNeteaseMusic.git) 
- 编写配套的luci插件，使源项目代码更方便的在路由器上运行
- 注：插件依赖于node.js，路由器主控芯片不支持FPU的设备不能正常运行node.js，已知斐讯K3不支持node.js

## 原理
- 其原理是采用 [QQ/虾米/百度/酷狗/酷我/咕咪/JOOX]等音源 替换网易云变灰歌曲链接
- 通俗地理解就是通过脚本，将主流客户端的音乐链接汇集到一个客户端上

## 编译
```
#进入OpenWRT/LEDE源码package目录
cd package
#克隆插件源码
git clone https://github.com/maxlicheng/luci-app-unblockmusic.git
#返回上一层目录
cd ..
#配置
make menuconfig
#在luci->application选中插件,编译
#单独编译路径较上一版本有变动，需要指定到app文件夹
make package/luci-app-unblockmusic/app/compile V=99
```

## 安装
- 假定路由器是x86_64架构
- 编译生成的ipk路径：bin/packages/x86_64/base/
- 将路径下的 UnblockNeteaseMusic_0.18.0-3_x86_64.ipk 和 luci-app-unblockmusic_2.2.0-1_all.ipk 用文件传输软件拷贝到路由器
- 若第一次安装还需将 node_v8.10.0-3_x86_64.ipk 拷贝到路由器
- 完成后依次执行以下安装命令，注意安装顺序
```
opkg install node_v8.10.0-3_x86_64.ipk
opkg install UnblockNeteaseMusic_0.18.0-3_x86_64.ipk 
opkg install luci-app-unblockmusic_v2.2.0-1_all.ipk
```

## 使用方法
- 1.在路由器web界面“服务”选项中找到“解锁网易云灰色歌曲”
- 2.勾选“启用解锁”，开启后，大部分设备无需设置代理，苹果系列设备除外
- 3.音源缺省“酷我音乐”，支持指定音源
- 4.点击“保存&应用”，完成插件配置

## 效果图
### luci界面
![Image text](https://www.maxlicheng.com/wp-content/uploads/2019/08/v2.2.0-views1.jpg)
### Windows客户端
![Image text](https://www.maxlicheng.com/wp-content/uploads/2019/07/views2.jpg)

## 补充
### 注1：插件运行后即可正常 下载/播放 付费歌曲及无版权音乐，若无法 下载/播放 可指定其它客户端音源进行尝试
### 注2：若开启“启用解锁”后，仍无法正常解锁歌曲，请按以下方法设置，因设备存在差异性，不一定所有设备都能正常生效，供参考
### Windows客户端
- 说明：经多次测试，一般开启“自动代理”后，Windows网易客户端都可以正常解锁，无需设置代理；若确实无法解锁，请尝试以下步骤进行设置
- 1.打开网易云客户端
- 2.进入设置，找到工具
- 3.选择 自定义代理
- 4.服务器填入路由器ip，端口号默认5200
- 5.保存并重启
- 6.搜索“周杰伦”进行测试，歌曲正常并能正常播放，完成PC端设置
![Image text](http://www.maxlicheng.com/wp-content/uploads/2019/06/luci-1.jpg)
 
### IOS客户端
#### 设置方法
- 1.网络设置，找到连入的wifi
- 2.进入参数设置，找到HTTP PROXY
- 3.进入Configure Proxy，选择Automatic，URL留空
- 4.保存
- 5.打开网易云app，搜索“周杰伦”进行测试，歌曲正常并能正常播放，完成IOS端设置
![Image text](https://www.maxlicheng.com/wp-content/uploads/2019/08/v2.20-views2.jpg)
#### 安装低版本客户端
- 说明：若插件解锁效果不稳定或者无效果，请用爱思助手安装本人提供的低版本网易云客户端安装包
- 具体安装教程请移步[《IOS网易云音乐低版本客户端安装教程》](https://www.maxlicheng.com/github/590.html)

## 关于issues
- 解锁效果及设备代理方面的问题，可先到核心功能项目中查看是否可以找到相关解决方案[ [ nondanee/UnblockNeteaseMusic-issues ] ](https://github.com/nondanee/UnblockNeteaseMusic/issues)
- 若实在没有相关的解决方案，欢迎开issues一同探讨
- 尽量在本项目的issues提源码编译和安装方面的问题，并附上你的路由器设备型号，最好以make menuconfig的截图或者文字贴到issues中，如
```
Target System (MediaTek Ralink MIPS) --->
Subtarget (MT7621 based boards) --->
Target Profile (Newifi D2) --->
```

## 鸣谢
- 感谢 [[nondanee]](https://github.com/nondanee) 开发的解锁网易云灰色歌曲核心项目
- 感谢 [[1715173329]](https://github.com/1715173329) 对本项目的[二次优化](https://github.com/project-openwrt/luci-app-unblockmusic)
- 本插件已被 [[L大]](https://github.com/coolsnowwolf) 收录至 [[LEDE源码]](https://github.com/coolsnowwolf/lede)，并对本项目进行了多次优化，感谢 [[L大]](https://github.com/coolsnowwolf) 对本项目的认可及付出


## 其他 
- 更多设备的使用方法(MacOS等)，可移步个人博客：
- [《路由器解锁网易云灰色歌曲》](https://www.maxlicheng.com/github/232.html)
- [《Win10系统解锁网易云音乐灰色歌曲》](https://www.maxlicheng.com/github/197.html)
- [《IOS旧版本App下载教程》](https://www.maxlicheng.com/github/605.html)
- [《IOS网易云音乐低版本客户端安装教程》](https://www.maxlicheng.com/github/590.html)
- [《【视频】低版本IOS网易云音乐客户端听周杰伦歌曲效果》](https://www.bilibili.com/video/av61511828/)



