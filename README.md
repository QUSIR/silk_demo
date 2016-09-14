# 使用说明
1.在src目录下执行make命令生成静态链接库

2.在test目录下有相应的编解码的例子程序


以上工程是在新塘`N3292x`平台下交叉编译成功


如果想修改编译器可修改`src`目录下的`makefile`文件

	target = libsilk.a
	includes=-I ./
	flags=
	silk_objects = *.c
	
	CC = arm-linux-gcc
	
	ortp.o : $(ortp_objects)
		$(CC) -c $(silk_objects) $(includes) $(flags)
		ar rcs $(target) *.o
		cp $(target) ../ 
		
	clean:
		rm *.o



将以上的`CC=arm-linux-gcc` 修改为`CC=gcc`

##测试指令

编码

	./SILK_Encoder compare.pcm tmp.bit -Fs_API 8000 -packetlength 60 -rate 8000
解码

	./SILK_Decoder tmp.bit tempme.pcm -Fs_API 8000


编解码过程中生成中间文件为`tmp.bit`文件，以上`SILK_Encoder`和`SILK_Decoder`由`tset`目录下测试程序生成

