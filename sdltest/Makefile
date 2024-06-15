all:
	/home/wmt/work_q90/arm-buildroot-linux-musleabi_sdk-buildroot/bin/arm-linux-gcc main.c -o sdltest -ggdb -lSDL -I/home/wmt/work_q90/arm-buildroot-linux-musleabi_sdk-buildroot/arm-buildroot-linux-musleabi/sysroot/usr/include/SDL -lSDL  -lpthread  -lm  -lasound -lm -ldl 

#-L/opt/miyoo/arm-miyoo-linux-uclibcgnueabi/sysroot/usr/lib

clean:
	rm -rf sdltest

run:
	sudo cp sdltest /media/wmt/MAIN/
	sudo cp sdltest.sh /media/wmt/MAIN/
	sudo cp sdltest /media/wmt/rootfs/bin/

