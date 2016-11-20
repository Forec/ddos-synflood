# SYN Flood 拒绝服务攻击
> This project is a simple DDos attack tool based on SYN flood. Written in C++, using libnet. I wrote a tutorial at [http://blog.forec.cn/2016/11/20/ddos-syn-attack/](http://blog.forec.cn/2016/11/20/ddos-syn-attack/).

# Platform
* The code is written under Windows 10, in VS Ultimate 2013, version `12.0.21005.1 REL`. 
* [中文版安装指南看这里](http://blog.forec.cn/2016/11/20/ddos-syn-attack/)
* To configure the libnet package, you need to download its newest source code from [here](https://github.com/sam-github/libnet/tree/master/libnet), and then install `WinPcap` by this [installer](http://www.winpcap.org/install/bin/WinPcap_4_1_3.exe). After that, download `WpdPack` source code from this [link](http://www.winpcap.org/install/bin/WpdPack_4_1_2.zip). Unzip the libnet and wpdpack compressed package.
* Assume that you unzip libnet's package to `E:\libnet-1.2-rc3`, unzip wpdpack's package to `E:\WpdPack`. There's a folder `win32` in `E:\libnet-1.2-rc3\libnet`. You need to build a visual studio project, using the codes in that folder. 
* Configure the project: there're two folders named `include` in `E:\libnet-1.2-rc3\libnet` and `E:\WpdPack`, here it should be `E:\libnet-1.2-rc3\libnet\include` and `E:\WpdPack\include`. Add the two paths into the `Include` path of the project (in project settings, choose VC++ path, and you will see this option).
* Add the lib path of WpdPack into `Lib` path of the project, here it should be `E:\WpdPack\Lib`.
* Edit the `in_systm.h` under `E:\libnet-1.2-rc3\libnet\win32`, add the following definitions at the end of file:
```C
typedef char int8_t;
typedef short int16_t;
typedef int int32_t;
```
* Now you can build by press `F7`. You will find `Libnet.dll` and `Libnet.lib` under `E:\libnet-1.2-rc3\libnet\win32\Debug`. Copy them to `C:\Windows\System32` and `C:\Windows\SysWOW64`. After the upper steps, you have configured libnet already.
* You can now create a VS project containing the two files in this repository: `SYNFlood.cpp` and `wingetopt.h`.
* Setup the project settings, add `E:\libnet-1.2-rc3\libnet\include`, `E:\libnet-1.2-rc3\libnet\src`, `E:\libnet-1.2-rc3\libnet\include\libnet`, `E:\WpdPack\Include`, `E:\WpdPack\Include\pcap` into the project's VC++ include path.
* Add `E:\WpdPack\Lib`, `E:\WpdPack\Lib\x64`, `E:\libnet-1.2-rc3\libnet\win32\Debug` into the VC++ library path.
* Add `libnet.lib` to the addtional entries of linker.
* Add `E:\libnet-1.2-rc3\libnet\win32\Debug` to the additional library paths.
* Generate the executable file now.

# Usage
* You can download a compiled binary file from [here](http://7xktmz.com1.z0.glb.clouddn.com/synFlood.exe).
* Three optional flags are provided:
 * `-t` : set the target ipaddress and port, using the format of `192.168.1.193.80`, here 80 is the target port, and `192.168.1.193` is the target ip address.
 * `-s` : the number of attacing packets to be sent per second. By default, it will send in maximum speed.
 * `-p` : number of threads to send packets per second. Default is 1 thread.
* For example, run `synFlood.exe -t 10.3.8.211.80`, it will send syn packets to 10.3.8.211:80 at maximum speed with 1 thread.
* You can use `wireshark` to capture the SYN packets sent.

# Running status
Use the program to attack my CVM, the `wireshark` captures those SYN packets. However, since the provider of my CVM has defense for DDos attack, I didn't see any thing wrong with my website server running in CVM.
<img src="http://7xktmz.com1.z0.glb.clouddn.com/syn-flood-attack.jpg" width="400px"/>

# Update-logs
* 2016-11-20: Add this project and build repository.

# License
All codes in this repository are licensed under the terms you may find in the file named "LICENSE" in this directory.