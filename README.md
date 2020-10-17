# lede-for-r2s 固件在线编译项目
* 直接下载 https://github.com/szdosar/lede-for-r2s/releases

![image](https://github.com/szdosar/lede-for-r2s/blob/main/r2soverview.png)
## 采用 Lean 的 Openwrt 源码仓库
仓库地址 https://github.com/coolsnowwolf/lede<br>
原汁原味，无修改<br>
默认登陆 IP <code>192.168.1.1</code><br>
初始密码 <code>password</code>
* 我的自动化流程用了自有服务器<br>
如果你没有服务器，就用 github 的默认服务器<br>
方法：将流程文件中的<code>runs-on: self-hosted</code><br>
改为<code>runs-on: ubuntu-latest</code>

## 适用硬件
FriendlyElec NanoPi R2S 芯片 RK3328
![image](https://github.com/szdosar/lede-for-r2s/blob/main/r2s.jpg)
## 定制编译的组件
### 定制编译的方法1--可选项<br>
* 要触发 SSH 定制，请修改流程文件<br>
将<code>SSH_ACTIONS: false</code><br>
改为<code>SSH_ACTIONS: true</code><br>
流程运行到这，会生成连接网址<br>
--如何找到这个链接？<br>
-1-.点击上方的【Actions】<br>
-2-.点击正在运行中的流程<br>
-3-.点击【build】<br>
-4-.待流程运行到 SSH connection to Actions 环节<br>
-5-.等几分钟，看到显示出来的链接<br>
它看起来像 https://tmate.io/t/BHhWX7CY7hZJBRNEaVtm9xWJz<br>
![image](https://github.com/szdosar/lede-for-r2s/blob/main/r2s-ssh.png)
-6-.点击链接，然后按【Q】或 Ctrl+C 继续<br>
-7-.输入命令<code>cd lede && make menuconfig</code><br>
-8-.定制你要编译的组件<br>
-9-.你还可以修改默认登陆 IP<br>
** >>>><br>
通过修改源码中此文件 package/base-files/files/bin/config_generate 的下面代码实现<br>
<code>lan) ipad=${ipaddr:-"192.168.1.1"} ;;</code><br>
** <<<<<br>
* 退出定制<br>
1.完成后输入【exit】可退出 SSH 定制<br>
2.默认半小时无动作会跳过这个环节<br>
3.自动化流程会继续未完成的环节<br>
### 定制编译的方法2--可选项<br>
编译前，你可事先编辑文件 r2s-rk3328-config 来定制编译的组件<br>
但你要适当修改流程文件中的这段代码<br>
<code>wget -c https://raw.githubusercontent.com/szdosar/lede-for-r2s/main/r2s-rk3328-config -O .config</code>

## 触发自动化流程的运行
* 修改 CHANGELOG.md 文件

## 感谢
* Lean<br>
仓库地址 https://github.com/coolsnowwolf/lede<br>
* 引用了 p3terx/debugger-action@main<br>
新项目地址 https://github.com/P3TERX/ssh2actions<br>
* 引用了 helloworld 项目<br>
项目地址 https://github.com/fw876/helloworld<br>
*采用了 ShadowSocksR Plus+ 科学上网组件<br>
* 发布代码引用了项目 Upload files to a GitHub release<br>
项目地址https://github.com/svenstaro/upload-release-action<br>
* 灵感来源于悟空的视频
* 截至2020年10月16日，Lienol/openwrt 项目未加入支持 r2s
* 当前 coolsnowwolf/lede 项目已直接支持 r2s<br>
仓库地址 https://github.com/coolsnowwolf/lede<br>
>>在 Target System 里选 (Rockchip) ---><br>
>>在 Subtarget 里选 (RK33XX boards (64 bit)) ---><br>
>>在 Target Profile 里选 （FriendlyARM NanoPi R2S)<br>
![image](https://github.com/szdosar/lede-for-r2s/blob/main/r2s-menuconfig.png)
## 附录 config.buildinfo
https://raw.githubusercontent.com/szdosar/lede-for-r2s/main/config.buildinfo
