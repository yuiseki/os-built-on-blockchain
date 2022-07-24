
tmp/linux-5.18.14.tar.xz:
	cd tmp && wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.18.14.tar.xz

tmp/linux-5.18.14/Makefile:
	cd tmp && xzcat linux-5.18.14.tar.xz | tar xfv -

tmp/linux-5.18.14/.config:
	cd tmp/linux-5.18.14 && cp arch/x86/configs/x86_64_defconfig ./.config
	cd tmp/linux-5.18.14 && make menuconfig

tmp/linux-5.18.14/arch/x86/boot/bzImage:
	cd tmp/linux-5.18.14 && make -j

tmp/busybox-1.35.0.tar.bz2:
	cd tmp && wget https://busybox.net/downloads/busybox-1.35.0.tar.bz2

tmp/busybox-1.35.0/Makefile:
	cd tmp && tar -jxvf busybox-1.35.0.tar.bz2

# Setting -> Build static binary (no shared libs)をチェックする
# Networking Utilities -> Enable IPv6 Supportのチェックを外す
tmp/busybox-1.35.0/_install/linuxrc:
	cd tmp/busybox-1.35.0 && make menuconfig
	cd tmp/busybox-1.35.0 && make install

tmp/busybox-1.35.0/_install/root:
	cd tmp/busybox-1.35.0/_install && bash -c 'mkdir -pv {bin,dev,sbin,etc,proc,sys/kernel/debug,usr/{bin,sbin},lib,lib64,mnt/root,root}'

tmp/busybox-1.35.0/_install/init:
	cp init tmp/busybox-1.35.0/_install

tmp/busybox-1.35.0/_install/etc/init.d/rcS:
	mkdir -p tmp/busybox-1.35.0/_install/etc/init.d/
	cp ./rcS tmp/busybox-1.35.0/_install/etc/init.d/

tmp/busybox.img:
	cd tmp/busybox-1.35.0/_install && find . | cpio -o --format=newc | gzip > ../../busybox.img

# Ctrl + A X で終了
qemu:
	qemu-system-x86_64 -nographic \
		-kernel ./tmp/linux-5.18.14/arch/x86/boot/bzImage \
		-initrd ./tmp/busybox.img \
		-append "console=ttyS0 root=/dev/ram rdinit=/sbin/init"
