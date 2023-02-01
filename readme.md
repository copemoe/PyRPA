## 基本说明：

本项目灵感来自B站UP主：“不高兴就喝水”的 https://www.bilibili.com/video/BV1T34y1o73U 视频，特此鸣谢。
本程序目的同样是代替在PC上需手动在指定位置按照特定流程点击、输入等重复性的操作。

基本工作流程及原理为对该当前目录下的Source文件夹下的任务文件夹(子文件)里的xls表格逐行遍历，当屏幕中出现xls中的图片名所对应的图像区域时则会按当前行的参数设定以及全局设定执行当前行的相关操作，图片名字不填写时直接执行动作。

【更新记录】  

-V0.8.1 初始版本：   
1、中文字符指令方便记忆。   
2、图片支持超时方式查找，超时时间，超时动作，都支持设置，完全闭环不会失控。(也支持非图片模式)    
3、可界面配置启停热键和运行次数，日志开关。    
4、热键启动后自动最小化窗口，运行状态在屏幕左上角小标签显示，运行结束弹出通知。   
5、可在界面选择数据源(任务文件夹)，支持免退出程序切换任务和修改数据。    
6、新增多项执行动作(涵盖日常90%操作)。    
7、EXCEL单行的执行动作支持多个命令的任意混合。    
8、点击位置支持偏移量设置。   
9、单个功能支持临时使能失能。    
10、任务结束可以选择其它任务继续运行或者重新运行当前任务。    

-V0.8.2：   
1、修复调用系统命令时不支持用路径启动应用程序的问题。  

-V0.8.2.1：  
1、修复因修复上一条问题导致的调用系统命令阻塞问题。     

-V0.8.3：  
1、修复滚动问题。

-V0.8.4（重要更新）：  
1、修复部分用户出现打开后只有准备标签，没有界面的问题。   
2、增加表格填写时的容错率。   
3、输入指令由模拟键盘打字改成直接输入字符，这将支持直接输入中文。   
4、新增找图超时时间参数-1（无限等待）。    

-V0.8.5（重要更新）：  
1、修复因超时行为为跳过时，下次遇到非跳过的鼠标还是会执行之前的动作的情况。    
2、新增鼠标左右键的按下和释放操作，但请配套使用。    
3、优化点击策略。    
4、弹窗时按下停止热键的同时关闭弹窗提示。   

-V0.8.5.1：  
1、修复因优化V0.8.5中的点击策略导致的偏移指令失效问题。 

-V0.8.5.2：  
1、支持多开，但程序关闭时间会增加几秒。     

-V0.8.5.3：  
1、修复非找图模式下的点击问题。     

-V0.8.6：  
1、新增跳转指令，可以在超时行为和执行动作中使用。   
2、新增音频播放，可以作为无人值守时的提示音。

-V0.9.0：    
1、更现代化的样式，暗黑和白色主题。   
2、禁用-c版本的关闭按钮。

-V0.9.3：    
1、新增打开自动运行，结束自动退出功能。


【常见问题】  
某些应用无法点击：  
将工具右击选择 【属性】 - 【兼容性】 - 【以管理员身份运行此程序】 打勾。
打开异常：  
测试环境是Win10 64位，如果与你电脑系统不同可能会出现问题，可以尝试在自己的电脑上用源码重新打包。



## 操作项说明：

操作项是指对应任务文件夹中的表格文件的第一行，其中：   
[A1] 功能备注：起备忘作用，程序不参与运行。   
[B1] 启用该项：1为启用，0为禁用。禁用后将跳过该项继续执行下一项。  
[C1] 图片名：   

| 不填写时                                             | 填写时(xxx.png)                                              |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| 非找图模式运行，也即遍历到该行就运行，没有触发信号。 | 输入在屏幕上要找的图片区域的截图，PNG格式。 默认找到后第一个动作将鼠标移动到找到的区域中心点。 |

[D1]超时时间(秒)：指等待当前屏幕要找的图片出现的最大时间，超时没找到将执行**超时行为**，该项为0时只找一次。参数为-1时不执行超时行为，也即一直等待图片出现(V0.8.3之后版本)。  
[E1]超时行为：    

| 弹窗  | 表示弹窗提示(有阻塞作用，用户可以在这期间进行检查)。 |
| ---- | ------------------------------------------------------------ |
| 跳过 | 不提示直接跳过该条，不再等待。                          |
| 退出 | 退出当前任务文件夹下的Excel表，等待下次开始热键按下。        |
| 跳转=x | 跳转到x行(以Excel实际行号为准)。 |

