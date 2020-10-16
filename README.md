# lede-for-r2s 在线编译项目
* 当前 coolsnowwolf/lede 项目已直接支持 r2s
* 截至2020年10月16日，Lienol/openwrt 项目未加入支持 r2s

## 采用 Lean 的 Openwrt 源码仓库
仓库地址 https://github.com/coolsnowwolf/lede<br>
原汁原味，无修改<br>
默认登陆 IP <code>192.168.1.1</code><br>
初始密码 <code>password</code>
* 我的自动化流程用了自有服务器<br>
可将流程文件中的<code>runs-on: self-hosted</code><br>
改为<code>runs-on: ubuntu-latest</code>

## 适用硬件
FriendlyElec NanoPi R2S 芯片 RK3328

## 定制编译的组件
### 定制编译的方法1<br>
* 要触发定制，请修改流程文件<br>
将<code>SSH_ACTIONS: false</code><br>
改为<code>SSH_ACTIONS: true</code><br>
流程运行到这，会生成连接网址<br>
点击它，按【Q】继续<br>
然后输入<code>cd lede && make menuconfig</code><br>
定制你要编译的组件<br>
你还可以修改默认登陆 IP<br>
** >>>><br>
通过修改源码中此文件 package/base-files/files/bin/config_generate 的下面代码实现<br>
<code>lan) ipad=${ipaddr:-"192.168.1.1"} ;;</code><br>
** <<<<<br>
* 退出定制<br>
完成后输入【exit】可退出 SSH 定制<br>
默认半小时无动作会跳过这个环节<br>
### 定制编译的方法2<br>
编译前，你可事先编辑文件 r2s-rk3328-config 来定制编译的组件<br>
但你要适当修改流程文件中的这段代码<br>
<code>wget -c https://raw.githubusercontent.com/szdosar/lede-for-r2s/main/r2s-rk3328-config -O .config</code>


## 感谢
* Lean
仓库地址 https://github.com/coolsnowwolf/lede<br>
* fyglinfo
项目地址 https://github.com/fyglinfo/actions-openwrt-passwall
* 引用了 p3terx/debugger-action@main<br>
新项目地址 https://github.com/P3TERX/ssh2actions<br>
* 引用了 helloworld 项目<br>
项目地址 https://github.com/fw876/helloworld<br>
* 采用 ShadowSocksR Plus+<br>
* 发布代码引用了项目 Upload files to a GitHub release<br>
项目地址https://github.com/svenstaro/upload-release-action<br>
