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
* 当前 coolsnowwolf/lede 项目已直接支持 r2s
* 截至2020年10月16日，Lienol/openwrt 项目未加入支持 r2s

## 附录 config.buildinfo
<code>
  CONFIG_TARGET_rockchip=y
CONFIG_TARGET_rockchip_armv8=y
CONFIG_TARGET_rockchip_armv8_DEVICE_friendlyarm_nanopi-r2s=y
CONFIG_ARIA2_BITTORRENT=y
CONFIG_ARIA2_NOXML=y
CONFIG_ARIA2_OPENSSL=y
CONFIG_ARIA2_WEBSOCKET=y
CONFIG_LIBCURL_COOKIES=y
CONFIG_LIBCURL_FILE=y
CONFIG_LIBCURL_FTP=y
CONFIG_LIBCURL_HTTP=y
CONFIG_LIBCURL_MBEDTLS=y
CONFIG_LIBCURL_NO_SMB="!"
CONFIG_LIBCURL_PROXY=y
# CONFIG_PACKAGE_UnblockNeteaseMusic is not set
# CONFIG_PACKAGE_UnblockNeteaseMusicGo is not set
CONFIG_PACKAGE_aria2=y
CONFIG_PACKAGE_ariang=y
CONFIG_PACKAGE_bind-libs=y
CONFIG_PACKAGE_bind-nslookup=y
CONFIG_PACKAGE_blkid=y
CONFIG_PACKAGE_btrfs-progs=y
CONFIG_PACKAGE_ca-bundle=y
CONFIG_PACKAGE_curl=y
CONFIG_PACKAGE_ddns-scripts_cloudflare.com-v4=y
CONFIG_PACKAGE_ddns-scripts_no-ip_com=y
CONFIG_PACKAGE_dnsmasq_full_auth=y
CONFIG_PACKAGE_dnsmasq_full_broken_rtc=y
CONFIG_PACKAGE_dnsmasq_full_conntrack=y
CONFIG_PACKAGE_dnsmasq_full_dhcpv6=y
CONFIG_PACKAGE_dnsmasq_full_dnssec=y
CONFIG_PACKAGE_dnsmasq_full_noid=y
# CONFIG_PACKAGE_etherwake is not set
CONFIG_PACKAGE_frpc=y
CONFIG_PACKAGE_frps=y
CONFIG_PACKAGE_iptables-mod-ipsec=y
CONFIG_PACKAGE_kmod-crypto-acompress=y
CONFIG_PACKAGE_kmod-crypto-cbc=y
CONFIG_PACKAGE_kmod-crypto-deflate=y
CONFIG_PACKAGE_kmod-crypto-des=y
CONFIG_PACKAGE_kmod-crypto-echainiv=y
CONFIG_PACKAGE_kmod-crypto-hmac=y
CONFIG_PACKAGE_kmod-crypto-md5=y
CONFIG_PACKAGE_kmod-fs-btrfs=y
CONFIG_PACKAGE_kmod-ipsec=y
CONFIG_PACKAGE_kmod-ipsec4=y
CONFIG_PACKAGE_kmod-ipsec6=y
CONFIG_PACKAGE_kmod-ipt-ipsec=y
CONFIG_PACKAGE_kmod-iptunnel4=y
CONFIG_PACKAGE_kmod-iptunnel6=y
CONFIG_PACKAGE_kmod-lib-crc32c=y
CONFIG_PACKAGE_kmod-lib-lzo=y
CONFIG_PACKAGE_kmod-lib-raid6=y
CONFIG_PACKAGE_kmod-lib-xor=y
CONFIG_PACKAGE_kmod-lib-zlib-deflate=y
CONFIG_PACKAGE_kmod-lib-zlib-inflate=y
CONFIG_PACKAGE_kmod-lib-zstd=y
CONFIG_PACKAGE_kmod-md-mod=y
CONFIG_PACKAGE_kmod-md-raid0=y
CONFIG_PACKAGE_kmod-md-raid1=y
CONFIG_PACKAGE_kmod-md-raid10=y
CONFIG_PACKAGE_kmod-md-raid456=y
# CONFIG_PACKAGE_kmod-tun is not set
CONFIG_PACKAGE_libattr=y
CONFIG_PACKAGE_libcap=y
CONFIG_PACKAGE_libcurl=y
CONFIG_PACKAGE_libgmp=y
# CONFIG_PACKAGE_libhttp-parser is not set
CONFIG_PACKAGE_liblzo=y
# CONFIG_PACKAGE_libminiupnpc is not set
CONFIG_PACKAGE_libmount=y
# CONFIG_PACKAGE_libnatpmp is not set
CONFIG_PACKAGE_libnetfilter-conntrack=y
CONFIG_PACKAGE_libnettle=y
CONFIG_PACKAGE_libnfnetlink=y
# CONFIG_PACKAGE_libnghttp2 is not set
CONFIG_PACKAGE_libnss=y
CONFIG_PACKAGE_libreadline=y
CONFIG_PACKAGE_libsqlite3=y
CONFIG_PACKAGE_libwebsockets-full=y
CONFIG_PACKAGE_lsblk=y
# CONFIG_PACKAGE_luci-app-accesscontrol is not set
CONFIG_PACKAGE_luci-app-aria2=y
# CONFIG_PACKAGE_luci-app-autoreboot is not set
CONFIG_PACKAGE_luci-app-diskman=y
CONFIG_PACKAGE_luci-app-diskman_INCLUDE_btrfs_progs=y
CONFIG_PACKAGE_luci-app-diskman_INCLUDE_kmod_md_linear=y
CONFIG_PACKAGE_luci-app-diskman_INCLUDE_kmod_md_raid456=y
CONFIG_PACKAGE_luci-app-diskman_INCLUDE_lsblk=y
CONFIG_PACKAGE_luci-app-diskman_INCLUDE_mdadm=y
CONFIG_PACKAGE_luci-app-frpc=y
CONFIG_PACKAGE_luci-app-frps=y
CONFIG_PACKAGE_luci-app-ipsec-vpnd=y
CONFIG_PACKAGE_luci-app-netdata=y
CONFIG_PACKAGE_luci-app-ssr-plus_INCLUDE_NaiveProxy=y
CONFIG_PACKAGE_luci-app-ttyd=y
# CONFIG_PACKAGE_luci-app-unblockmusic is not set
# CONFIG_PACKAGE_luci-app-webadmin is not set
# CONFIG_PACKAGE_luci-app-wol is not set
CONFIG_PACKAGE_luci-app-xlnetacc=y
# CONFIG_PACKAGE_luci-app-zerotier is not set
CONFIG_PACKAGE_luci-i18n-aria2-zh-cn=y
CONFIG_PACKAGE_luci-i18n-frpc-zh-cn=y
CONFIG_PACKAGE_luci-i18n-frps-zh-cn=y
CONFIG_PACKAGE_luci-i18n-ipsec-vpnd-zh-cn=y
CONFIG_PACKAGE_luci-i18n-netdata-zh-cn=y
CONFIG_PACKAGE_luci-i18n-ttyd-zh-cn=y
CONFIG_PACKAGE_mdadm=y
CONFIG_PACKAGE_naiveproxy=y
CONFIG_PACKAGE_nano=y
CONFIG_PACKAGE_netdata=y
# CONFIG_PACKAGE_node is not set
CONFIG_PACKAGE_nspr=y
CONFIG_PACKAGE_parted=y
CONFIG_PACKAGE_shadowsocks-libev-ss-rules=y
CONFIG_PACKAGE_shadowsocks-libev-ss-server=y
CONFIG_PACKAGE_shadowsocks-libev-ss-tunnel=y
CONFIG_PACKAGE_smartmontools=y
CONFIG_PACKAGE_strongswan=y
CONFIG_PACKAGE_strongswan-charon=y
CONFIG_PACKAGE_strongswan-ipsec=y
CONFIG_PACKAGE_strongswan-minimal=y
CONFIG_PACKAGE_strongswan-mod-aes=y
CONFIG_PACKAGE_strongswan-mod-gmp=y
CONFIG_PACKAGE_strongswan-mod-hmac=y
CONFIG_PACKAGE_strongswan-mod-kernel-libipsec=y
CONFIG_PACKAGE_strongswan-mod-kernel-netlink=y
CONFIG_PACKAGE_strongswan-mod-nonce=y
CONFIG_PACKAGE_strongswan-mod-pubkey=y
CONFIG_PACKAGE_strongswan-mod-random=y
CONFIG_PACKAGE_strongswan-mod-sha1=y
CONFIG_PACKAGE_strongswan-mod-socket-default=y
CONFIG_PACKAGE_strongswan-mod-stroke=y
CONFIG_PACKAGE_strongswan-mod-updown=y
CONFIG_PACKAGE_strongswan-mod-x509=y
CONFIG_PACKAGE_strongswan-mod-xauth-generic=y
CONFIG_PACKAGE_strongswan-mod-xcbc=y
CONFIG_PACKAGE_ttyd=y
CONFIG_PACKAGE_uclibcxx=y
# CONFIG_PACKAGE_wol is not set
# CONFIG_PACKAGE_zerotier is not set
CONFIG_SQLITE3_DYNAMIC_EXTENSIONS=y
CONFIG_SQLITE3_FTS3=y
CONFIG_SQLITE3_FTS4=y
CONFIG_SQLITE3_FTS5=y
CONFIG_SQLITE3_JSON1=y
CONFIG_SQLITE3_RTREE=y
CONFIG_STRONGSWAN_ROUTING_TABLE="220"
CONFIG_STRONGSWAN_ROUTING_TABLE_PRIO="220"
</code>
