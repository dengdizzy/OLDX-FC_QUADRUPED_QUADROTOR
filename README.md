
# 1 OLDX-MocoMoco四足机器人开发平台项目  
<div align=center><img width="600" height="130" src="https://github.com/golaced/OLDX_DRONE_SIM/blob/rmd/support_file/img_file/logo.JPG"/></div>
<div align=center><img width="400" height="300" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/fc2.jpg"/></div>

  ____OLDX-MocoMoco四足机器人（OLDX-MocoMoco Quadruped）是目前国内首个真正意义上的开源足式机器人二次开发平台，团队已经开发了一套完整的免费开源
  项目OLDX-FC，随着近年来波士顿动力公司不断推出的足式机器人引起了国内外许多爱好者的关注，也出现了许多电子发烧友自己开发的足式机器人，但
  不同于四轴飞行器仅采用无刷电机和机架就能进行开发，而足式机器人本身结构复杂特别是伺服驱动部分可以独立作为一个学科进行研究，因此造成了
  虽然有许多不错的足式机器人项目但是由于项目成本或者编程语言不为国内环境所熟悉的原因而阻碍了它们的推广或开源。团队4年前就开始研发的六
  足机器人具有丰富的机器人，通过将其与所开发的飞控项目二次结合推出了MocoMoco四足机器人开发平台，囊括机器人结构、步态算法和SLAM无人驾驶
  等多个足式机器人核心技术内容。项目遵循GPL协议，能对DEMO内相关源码进行修改和二次开发。<br><br>

**-如果该项目对您有帮助请 Star 我们的项目-**<br>
**-如果您愿意分享对该项目的优化和改进请联系golaced@163.com或加入我们的QQ群567423074，加速开源项目的进度-**<br>

<br>
**-由于本人非专业研究四足机器人，该项目只是基于个人学术水平开发并不代表目前足式机器人算法就是这样，请不要过分依赖项目内容或与正规产品对比-**<br>
	
# 2 MocoMoco四足机器人平台介绍

 <div align=center><img width="550" height="300" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/r2.jpg"/></div>

____MocoMoco四足机器人是一个8自由度足式机器人其借鉴了GhostRobtic推出的Minitature机器人，之所以没有像波士顿动力或其他开发者一样采用
12自由度机器人是因为其在维护难度和成本上都大大提升，而8自由度机器人实际能完美的模拟12自由度单轴的控制特性能快速学习虚拟腿和
虚拟力相关步态理论，仅损失了部分侧向移动能力。同时对小体积足式机器人来首先与自身移动速度其相比外部环境来说不存绝对意义上狭窄
的区域，能满足绝大部分室内外场景下的可靠移动。<br>
____另外驱动采用固定位置安装的方式使用寿命和维护难度都有较大的优势，适合实验调试中可能出现的损坏等情况。为降低伺服驱动成本将其采用的无刷电机替换为高性能舵机,采用碳板和3D打印件作为主体结构具有安装方便，容易维护的特点，是一个桌面级的四足机器人研发和SLAM算法验证平台。控制器方面采用了目前国内开发群体较多的STM32和树莓派，同时该硬件架构将在后续机器人项目中沿用将首先移植OLDX-FC飞控项目实现真正的
一板多用的目的。电路板硬件方面采用了一体化集成设计采用最小推出的树莓派A3+具有小体积高性能的特点能为后续图像、激光雷达SLAM提供开发可能，
控制板采用STM32F4作为处理器，板载3轴加速度计、3轴陀螺仪、3轴磁力计和气压计采用内减震设计，电路安装孔能完美与树莓派安装同时提供3D打印外壳。
控制板采用外部可更换供电模块供电具有12路PWM输出和4路AD采样，并外扩4路串口兼容正点原子推出的无线调试其方面机器人不同调试。

**控制器硬件参数：**

