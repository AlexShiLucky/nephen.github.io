---
layout: post
title:  "Robot测试与方案"
categories: "work_lifes"
author: Lever
tags: 工作
comments: true
update: 2016-04-27 01:42:47 Utk
---
<br>
#测试性能参数选项
参考淘宝记载的工业机械臂相关信息统计及项目实际情况，包括具体的测试手法的方案，归纳总结具体如下叙述。

产品参数部分：

1. 开关电源电压、控制部分供电、舵机部分供电、功耗、最大电流 -> 电气工程师实际测量后提供
2. 内部元件整体展示、基础模块、机械臂清单（电路板元件介绍） -> 电气工程师与结构工程师共同提供
3. 物理特性（产品重量、自由度、可夹持物品重量即负载能力、夹持器张角距离、夹持器整体长度、材质）-> 实际测量
4. 控制方式 -> 自主编程
5. 产品尺寸图 -> 结构设计师提供
6. 产品手册 -> 结构设计师与软件工程师共同提供

<!--more-->
产品性能部分：

1. 水平行程 -> 实际测量
2. 垂直行程 -> 实际测量
3. 重复定位精度
 - 检查舵机上电后，机械臂各电机关节是否是不可手动转动的，这样可以减少硬件上不必要的误差。 
 - 下载最新加入测试方案的固件，机械臂通过运行一定的动作后点击手机屏幕（手机固定于桌面），打开手机端测试APP，手机端APP感知机械臂点击位置即坐标（包括x，y），通过统计10次或者更多次数数据的方差来确定水平方向的重复定位精度，测试结果通过APP计算得出。-> 实际命令$En，其中n为数字1~9，重复运动该数字的10倍。
4. 最大单轴角速度 -> 该测量步骤在固件里面自动进行，如需测量A轴的角速度，通过上位机或手机APP点击测量后，机械臂的A轴会转动，固件会计算转动的时间，然后通过角度除以时间来获得角速度，并将结果返回给上位机或APP。-> $Ax，其中x为字母A~B,X，分别表示测试各个轴的最大角速度。
5. 各轴运动范围 -> 实际测量

#广告效果
产品包装可以参考[定制六轴机器人机械臂手臂工业多轴机械爪数控机械多行业自由应用 ](https://item.taobao.com/item.htm?spm=a230r.1.14.183.FGiDPM&id=541772986687&ns=1&abbucket=16#detail)，主要是从效率方面为客户着想。另外还可以从企业特色、应用领域等方面入手。

#方案计划
`Raspberry Pi 3`板是机器人的“大脑”，并与Arduino板通信以控制电机。它还从传感器获取数据，以便机器人可以根据其环境调整其行为。所有的重型计算都是在Raspberry Pi上完成的，所以机器人可以用于更多有趣的应用程序。    
`ROS`表示“机器人操作系统”。它是一个开源工具套件，帮助机器人变得更强大。ROS实际上用在Rasperry Pi 3板上。它保持机器人的模型在3D空间中执行高级计算。    
不要忘记什么是`开源精神`：从他人的工作中获益，并回馈社会。    
我们选择了`Arduino Mega`板，因为我们发现Arduino Uno容量对我们的需求太有限，我们想要与RAMPS 1.4屏蔽接口。    
你将能够购买一个可访问的机器人，就像你可以得到一个负担得起的3D打印机。
URDF教程将逐步指导您创建机器人手臂的模型，并在Gazebo模拟器中运行。一旦您有一个urdf和控制器在Gazebo中运行，您可以使用arm_navigation向导为您的手臂配置我们的运动规划算法。

MoveIt！现在已经被社区使用了超过65个机器人。此[页面](http://moveit.ros.org/robots/)收集有关使用MoveIt的信息！与不同的机器人。点击各个机器人以查看详细信息。