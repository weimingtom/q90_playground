# q90_playground
[WIP] My Q90 Playground.  
Currently not tested under official Q90 firmware, use MiyooCFW firmware (burn to TF Card and insert) instead.     
Sup M3 can support MiyooCFW (Burn it to TF Card and insert into it) too, but not suggested,   
see below 'About running MiyooCFW for Sup M3'.       

## cross compile gcc  
* https://github.com/MiyooCFW/toolchain/releases/download/v2.0.0/miyoo-toolchain-v2.0.0-arm-buildroot-linux-musleabi_sdk-buildroot.tar.gz  
* https://github.com/MiyooCFW/toolchain/releases/tag/v2.0.0  
* miyoo-toolchain-v2.0.0-arm-buildroot-linux-musleabi_sdk-buildroot.tar.gz  
* arm-buildroot-linux-musleabi_sdk-buildroot
* arm-linux-gcc, equals arm-buildroot-linux-musleabi-gcc  
* Tested under xubuntu 20  
* **After extract musl toolchain, run relocate-sdk.sh**    

## MiyooCFW, Using firmware burn to the TF Card  
* MiyooCFW-2.0.0-Beta-7fc5140.zip/miyoo-cfw-2.0.0-gb0130e40_musl-BETA.img  
* https://github.com/TriForceX/MiyooCFW/wiki/  
* MiyooCFW-2.0.0-Beta-7fc5140.zip  
from https://github.com/TriForceX/MiyooCFW/releases  
don't use uclibc version in the zip file. use musl for prebuilt toolchain in github.com/MiyooCFW/toolchain   
* 

## Copy files to the TF Card which mount to the VirtualBox xubuntu    
* How:  
```
copy files to TF Card  
$ sudo cp sdltest /media/wmt/MAIN/  
$ sudo cp sdltest.sh /media/wmt/MAIN/  
$ sudo cp sdltest /media/wmt/rootfs/bin/  

复制到 /MAIN分区后（q80挂载/mnt）  
然后在掌机（烧录MiyooCFW-2.0.0-Beta-7fc5140.zip/miyoo-cfw-2.0.0-gb0130e40_musl-BETA.img）  
musl固件中
按select键，然后选Add Link，选择/mnt/sdltest即可添加快捷方式
然后运行
```
* record  
```
关于Q90自制软件，简单做法大概是这样：
（1）首先要有一台支持miyoocfw的掌机，
但最好不是sup m3（我不知道怎么解决），
后来我是用q90代替
（2）固件用TriForceX/MiyooCFW的MiyooCFW-2.0.0-Beta musl
（3）工具链用MiyooCFW/toolchain的miyoo-toolchain-v2.0.0 musl，
系统是xubuntu 2004 非32位
（4）示例代码参考doodlewind/MiyooSDK或者steward-fu/archives的
src_sdltest.7z，不过其实都是类似的，不过这个例子有问题，
它没指定工具链路径（可能会调用到其他工具链导致动态库
ld链接失败得不到最终的elf文件），
而且如果是用miyoo-toolchain还要加上一些别的静态库诸如asound，
具体可以查看工具链中sdl.pc文件内容。
（5）安装到tf卡，需要用虚拟机xubuntu挂载tf卡然后sudo cp到/mnt下
（elf文件似乎就够了，不需要sh）
（6）运行的话，用select按键选Add Link，
选择/mnt/sdltest即可添加快捷方式
```

## About running MiyooCFW for Sup M3, not Q90  
``
sup m3, MiyooCFW-2.0.0-Beta-7fc5140.zip, musl
隔了好几个月，我终于摸索出怎么在sup m3上正确配置运行MiyooCFW的方法。
其实很简单，就是要多修改options.cfg这个文件才行。
（1）首先要穷举console.cfg中的CONSOLE_VARIANT值，
我选择了CONSOLE_VARIANT=m3_r61520（参考firstboot文件），
可以显示（为了跳过安装程序，需要把firstboot改名，例如firstboot.skip），
但屏幕还是会反色
（2）如何解决反色问题呢，答案在firstboot里，
firstboot里面提到一个配置文件options.cfg，
这个文件不容易找到是因为需要tf卡通过掌机去连PC，
而不是通过读卡器连PC，这样就可以看到main盘符，
然后修改里面options.cfg的配置INVERT=0，
然后重启即可得到正常颜色的MiyooCFW
（3）由于sup m3的按键不太适应MiyooCFW，
所以只能勉强用，但framebuffer应该正常了
```
```
（1）修改console.cfg
CONSOLE_VARIANT=m3_r61520
参考：firstboot内容devices_ID
bittboy2x_v1
bittboy2x_v2
bittboy3.5
q20
q90
v90
pocketgo
pocketgo_TE
xyc_gc9306
m3_r61520
m3_rm68090
m3_hx8347d
m3_gc9306
（2）等安装后重命名firstboot文件为firstboot.done
```

## sdltest
* main.c from src_sdltest.7z of https://github.com/steward-fu/archives/releases?q=miyoo&expanded=true  

## TODO  
* (done)  