项目|参数
-------------|-------------
处理器|STM32F405RGT6
处理器性能|32Bit ARM Cortex-M4 168MH
陀螺仪 加速度计|LSM6DS33 
磁力计|LIS3MDL
气压计|MS5611
预留接口|GPS-1 串口-4 AD采样-4 着地开关输入-4
PWM 输出通道| 12通道输出 
供电|5V输入 舵机外部供电  AD传感器3.3/5V供电选择
图像处理器|树莓派A3+  1.4G 4核  带独立供电开关(控制板兼容树莓派全系列可作为外扩IO板安装，但通讯仅采用引脚串口)
遥控方式|2.4G射频 SBUS航模遥控
地面站|QGround   匿名地面站(需要额外OLDX-REMOTE监视器)

**机器人参数：**

项目|参数
-------------|-------------
足式机器人类型|8自由度并联机器人
尺寸|30cm * 20cm *10cm  
全腿长|8cm
重量|600g
供电|7.4V  18650 * 2(3000mah  续航>35 min) 带开关 
步态支持|Tort步态  Fly-Trot步态  波动步态
最大移动速度|0.4m/s
最大转向速度|30度/s
步态周期|>0.35 s
舵机性能|Kpower 12g金属舵机 *8(6V-60度/0.035s  9kg扭矩)
足底传感器|薄膜压力/微动开关(默认无传感器)
控制模式|遥控模式  姿态平衡模式(有/无着地传感器)  驾驶模式  


<br>
**控制器PCB接口说明：**
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/fc.jpg"/></div>
<br>

接口|说明(以图片视角)|支持模块
-------------|-------------|-------------
复位|控制器复位按键|
无线下载|从左到右：GND SCK SWD 5V|接正点原子无线调试模块
SWD|从左到右：GND SWD SCK 5V|接Stlink 转接板
GPS|从左到右：5V RX2 TX2 SCL SDA GND|接MINIGPS
足底传感器|从上到下： VCC GND AD1/SCL1 KEY_GROUND1/SDA1|接压力/开关/震动/测距
供电选择|水平跳帽从上到下：3.3V  5V|
SBUS|从左到右：GND 5V Signal|天地飞接收机WBUS  Futaba SBUS接收机
光流|从左到右: RX4 TX4 GND 5V|接光流传感器
数传|从左到右: TX1 RX1 GND 5V|接匿名数传 
树莓派|从左到右：TX3 RX3 GND 5V|树莓派A3
腿1|从左到右：GND VCC PWM   从上到下：外侧舵机  里侧舵机  机械臂/云台|舵机外部供电
电源|从上到下：BEEP 舵机供电使能 GND GND 5V  VCC舵机  VCC舵机 VCC电池|电源模块 

**注：控制器机体为RGB LED方向，上表中仅给出腿1 舵机接口和传感器接口引脚顺序，其余三个腿为镜像对称的结构，
即以腿2为例 从上到下为：外侧舵机  内侧舵机  云台  从左到右为：PWM VCC GND    腿2传感器 从上到下为：
KEY_GROUND2/SDA2  AD2/SCL2  GND  VCC**

# 3 DEMO测试
____该项目免费提供了基础测试的3D打印机架能免费下载自行打印，官方将推出全碳版本的机架请
关注淘宝店后续推出的第三方扩展模块，控制器同时兼任二者各版本机架所需螺丝型号如下：

金属件|数量(3D打印机架)|装配
-------------|-------------|----------
M3*30|8|安装机臂
M2*10|8|安装舵机
M3*5|8|安装腿
M3*10|4|安装足底
M3*15铜柱|4|中心体支撑
M1.4*4|8|固定齿轮
M2.5*3|4|安装电池盒
M2.5*5|8|固定控制器
M2.5铜柱*4|4|控制器支撑

金属件|数量(官方碳素机架)|装配
-------------|-------------|----------
M2*16|8|固定机臂
M2*5|8|安装舵机
M3*5|8|安装腿
M3*10|4|安装足底
M3*32铜柱|4|中心体支撑
M3*4|8|中心体固定
M1.4*4|8|固定齿轮
M2.5*3|4|安装电池盒
M2.5*5|8|固定控制器

**-搭建该项目的方式-**

方式|说明
-------------|-------------
整机购买|8
机架打印+控制器购买|8
机架打印+控制器制版加工|

## 3.1 机器人组装（官方机架）
### 3.1.1 机臂和中心体组装
(1)组装机臂，需要2个机臂碳素片、半圆3D打印件、中心体3D打印支持件，注意机器人机臂需要具有5°的外扩角度，注意上板卡槽为T字，下标卡槽为L字，同时用2mm螺丝加固机臂，结果如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a1.jpg"/></div>

