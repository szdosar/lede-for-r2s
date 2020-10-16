# lede-for-r2s
## 采用 Lean 的 Openwrt 源码仓库
仓库地址 https://github.com/coolsnowwolf/lede
默认登陆IP 192.168.1.1, 密码 password

## 硬件
FriendlyElec NanoPi R2S 芯片 RK3328

## 定制编译的组件
引用了 p3terx/debugger-action@main<br>
新项目地址 https://github.com/P3TERX/ssh2actions
但我仍用旧代码<br>
<code>- name: SSH connection to Actions</code><br>
<code>  uses: p3terx/debugger-action@main</code><br>
要定制编译的组件，请注销 actiongs 中这两行前面的#号，项目运行到这两行，会生成连接网址<br>
点击它，按【Q】，然后输入<code>cd lede && make menuconfig</code>，定制你要编译的组件<br>
完成后输入【exit】退出，默认半小时无动作会跳过这个环节<br>
你也可以直接事先编辑文件 r2s-rk3328-config，但你要适当修改 actiongs 中的这段代码<br>
<code>wget -c https://raw.githubusercontent.com/szdosar/lede-for-r2s/main/r2s-rk3328-config -O .config</code>

## 引用了 helloworld 项目以便科学上网
项目地址 https://github.com/fw876/helloworld
