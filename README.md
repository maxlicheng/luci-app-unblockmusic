## v2.3.1 版本更新
## 版本说明
- 同步L大优化后的代码；
- 支持多种方式代理，支持全系列路由器；
- 优化golang Makefile，解决因goproxy环境变量无法访问导致编译失败的错误。

## 功能更新：
- 增加golang版本的UnblockNeteaseMusic;
- 增加云服务器代理选项，可自定义；
- 更新Nodejs版本UnblockNeteaseMusic；
- golang、nodejs、云服务器三种代理方式可自由选择。

## 功能优化
- 优化代理逻辑；
- 增加音源选项；
- 优化日志显示;
- 支持中英文切换。

## 其他
- 因每个人的网络环境及设备存在差异，插件代理成功率也会存在差异，若你使用的版本能够正常代理，请不要轻易更新。 

## 说明
- luci-app-unblockmusic是用来解锁网易云灰色歌曲的OpenWRT/LEDE路由器插件
- 安装插件后可 免费 下载/播放 网易云付费歌曲 及 无版权音乐
- 核心功能： 
- [1].[nondanee/UnblockNeteaseMusic (node.js版本)](https://github.com/nondanee/UnblockNeteaseMusic.git)  
- [2].[cnsilvan/UnblockNeteaseMusic (golang版本)](https://github.com/cnsilvan/UnblockNeteaseMusic.git)
- 编写配套的luci插件，使源项目代码更方便的在路由器上运行

## 原理
- 其原理是采用 [QQ/虾米/百度/酷狗/酷我/咕咪/JOOX]等音源 替换网易云变灰歌曲链接
- 通俗地理解就是通过脚本，将主流客户端的音乐链接汇集到一个客户端上

## 编译
```shell
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
- **若编译过程中遇到问题可参考以下文章**
> [《OpenWRT node源码更新》](https://www.maxlicheng.com/embedded/623.html)  
> [《关于官方OpenWRT源码不支持luci-app-unblockmusic插件的解决方法》](https://www.maxlicheng.com/github/624.html)  

## 安装
- 假定路由器是mipsel架构
- 编译生成的ipk路径：bin/packages/mipsel/base/
- 将路径下的 UnblockNeteaseMusic_0.24.1-3_all.ipk 、UnblockNeteaseMusicGo_0.1.9-1_mipsel_24kc.ipk、luci-app-unblockmusic_2.3.1-40_all.ipk、 luci-i18n-unblockmusic-zh-cn_2.3.1-41_all.ipk用文件传输软件拷贝到路由器
- 若第一次安装还需将libopenssl1.1_1.1.1f-1_mipsel_24kc.ipk 及node_v12.16.1-1_mipsel_24kc.ipk 拷贝到路由器
- 完成后依次执行以下安装命令，注意安装顺序
- 若无法安装，可尝试使用opkg remove命令移除旧版本
```shell 
opkg install libopenssl1.1_1.1.1f-1_mipsel_24kc.ipk
opkg install node_v12.16.1-1_mipsel_24kc.ipk
opkg install UnblockNeteaseMusic_0.24.1-3_all.ipk
opkg install UnblockNeteaseMusicGo_0.1.9-1_mipsel_24kc.ipk
opkg install luci-app-unblockmusic_2.3.1-40_all.ipk
opkg install luci-i18n-unblockmusic-zh-cn_2.3.1-41_all.ipk
```

## 使用方法
- 1.在路由器web界面“服务”选项中找到“解锁网易云灰色歌曲”
- 2.选择其中一种代理方式，如golang版UnblockNeteaseMusic
- 3.勾选“启用解锁”，开启后，大部分设备无需设置代理，苹果系列设备除外
- 4.音源缺省“酷我音乐”，支持指定音源
- 5.点击“保存&应用”，完成插件配置
- 6.其他待补充

## 参考
- 以下是作者使用的各个系统的网易云音乐客户端版本，供大家参考。
> **Win10**：v2.5.3（Build:197601）  
> **IOS13**：v5.8.0  
> **Android**：v4.3.1.567509  

## 建议
- 因插件使用的ipv4进行代理，路由器尽量不开或者少开ipv6，可尝试用以下命令关闭路由器的ipv6
```shell
/etc/init.d/odhcpd disable
/etc/init.d/odhcpd stop
```

## 效果图
### luci界面
![Image text](https://www.maxlicheng.com/wp-content/uploads/2019/08/v2.2.0-views1.jpg)
### Windows客户端
![Image text](https://www.maxlicheng.com/wp-content/uploads/2019/07/views2.jpg)

## 补充
### 注1：插件运行后即可正常 下载/播放 付费歌曲及无版权音乐，若无法 下载/播放 可指定其它客户端音源进行尝试
### 注2：若开启“启用解锁”后，仍无法正常解锁歌曲，请按以下方法设置，因设备存在差异性，不一定所有设备都能正常生效，供参考
### Windows客户端
- **说明**：经多次测试，一般开启“自动代理”后，Windows网易客户端都可以正常解锁，无需设置代理；若确实无法解锁，请尝试以下步骤进行设置
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
- **说明**：若插件解锁效果不稳定或者无效果，可参考本人的教程笔记，下载低版本IOS网易云客户端安装包，用爱思助手进行手动安装。
- 具体安装教程请移步[《IOS网易云音乐低版本客户端安装教程》](https://www.maxlicheng.com/github/590.html)

## 关于issues
- 解锁效果及设备代理方面的问题，可先到核心功能项目中查看是否可以找到相关解决方案[ [ issues ] ](https://github.com/nondanee/UnblockNeteaseMusic/issues)
- 若实在没有相关的解决方案，欢迎开issues一同探讨
- 尽量在本项目的issues提源码编译和安装方面的问题，并附上你的路由器设备型号，最好以make menuconfig的截图或者文字贴到issues中，如
```
Target System (MediaTek Ralink MIPS) --->
Subtarget (MT7621 based boards) --->
Target Profile (Newifi D2) --->
```

## 鸣谢
- 感谢 [[nondanee]](https://github.com/nondanee) 开发的Node.js版解锁网易云灰色歌曲核心项目；
- 感谢 [[1715173329]](https://github.com/1715173329) 对本项目的[二次优化](https://github.com/project-openwrt/luci-app-unblockmusic)；
- 本插件已被 [[L大]](https://github.com/coolsnowwolf) 收录至 [[LEDE源码]](https://github.com/coolsnowwolf/lede)，并对本项目进行了多次优化，感谢 [[L大]](https://github.com/coolsnowwolf) 对本项目的认可及付出；
- 感谢 [[rufengsuixing]](https://github.com/rufengsuixing)对本项目的[二次优化](https://github.com/rufengsuixing/luci-app-unblockmusic)。
- 感谢 [[binsee]](https://github.com/binsee)对本项目的[多次优化](https://github.com/binsee/luci-app-unblockmusic)。
- 感谢 [[cnsilvan]](https://github.com/cnsilvan) 开发的golang版解锁网易云灰色歌曲核心项目；


## 其他 
- 更多设备的使用方法(MacOS等)，可移步个人博客：
> [《路由器解锁网易云灰色歌曲》](https://www.maxlicheng.com/github/232.html)  
> [《Win10系统解锁网易云音乐灰色歌曲》](https://www.maxlicheng.com/github/197.html)  
> [《IOS旧版本App下载教程》](https://www.maxlicheng.com/github/605.html)  
> [《IOS网易云音乐低版本客户端安装教程》](https://www.maxlicheng.com/github/590.html)  
> [《【视频】低版本IOS网易云音乐客户端听周杰伦歌曲效果》](https://www.bilibili.com/video/av61511828/)  



