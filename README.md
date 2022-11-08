# Project RisukaScope硬件系统
硬件系统主要分为以下几个部分：

## 电源
`/Power`文件夹。  
一个基于XL4016/SY8253的6~9V/5V/3.3V三轨供电系统。
此外还有一个给模拟前端用的5V模拟电源输出，用了一个LM1117-5.0。  
这部分十分臃肿，所以之后会做一个新的出来。

## 射频前端
`/RFFE`文件夹。  
前端LNA+滤波+多级Gain Block放大。  
前端LNA是NXP的BGU8009 GNSS LNA。  
滤波器是TA2494A。SAW滤波器，中心频率1420MHz，带宽80MHz。  
Gain Block用的是烂大街的SBB5089。  
Qucs仿真得到这个电路的增益~56dB，NF~0.66dB；实测增益48dB，NF因条件有限未测试。

## 调谐器与ADC
`Tuner ADC`文件夹。调谐器用的是各类SDR设备上常见的MSI001芯片，只用了L Band端口。实际试了一下应该有8MHz的带宽。  
ADC用的是AD9201，I/Q双通道同步采样ADC。  
系统采样率16MSPS。

## 通信与用户界面
`/Connectivity Interface`文件夹。
用了个ESP32-C3实现蓝牙/Wi-Fi通信。ESP32-C3通过SPI连接到FPGA。  
CD4504做缓冲器驱动舵机。  
预留了RGB LCD和以太网模块的接口。但目前还没用上。  
下面预留了八个机械键盘轴和两个电位器的位置，用于机械结构的操控。  
但后来想了想，感觉这样一点也不好用，不如直接遥控了。  
因为很多东西都没啥卵用，所以这部分也要大改。

## PMOD-Flash TinyRTC
`PMOD-Flash`文件夹。  
仿照Arduino平台上曾红极一时的I2C TinyRTC模块设计的PMOD Flash+RTC模块。  
一个W25N01 Flash+RX8010 RTC。RTC备份电源用的是硬币状的超级电容器。