[F1]找图间隔(秒)：当超时时间不为0时，在超时时间内，上次没找到图后开启下次找图的时间间隔。  
[G1]执行动作：[指令]=[参数]

| 左键=X          | 左键点击X下                                                  |
| --------------- | ------------------------------------------------------------ |
| 右键=X          | 右键点击X下                                                  |
| 中键=1          | 鼠标中键按下                                                 |
| 偏移=x/y        | 鼠标相对位移                                                 |
| 移动=x/y        | 鼠标移动到绝对位置                                           |
| 鼠标拖拽=x/y    | 鼠标左键按下并拖拽到指定位置                                 |
| 相对拖拽=x/y    | 鼠标从当前位置拖拽 例如“相对拖拽=10/0” 从当前位置向右拖拽10像素 |
| 按键=enter      | 模拟按键按下enter                                            |
| 输入=hello      | 输入字符信息hello                                            |
| 等待=2          | 等待2秒                                                      |
| 滚动=-2000      | 屏幕向上滚动2000像素                                         |
| 热键=ctrl+alt+q | 模拟热键操作ctrl+alt+q                                       |
| 命令=notpad     | 调用系统CMD并打开记事本                                      |
| 截屏=1          | 全屏截屏(默认保存在当前目录的Screenshot)                     |
| 弹窗=hello      | 弹窗hello                                                    |
| 左键按下=1      | 按下鼠标左键（请与释放配套使用）                             |
| 左键释放=1      | 释放鼠标左键                                                 |
| 右键按下=1      | 按下鼠标右键（请与释放配套使用）                             |
| 右键释放=1      | 释放鼠标右键                                                 |
| 播放=file       | 播放Source目录下的音频文件，file支持MP3和WAV格式。           | 
| 跳转=x          | 跳转到x行(以Excel实际行号为准)。                            |
## .ini文件说明：
1、[SAVE] 字段保存工具上次的配置，方便在下次读出； 其中theme = 0 或 theme = 1 来变更配色。
2、[TASKCFG] 字段设置任务文件夹Source下的文件夹名，若有值则运对应任务；自动开始自动结束并退出。可以配合window 计划任务实现定时运行。


## 注意事项：

0、任务文件夹名、图片名、表格名是任意的**英文字符**(格式要为xls)，但是表格的第1行属性必须不变。   
1、指令部分名称必须是以上方式，并且大小写一致，参数部分为数字或小写字符。   
2、动作与动作之间用中文逗号隔开,各个动作可以任意组合，列表也可任意扩展。   
3、截图时尽可能小的图片可以提升运行速度，尽可能大的找图间隔可以降低CPU占用，但响应会变慢。        

## 使用指北：

详细使用教程请查看视频 https://www.bilibili.com/video/BV1KL411j7qs/ ，***\*版本更新记录在视频置顶评论区更新，版本地址在视频简介查看\****。  

​	一般的，“启用该项”用于测试期间的临时启用和禁用。 “按键”指令用于按下单个按键，如果你需要输入字符，请使用“输入”指令（配合“热键”切换输入法状态），如果需要调用热键请使用“热键”。 https://blog.csdn.net/sinat_41870148/article/details/109772114 这里是pyautogui包含的按键类型。

​	“偏移”是用于某些场合要点击的位置不是图片中心点情况，比如在保障识别的图片的唯一性的同时无法保证要点击的位置就是图片中心(这时候可以在执行动作第一项使用“等待”延时命令“慢放”执行动作前鼠标被移动的位置，若有必要，则使用“偏移”，否则重新截图)。      
​	"弹窗"指令可以用于暂停操作并提示,在这期间你可以使用热键停止或者继续。   
​	在V0.8.6版本中你可以使用“跳转”进行某一部分表格的循环控制或者“接龙”，使用“播放”进行无人值守时的提醒。  
​	在V0.9.0及之后版本支持主题切换并重绘制了界面(修改ini文件中的theme=1或=0)。    

Tips:虽然程序经过很多轮测试，修改了多种可能引起异常的BUG。但是还是会有一些因操作不当引发的问题，这样的情况请直接查看日志自行解决。 



## 责任和义务：

当你使用本程序后即表示同意以下条例：   
任何人不得以任何方式倒卖本开源程序。     
使用该程序不当给你造成的任何损失，作者不予承担风险。    
本程序初衷为开源学习并代替手动重复性的操作，不可用于任何非正规途径。      



## 针对二次开发：

程序用到的环境和依耐库以及一些说明请移步源码查看注释。



## 结束语：


祝你玩的开心！ 记得三连。

作者邮箱： chundong_cindy@163.com