(2)组装中心体，需要上下中心体碳素片、4个M3*32铜柱，首先将铜柱固定在底板上结果如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a2.jpg"/></div>

(3)安装机臂，将四个机臂固定在下板卡槽上注意要用5°外扩，结果如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a3.jpg"/></div>

### 3.1.2 安装电池仓、控制板和舵机
(1)首先安装电池仓，其安装在中心体底部并且开关方向朝向后方，结果如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a4.jpg"/></div>

(2)安装舵机，舵机安装采用轴承在下的方式,并且外侧舵机轴承朝向机体内部，内侧舵机轴承超外以保证腿部移动时不会受机体阻碍，用2mm自锁螺丝固定在碳板上，结果如下图所示:
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a5.jpg"/></div>

(3)安装控制板，将控制板安装在中心体上方，主要如没有安装控制器外壳则需要将控制器采用3D打印件垫高以防止电路板底部与碳板和电池仓估计螺丝短路，结果如下图所示:
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a6.jpg"/></div>

(4)连接舵机线，从机臂内部绕线将舵机线与控制板连接，具体连接顺序参照下标，另外注意PWM引脚朝向机体内部为5V供电即可，具体引脚供电顺序参考PCB IO图：

**舵机接线**
||
-------------|-------------|----------
Sch.PWM3 TIM3_3 [D_LEG] 外舵机1|机体右 |Sch.PWM6 TIM4_2 [D_LEG] 外舵机2
Sch.PWM2 TIM3_2 [X_LEG] 内舵机1| |Sch.PWM5 TIM4_1 [X_LEG] 内舵机2
Sch.PWM1 TIM3_1 NS| |Sch.PWM4 TIM3_4 NS
机头||机尾
Sch.PWM7 TIM4_3 NS| |Sch.PWM10 TIM8_1 NS
Sch.PWM8 TIM4_4 [X_LEG] 内舵机3| |Sch.PWM11 TIM8_2 [X_LEG] 内舵机4
Sch.PWM9 TIM1_1 [D_LEG] 外舵机3|机体左 |PSch.WM12 TIM8_3 [D_LEG] 外舵机4

### 3.1.3 连接电子模块和上板
(1)将降压模块与电池仓焊接，注意输入输出关系和正负极，结果如下图所示:
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>

(2)将降压模块通过XH2.8-8线进行连接，并将降压模块卡入底板后部卡槽，结果如下图所示:
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a8.jpg"/></div>

(3)安装上板，将上板与降压模块和机臂卡槽对应安装，采用螺丝将上板与4个支撑铜柱固定，结果如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a9.jpg"/></div>

## 3.2 腿部安装、偏差校准与IMU传感器校准
(1)组装腿部支持结构，首先不连接足底3D打印件以方便后续腿部偏差安装，将舵机附带的齿轮臂与3D打印件组装并采用1.25mm螺丝固定防止滑落，结果如下图所示:
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>

(2)连接下载器对机器人供电测试系统供电是否正常，DEBUG程序对腿部结构偏差进行校准：
a.首先将vmc_demo.c 文件下force_dj_off_reset加入watch中并在DEBUG中置为1将舵机偏差复位。<br>
b.将vmc_all.sita_test[4]置1此时舵机会被供电转动到默认偏差下的90°。<br>
c.将安装好的大小腿以大约90°垂直舵机的方式进行安装，如下图所示：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>
d.修改vmc[i].param.PWM_OFF中的偏差参数，[0]对应外侧舵机角度[1]为内侧舵机通过调整参数和目视校准保证舵机90°绝对垂直，完成对4只角全部校准后用舵机配套螺丝固定轴承。<br>
e.将mems.Gyro_CALIBRATE置为1，将当前标定后的偏差存储在FLASH中。<br>
f.复位芯片查看读出的偏差是否一致
<br>

