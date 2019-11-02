# 单片机板贪吃蛇
![](https://img.shields.io/badge/language-c-red.svg)
![](https://img.shields.io/github/license/stevenling/gluttonous-snake)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/)

## 引脚连接

LPC 位置 | 外接器件位置 
:-: | :-: 
LPC1768->P2.0-P2.7 | LED点阵R1-R8
LPC1768->P0.4-P0.11 | LED点阵C1-C8
LPC1768->P2.10 | 按键‘w’
LPC1768->P2.11 | 按键‘a’
LPC1768->P2.12 | 按键‘s’
LPC1768->P2.13 | 按键‘d’
LPC1768->GND |  所有按键另一侧

## 整体连接图

![](https://github.com/stevenling/gluttonous-snake/blob/master/src/%E5%8D%95%E7%89%87%E6%9C%BA%E6%95%B4%E4%BD%93%E8%BF%9E%E6%8E%A5%E5%9B%BE.jpg)

## 程序流程图

![](https://github.com/stevenling/gluttonous-snake/blob/master/src/%E7%A8%8B%E5%BA%8F%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## 程序设计过程

1. 蛇位置的初始化
2. 放置食物
3. 扫描实体按键控制蛇的方向
4. 判断蛇是否吃到食物
5. 吃到食物则统计分数并重新画蛇的长度
6. 分析蛇是否撞到自己或墙
7. 撞到游戏结束否则回到第 2 步

## 具体情况及处理
- 蛇运动的处理  
  根据用户输入按键进行柔体移动

- 吃到食物的处理  
  吃掉食物把食物标志清楚，把食物的位置放入蛇的矩阵里。

- 放新食物的处理  
    判断食物标志，没有食物，放食物，判断是否与蛇身重叠，重叠了重放。

- 死亡的处理  
    撞到自己的身体，撞墙


## 遇到的问题与解决方法

- 问题一：一开始利用8*8点阵，1088BS模块的上下两排引脚对应的R1-R8及C1-C8是错开的，从一开始就错误了

- 解决方法：利用网上的1088BS模块来确定引脚的正确输入和连接，对应的用引脚在LPC168接到8*8点阵，及利用2.10-2.13对应的外部中断来实现上下左右按钮的判断及输入

- 问题二：蛇头吃到食物后如果显示新的蛇？

- 解决方法：在蛇吃到食物后，直接将这个食物位置标志为新的蛇头位置。 

- 问题三：由于事先已经规定好了点阵的 XY 轴方向，但是按钮的上下左右方向错位

- 解决方法：修改代码将实际硬件人为规定的上下左右与代码中的上下左右进行匹配，在此之后的蛇身增加长度或是蛇身移动的闪动对应的 XY 轴加一或减一来实现按钮方向上在实际面包板上和代码上是一致的。

- 问题四：如何增加游戏体验？

- 解决方法：设计关卡环节，后面的关卡蛇移动的速度越来越快，每个关卡给三次闯关的机会，每次死亡后可以接着本关卡的挑战，直到累计三次死亡游戏直接结束跳回第一关卡。

- 问题五：还有新的功能吗？

- 解决方法：通过 LPC168 数码管来显示游戏结束后得到的分数，后来发现数码管的接口被 8 * 8 点阵所占用，后来通过 8 * 8 点阵来显示分数，更为直接。为了区别分数和关卡，将分数的点阵显示外围显示带有一个框框并且闪动数次。


## 视频演示

[贪啊贪吃蛇-哔哩哔哩](https://www.bilibili.com/video/av11734759)

## LICENCE
[MIT](https://github.com/stevenling/chat-room/blob/master/LICENSE)
