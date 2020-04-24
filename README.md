# phicomm-n1
斐讯N1盒子线刷软件及降级固件

N1系统降级：
在运行界面的版本号上点击4次, 至出现"打开adb", 这个状态重启后会保持
adb connect 10.0.0.6:5555
adb shell reboot fastboot
fastboot flash bootloader bootloader.img
fastboot flash boot boot.img
fastboot flash recovery recovery.img
fastboot reboot

N1电视固件的烧录：
adb connect 10.0.0.6:5555
将USB公对公插入盒子靠近HDMI的USB口，另一端插入电脑USB
adb shell reboot update
盒子应该重启进入黑色背景，中间显示PHICOMM
打开USB Burning Tool，导入需要烧录的img, 去掉Erase flash 和 Erase bootloader 这两项的勾选，点击“开始”
重启盒子

执行adb shell reboot update之后如果在设备管理器找不到libusb-win32 Usb Devices——WorldCup Device，将USB线和电源拔掉（如果不拔USB线盒子仍会通过USB供电），再连上USB，然后接通电源，盒子启动后再运行上述两条命令。


短接法强制进入线刷：
https://www.right.com.cn/forum/thread-308471-1-1.html
拆开盒子，将盒子主板用usb双公头线连接到电脑；
打开USB Burning Tool，导入需要烧录的img, 去掉Erase flash 和 Erase bootloader 这两项的勾选；
盒子主板背面印字上方有两个测试触点，短接这两点的后插入盒子电源加电（参看图片），
则盒子强制进入线刷模式并不会正常启动，此时电脑端windows发现新硬件，可以开始烧录；
短接可用金属镊子、回形针等等，手潮的新手注意安全。

如果烧录过程出现 [0x10103005]Romcode/初始化DDR/下载数据/读取镜像失败：
https://www.right.com.cn/forum/thread-308485-1-1.html
停止烧录，盒子断电，再点击“开始”，然后盒子加电即可开始烧录。


注册登录Google账户：
https://www.znds.com/tv-1119407-1-1.html

1. adb获取android id
adb pull /data/data/com.google.android.gsf/databases/gservices.db
sqlite3 gservice.db
"select * from main where name="android_id";

2.将安卓ID注册
https://www.google.com/android/uncertified/

3.清空缓存(非常重要)
安卓的设置 -> 备份和重置 -> 恢复出厂设置. 点击恢复出厂设置, 将之前的缓存清空. 不做这一步就去登录的话, 登录的时候框架会先检查此ROM是否已经注册, 如果之前尝试过登录, 在盒子里面有缓存, 他就会去优先读取缓存, 如果之前登录失败, 这个ROM未注册的信息就会一直在缓存里面, 导致即使你在谷歌那里注册了, 这个缓存的更新时间不知道是什么时候, 反正我一天了还没清空, 所以我直接恢复出厂了.

4. 登录账号
安卓的设置 -> 账号 -> 添加账号, 登录输入密码一气呵成. YouTube也能正常自动登录了

以上来源：kongkongyzt
也有朋友“bootless”提供了下面的经验

1、刷机或恢复出厂后要再查一次ID，变了在网站重新登记；
2、网站登记ID后需要一段时间才能注册过去，一开始注册后咋鼓捣也不行，结果第二天晚上就过去了；
3、N1可以不恢复出厂不停用Goog1e服务和商店，但添加账户前必须清空缓存。