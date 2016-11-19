# Hactonish

## 第一步 制作原版安装U盘+Clover引导

### 一，准备工作：
首先要有一个【Mac系统】，此操作均在Mac下进行
8G或者以上大小的U盘一个
原版安装镜像一个，是直接AppStore下载的APP文件，注意从网盘下载的DMG文件请挂载后将 【OS X Sierra】的文件拷贝到【应用程序】文件夹里。

### 二，制作步骤：
打开【磁盘工具】，将准备好的U盘进行【分区】操作，选择【一个分区】，格式为【Mac OS 扩展 (日志式)】，重点是命名，命名以后一定要记住，比如命名为【USB01】要区分大小写，那么记住它，接下来不要急着点【应用】，而是点下面的【选项】，选择【GUID 分区表】，选择之后再点【应用】对U盘进行格式化。到这里U盘就准备完毕了。

### 三，开始制作启动盘
请确保【OS X Sierra】在【应用程序】文件夹里。
打开【终端】，输入以下命令，

```bash
sudo /Applications/Install\ OS\ X\ 10.12.app/Contents/Resources/createinstallmedia --volume /Volumes/USB01 --applicationpath /Applications/Install\ OS\ X\ 10.12.app --nointeraction
```

按回车运行。

注意：USB01是你的U盘名字

回车后，系统会提示你输入管理员密码，接下来就是等待系统开始制作启动盘了。这时，命令执行中你会陆续看到类似以下的信息：

```bash
Erasing Disk: 0%... 10%... 20%... 30%...100%...
 Copying installer files to disk...
 Copy complete.
 Making disk bootable...
 Copying boot files...
 Copy complete.
 Done.
```

当你看到最后有 【Copy complete】和【Done】字样出现就是表示安装盘已经制作完成90%了，接下来最后一步也是最重要的一步就是安装【Clover】引导了。

### 四，安装Clover引导到U盘

用【Clover Configurator】挂载U盘的【EFI分区】，然后运行【Clover PKG】文件，选择安装到【U盘】，在【clover选项】界面，选在【安装Clover到EFI分区】，然后按个人的电脑进行clover配置，到这里整个启动盘就制作OK了。

如果没有 【Clover Configurator】，可用终端命令

```bash
diskutil list
// 找到U盘EFI分区的位置
mkdir /Volumes/EFI
sudo mount -t msdos /dev/disk1s1 /Volumes/EFI
// disk1s1 就是U盘EFI分区的位置，可能有所不同
```
## 第二步 用安装盘或者macOS PE引导已经安装好的系统

## 安装 AICPUPM Patch UEFI ，删除NullCPUPowerManagement，安装系列驱动

说明： 如果加入Clover不能正常启动，可以再用另一个U盘来制作Clover启动盘（比如在windows下用BDU制作，然后插入两个U盘进行安装)