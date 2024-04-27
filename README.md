# kdxf-studentpad-google
### 前言
刷入google服务主要分三种

1.adb法

2.提前预置

3.模块法

其中1,3都要root,2较为繁琐,我个人推荐3,如还未root请前往https://github.com/KDXF-BOOM/studentpad-research
进行破解。因为我google号没了无法添加 Google 认证,所以无法进行部分测试,如有问题请发邮件xxzzre@bytdbytd.eu.org或进群反馈

### adb法

大概思路参考https://blog.csdn.net/WTBEE/article/details/84571773
1. Open GAPPS下载Android9 arm64的GMS包
https://opengapps.org/
如果你不了解Variant差异的说明可以参考以下链接参考进行下载
https://cloud.tencent.com/developer/article/1545499
2. 下载好相应的包后请解压，其中Core和Optional下是GMS服务的一些核心文件和APK，是我们能否使用GMS服务的基础。GApps路径下是Google的一些原生应用，在GMS服务安装好之后可以根据喜好自行安装
3. 解压其中tar.lz解压后里面会有路径可以通过路径判断位置主要分为app,priv-app,common;common其实的内容其实是指system目录
4. 将这些文件分类为app,priv-app,system三个文件夹后使用adb指令

```
adb root
adb remount
adb push <地址>\app\. /system/app/
adb push <地址>\priv-app\. /system/priv-app/
adb push <地址>\system\etc\default-permissions /system/etc/
adb push <地址>\system\etc\permissions\. /system/etc/permissions/
adb push <地址>\system\etc\preferred-apps\ /system/etc/
adb push <地址>\system\etc\sysconfig\. /system/etc/sysconfig/
adb push <地址>\system\framework\. /system/framework/
adb push <地址>\system\lib64\. /system/lib64/
```
5,执行之后重启,然后通过[谷歌设备验证](https://github.com/zyzysu/kdxf-studentpad-google/edit/main/README.md#%E9%80%9A%E8%BF%87%E8%B0%B7%E6%AD%8C%E8%AE%BE%E5%A4%87%E9%AA%8C%E8%AF%81)
### 提前预置（还未实践）

1.解锁学习机bootloader参考[解锁bootloader]([https://github.com/KDXF-BOOM/studentpad-research?tab=readme-ov-file#%E5%88%B7%E5%85%A5system](https://github.com/KDXF-BOOM/studentpad-research?tab=readme-ov-file#%E8%A7%A3%E9%94%81bootloader%E6%9C%80%E9%87%8D%E8%A6%81%E7%9A%84%E4%B8%80%E9%9B%86))

2.通过spd_dump提取system参考[kdxf学习机分区提取](https://github.com/KDXF-BOOM/studentpad-research?tab=readme-ov-file#%E6%8F%90%E5%8F%96%E5%88%86%E5%8C%BA%E9%87%8D%E8%A6%81%E6%8F%90%E5%8F%96%E5%AE%8C%E8%AF%B7%E6%89%8B%E5%8A%A8%E5%B0%86system%E9%95%9C%E5%83%8F%E5%A4%8D%E5%88%B6%E4%B8%80%E4%BB%BD%E9%98%B2%E6%AD%A2%E5%87%BA%E6%84%8F%E5%A4%96%E7%8A%B6%E5%86%B5%E5%90%8E%E6%97%A0%E6%B3%95%E6%81%A2%E5%A4%8D%E8%87%B3%E5%8E%9F%E6%9D%A5%E7%8A%B6%E6%80%81)

3.Open GAPPS下载Android9 arm64的GMS包

https://opengapps.org/

4.修补system参考[Android 9.0 导入GMS组件及Google Play Store](https://www.cnblogs.com/blogs-of-lxl/p/14271830.html)

5.刷回改过的system参考[kdxf学习机刷入system](https://github.com/KDXF-BOOM/studentpad-research?tab=readme-ov-file#%E5%88%B7%E5%85%A5system)

6.通过[谷歌设备验证](https://github.com/zyzysu/kdxf-studentpad-google/edit/main/README.md#%E9%80%9A%E8%BF%87%E8%B0%B7%E6%AD%8C%E8%AE%BE%E5%A4%87%E9%AA%8C%E8%AF%81)

### 模块法

1.下载模块

2.安装并重启

3.通过[谷歌设备验证](https://github.com/zyzysu/kdxf-studentpad-google/edit/main/README.md#%E9%80%9A%E8%BF%87%E8%B0%B7%E6%AD%8C%E8%AE%BE%E5%A4%87%E9%AA%8C%E8%AF%81)

### 通过谷歌设备验证

1.获取GMS框架的Android ID

重启机器后,挂上代理，进入Play商店，等待出现设备未验证的提示，此时会生成一个GMS ANDROID ID

有两种办法获取id

* 1.通过 Device ID app获取id
  
 * 下载并安装[Device ID](https://github.com/zyzysu/kdxf-studentpad-google/raw/main/Device%20ID.apk)进入软件会有一串GSF的ID，这就是GMS ANDROID ID
 
* 2.通过adb获取
  
 * 运行以下命令获取id
   
   ```
   adb root
   adb shell 'sqlite3 /data/data/com.google.android.gsf/databases/gservices.db "select * from main where name = \"android_id\";"'
   ```

2.注册google设备id

挂上代理访问https://www.google.com/android/uncertified/
填入ID，点一下注册，等他有提示注册成功即可。
然后打开手机，把Google play商店清除全部数据并且强制停止运行,然后再打开Google play商店,如果还不行的话,等1小时候再登录Google play商店看看