(3)校准IMU传感器，将机器人以电池仓水平放置进行传感器零偏校准，将mems.Gyro_CALIBRATE和mems.Acc_CALIBRATE分别置为1完成陀螺仪和加速度计的校准。<br>
**注：对加速度的标定会觉得姿态解算0°在哪，而如果存在偏差会导致机器人移动稳定性出现移动中向左或右偏离。因此在后续对一些
控制参数和舵机偏差标定进行FLASH保持时建议仅对mems.Gyro_CALIBRATE置1**
<br>

(4)安装足底3D打印件，如有足底传感器在控制板上连接对应传感器，最后完成整机的组装：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>

## 3.3 移动测试


## 3.4 使用STLink或正点原子无线下载器调试
____使用下载器转接板与控制板进行连接，需要4P双头卡槽线、USB转接小板和大板以及一根micro USB线，连接后结果如下：
<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>

如采用正点原子无线下载器则请参考项目中附带的说明pdf文件，另外两种下载方式不可以同时使用。

## 3.5 高度和姿态Sin期望跟踪测试
____足式机器人基础稳定最重要的同样是基于IMU实现姿态自稳，通过在DEBUG模式下修改gait_test[i]能实现给定高度、俯仰角的Sin轨迹进行跟踪，
以验证控制器和参数的可靠性。通过在原地验证在再移动中验证可以看出不同步态算法的性能差距，在仅依靠舵机开环和无着地传感器前提下能实现的
最优步态效果如下：<br>
(1)不断跨腿下，机体高度能平滑变化<br>
(2)不断跨腿下，俯仰角能平滑变化<br>
(3)移动中同时实现上述过程<br>
(4)在可倾斜板子上验证姿态平衡，板子倾斜机器人快速反应保证机体平衡<br>

gait_test参数|说明
-------------|-------------
0|1高度  2俯仰角  3力矩测试
2|角度增量
3|幅值

**注：力矩测试是为了验证力矩闭环是否能够保证足尖跟踪给定曲线通过调节vmc_all.pid[Zr][P]/[D]适用不同驱动系统，另外修改UART_UP_LOAD_SEL=1
可在上位机上查看足尖期望反馈曲线**

## 3.6 参数调节
### 3.6.1 参数介绍
参数|说明|默认值
-------------|-------------|-------------
PID7-P|高度 内环P|500
PID7-I|高度 内环I|300
PID7-D|高度 内环D|1680
PID8-P|高度 外环P|1000
PID8-I|高度 外环I|100
PID8-D|高度 外环D|0
PID12-P|高度 ADRC b0|15
PID12-I||
PID12-D|高度 ADRC 死区|10
### 3.6.2 上位机回传数据

## 3.7 DEMO程序优化和后续开发建议
____DEMO程序为用户提供了一个最简单和四足机器人开发框架，包括了姿态解算和核心步态算法。所提供的步态算法以虚拟力为基础
通过雅克比矩阵输出扭矩，由于使用舵机因此仅通过简单的PD控制器变换为舵机旋转速度。在步态方面DEMO成像的整个状态机调度
结构与机器人库一样，只是简化了其中姿态控制策略采用了更简单直接的力控制方式，易于理解四足机器人最基础控制理论并能进一步进行
优化和改进。如果想深入对该项目进行开发并用于大型机器人中建议进一步研究SLIP模型、阻抗控制和柔顺控制理论，另外四足机器人
的核心有60%以上在可靠的伺服驱动，高效的伺服驱动系统能实现在最简单Sin轨迹+CPG算法下的可靠移动这一点已经被许多论文所
证明，机器人腿部结构设计也能在一定程度上提供自身稳定性。综上，后续升入开发建议如下：<br>
（1）优化腿部结构增加被动缓冲，构建12自由度机器人，增加着地传感器反馈<br>
（2）引入机器人倒立摆模型和基于模型先验知识下的优化控制、力矩控制<br>
（3）替换驱动系统采用无刷直驱或行星减速的结构提高各腿的一致性<br>
（4）引入视觉导航信息提高机器人移动的稳定性和足端轨迹的合理性


# 4 SDK开发
____该项目采用开源+机器人控制库授权的方式，即提供一个能运行机器人平台的基础项目源码同时提供高性能的闭源机器人控制库，
开源程序能进行修改和二次开发官方也会后续不断完善并与闭源机器人库一致。闭源机器人库则预留了完整的调用接口能基于SDK
快速地对机器人速度，姿态，足端轨迹，力矩等进行控制读取机器人位姿融合数据，即可采用现在SLAM小车底盘的开发方式对机器人进行
控制，二者具体功能区别如下：

