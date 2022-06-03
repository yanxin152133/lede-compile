# 1. lede-compile
## 1.1. 官方地址
[coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)

## 1.2. 编译
1. 不要用 root 用户进行编译
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1 密码 password

### 1.2.1. 相关命令
1. 首先装好 Linux 系统，推荐 Debian 11 或 Ubuntu LTS
2. 安装编译依赖
```html
sudo apt update -y
sudo apt full-upgrade -y
sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pip qemu-utils \
rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
```

3. 下载源代码，更新feeds并选择配置
```html
git clone https://github.com/coolsnowwolf/lede
cd lede
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
```

4. 下载dl库，编译固件（-j 后面是线程数，第一次编译推荐用单线程）
```html
make download -j8
make V=s -j1
```

### 1.2.2. 二次编译
```html
cd lede
git pull
./scripts/feeds update -a
./scripts/feeds install -a
make defconfig
make download -j8
make V=s -j$(nproc)
```

重新设置配置：
```html
rm -rf ./tmp && rm -rf .config
make menuconfig
make V=s -j$(nproc)
```

编译完成后输出路径：bin/targets

## 1.3. 版本
### 1.3.1. R22.5.5
![image](https://user-images.githubusercontent.com/43341537/171808932-f1082bf0-22e6-445e-87d9-1e990beb33a6.png)
