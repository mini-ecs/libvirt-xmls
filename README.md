宿主机如果需要使用virsh console到虚拟机的shell，需要修改虚拟机的相关配置文件
```sh
cat > /etc/default/grub << EOF
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL="console serial"
GRUB_SERIAL_COMMAND="serial --speed=115200 --unit=0 --word=8 --parity=no --stop=1"
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb"
GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200"
GRUB_DISABLE_RECOVERY="true"
EOF
```
使生效：
grub2-mkconfig -o /boot/grub2/grub.cfg

reboot