# openwrt-luci-kcp-udp  软件包

![](https://raw.githubusercontent.com/hongwenjun/openwrt-luci-kcp-udp/master/bin/lui_udp_kcp.png)

### OpenWRT-18.06.2 编译完成的 安装包
- udp2raw-tunne udpspeeder luci-udptools [安装包下载](https://github.com/hongwenjun/vps_setup/blob/master/openwrt-18.06.2/openwrt_udptools.zip)
- 单独下载 [luci-udptools 和 luci-kcptools](https://github.com/hongwenjun/openwrt-luci-kcp-udp/tree/master/bin) 图形管理配置包(全平台CPU通用)

### KcpTun 软件下载 client_linux 改名成 kcp-client 存放路径 /usr/bin
- https://github.com/xtaci/kcptun/releases

------

###  OpenWRT 安装 WireGuard 配置 Udp2Raw + UdpSpeeder (或者 KcpTun)
- 短网址: https://git.io/wrt.wg

--------

### OpenWRT-18.06.2 X64 固件和SDK 下载地址和文件名
https://downloads.openwrt.org/releases/18.06.2/targets/x86/64/
- openwrt-18.06.2-x86-64-combined-squashfs.img.gz
- openwrt-sdk-18.06.2-x86-64_gcc-7.3.0_musl.Linux-x86_64.tar.xz

### OpenWRT-18.06.2 x86 固件和SDK 下载地址和文件名
https://downloads.openwrt.org/releases/18.06.2/targets/x86/generic/
- openwrt-18.06.2-x86-generic-combined-squashfs.img.gz
- openwrt-sdk-18.06.2-x86-generic_gcc-7.3.0_musl.Linux-x86_64.tar.xz

### 按CPU选择下载SDK后，在VPS上 解压SDK并重命名为 opensdk
	tar xvJf openwrt-sdk-18.06.2-x86-64_gcc-7.3.0_musl.Linux-x86_64.tar.xz
	mv openwrt-sdk-18.06.2-x86-64_gcc-7.3.0_musl.Linux-x86_64  ~/opensdk

### 安装编译环境

```
apt -y install subversion build-essential libncurses5-dev zlib1g-dev gawk git ccache gettext libssl-dev xsltproc wget unzip python time
apt -y install libcloog-isl-dev
ln -s /usr/lib/x86_64-linux-gnu/libisl.so /usr/lib/libisl.so.10
```

### 下载 openwrt-luci-kcp-udp 到 opensdk/package
	cd ~/opensdk && git clone https://github.com/hongwenjun/openwrt-luci-kcp-udp.git
	mv openwrt-luci-kcp-udp/* package

### 配置make menuconfig; 在弹出的节目进入Luci—>3. applications，勾选为M即可，保存退出。
	cd ~/opensdk && make menuconfig

### 使用命令编译 luci-udptools  luci-kcptools(目前还没调试完成)
```
make package/luci-udptools/compile V=99
make package/luci-kcptools/compile V=99
make package/udp2raw/compile V=99
make package/udpspeeder/compile V=99

```
- 参考文件: 编译openwrt版udpspeeder和udp2raw [文章链接](https://www.atrandys.com/2018/1255.html)

###  方便下载ipk的脚本
```
#!/bin/bash
cd ~/opensdk/bin/packages/
ipk_url=http://$(curl -4 ip.sb):8000
python -m SimpleHTTPServer 8000 &
echo -e "请网页打开 ${ipk_url} 下载ipk文件"
echo -e "用命令 opkg install luci-xxxxxx.ipk 安装"
```
