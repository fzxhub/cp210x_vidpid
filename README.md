# CP2102修改VID和PID


## 简介
CP2102可以修改VID和PID后使用，自定义名称等操作。
[官方文件下载地址](https://www.silabs.com/interface/usb-bridges/classic/device.cp2102)

## 说明
CP2102改动了VID和PID后，官方的驱动就不能识别硬件了，因此需要同时修改VID和PID和制作驱动。才能识别新的硬件。

## 修改VID和PID
使用官方的[CP210xSetIDs.exe](./software/CP210x_LegacyUtilities.zip)的可以修改VID和PID，本质是修改CP2102芯片中EEPROM的数据达到目的，有编写CP2102驱动的能力，通过官方提供的API也可以修改。

注意：
1. 锁定选项使能写入后，后面就不能在再次修改数据了，非量产谨慎操作。
2. 修改VID和PID后，如果相应VID和PID没有驱动，就不能识别硬件了，包括[CP210xSetIDs.exe](./software/CP210x_LegacyUtilities.zip)软件。

![改VID和PID](/image/1.png)

## 自定义驱动
修改了D和PID，后官方驱动就不能识别cp2102，因为在驱动的.inf文件中标注明确的VID和PID，只有在驱动的.inf文件中的VID和PID才能被识别成相应的驱动。

这一步实现方案有两种：
方案一：文件中增加VID和PID，即可，但是修改系统文件需要权限。
方案二：自定义驱动

1. 有官方文件[an220-usb-driver-customization.pdf](./datasheet/an220-usb-driver-customization.pdf)说明，使用[CustomUSBDriverWizard.exe](./software/AN220SW.zip)按照步骤继续就可以。
2. 在选择驱动类型的时候我选择仅inf，即可。
3. 注意在填入VID和PID的地方填入自己的VID和PID就可以。
4. 插入硬件，在设备管理中给带感叹号的驱动安装驱动，选择生成驱动的位置即可。

注意：自己制作的自定义驱动一般没有签名，操作系统关闭驱动签名即可。