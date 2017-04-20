下载思维cdlinux
http://www.greenxf.com/soft/32141.html
↑这个不知道是不是思维
1.**用好压解压思维cdlinux.iso**不要用UltraISO会有大小写错误，巨坑
2.下载grub4dos，复制里面的grldr、grub.exe、menu.lst
3.修改menu.lst为以下内容
```
timeout=3

　　default 0

　　title CDlinux

　　find --set-root /CDlinux/bzImage

　　kernel /CDlinux/bzImage CDL_DEV=LABEL=CDlinux CDL_LANG=zh_CN.UTF-8

　　initrd /CDlinux/initrd
```
4.修改U盘名为CDlinux
5.用bootice建立分区引导，步骤为：打开，点击下面中间的分区引导记录，选第二个，然后默认的确定