**OLDX_VMC四足机器人数学库与开源DEMO版本的区别：**

项目|开源程序|闭源机器人库
-------------|--------------|-------------
步态算法|Trot|Fly-Tort  Tort  波动步态
步态理论|虚拟力|虚拟力
跨腿轨迹|摆线|最小Jerk轨迹  地面角度动态调节
足底传感器|无|压力  微动开关  震动传感器  距离传感器
图像导航|SDK开发|SDK开发
姿态控制|虚拟力闭环|位置+虚拟力闭环
速度闭环|机械参数估计|光流/视觉+机械参数估计
位置闭环|无|最小Jerk轨迹规划+ADRC轨迹跟踪
导航|光流  UWB  GPS|光流  UWB  GPS

## 4.1 获取授权库
____四足机器人数学库目前仅支持STM32F4系列单片机，数学库与单片机ID绑定一次性购买后则能永久使用且享受后续版本库的更新。
获取数学库前首先需要下载源码在watch中寻找并提供vmc_all.param.board_id对应的3个id。在向官方提供该ID并获取对应License
后修改源码中如下位置后即可正常使用否则在使用vmc.lib时不会为腿部进行供电和规划步态：

```
void vmc_init(void)
{ 	char i;
	get_license();
	//设置License
	vmc_all.param.your_key[0]=143;
	vmc_all.param.your_key[1]=42;
	vmc_all.param.your_key[2]=180;
```		

注：使用Demo程序需在vmc.h中定义#define USE_DEMO 1 否则默认使用数学库

## 4.2 步态测试
____采用VMC步态库时的测试方法与DEMO程序一样，同样可以进行Sin轨迹跟踪来测试步态性能的提升，另外更实际的方式是进行移动和
上下坡测试，用户可以通过使用步态数量高度的书本搭建楼梯、坡和障碍物，在桌面或室内完成步态算法的验证和测试，或者构建一个竞技场
与好友在后续图像自主控制中进行PK，如下图所示：

<div align=center><img width="540" height="460" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/a7.jpg"/></div>


## 4.3 参数调节

参数|说明|默认值
-------------|-------------|-------------
PID7-P|高度 内环P|500


## 4.4 将控制器用于其他四足机器人
(1)足端轨迹输出<br> 
如采用其他腿部构型的舵机驱动机器人可自行编程将vmc[i].epos转化为对应角度通过串口通信发送给用户的驱动控制器。<br>  
(2)力矩输出<br> 
如采用相同构型的无刷驱动机器人则可将vmc[i].torque力矩作为输出通过通讯发送给伺服驱动,同时通过调节vmc_all.gain_torque来进行力矩单位的匹配。

## 4.5 SDK开发
____机器人开发采用ROS框架机器人控制器将作为一个硬件节点解算顶层控制命令，对机体中心点的姿态、速度和位置进行控制，同时也可以
对足端轨迹和力矩进行直接赋值。
<br>

target_track_downward_task|下置相机目标跟踪
-------------|-------------
target|目标图像信息结构体
spdz|下降速度
end_z|下降停止高度  
mode|模式 MODE_SPD：使用像素偏差  MODE_POS：使用估计的全局位置
完成条件|达到下降高度


# 5 捐赠与项目后续开发计划
____团队计划后期推出5kg~10kg级的足式机器人开发底盘，支持RPlidar激光雷达导航进行SLAM算法验证，能以相同的价格替代目前市面上同类的四轮小车平台如Autolabor等。
 <div align=center><img width="800" height="300" src="https://github.com/golaced/OLDX-FC_QUADRUPED_QUADROTOR/blob/rmd/support_file/img_file1/r1.jpg"/></div>
____如果您觉得该项目对您有帮助，也为了更好的项目推进和软硬件更新，如果愿意请通过微信捐赠该项目！
<div align=center><img width="240" height="300" src="https://github.com/golaced/OLDX_DRONE_SIM/blob/rmd/support_file/img_file/pay.png"/></div>





