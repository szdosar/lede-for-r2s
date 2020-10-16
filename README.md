# lede-for-r2s 在线编译项目
## 采用 Lean 的 Openwrt 源码仓库
仓库地址 https://github.com/coolsnowwolf/lede<br>
原汁原味，无修改<br>
默认登陆 IP <code>192.168.1.1</code><br>
初始密码 <code>password</code>

## 适用硬件
FriendlyElec NanoPi R2S 芯片 RK3328

## 定制编译的组件
### 定制编译的步骤<br>
* 要触发定制，请注销 actions 中这两行前面的#号<br>
<code>- name: SSH connection to Actions</code><br>
<code>  uses: p3terx/debugger-action@main</code><br>
项目运行到这两行，会生成连接网址<br>
点击它，按【Q】<br>
然后输入<code>cd lede && make menuconfig</code>，定制你要编译的组件<br>
完成后输入【exit】退出<br>
默认半小时无动作会跳过这个环节<br>
你也可以直接事先编辑文件 r2s-rk3328-config<br>
但你要适当修改 actions 中的这段代码<br>
<code>wget -c https://raw.githubusercontent.com/szdosar/lede-for-r2s/main/r2s-rk3328-config -O .config</code>

* 修改默认登陆 IP<br>
通过修改package/base-files/files/bin/config_generate中的下面代码实现
<code>lan) ipad=${ipaddr:-"192.168.1.1"} ;;</code>

* 引用了 p3terx/debugger-action@main<br>
新项目地址 https://github.com/P3TERX/ssh2actions
但我仍用旧代码<br>

## 引用了 helloworld 项目以便科学上网
项目地址 https://github.com/fw876/helloworld
