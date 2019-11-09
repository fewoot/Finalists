# 2020-5月机器人格斗大赛赛前准备  
###### 创建日期：2019年10月31日10:40:24  
----------------------
## 准备-任务：

### 1.测量铲子和绝对平面的间隙（铲子下底面平整度）  
资料：
1. > Flatness is can be measured using a height gauge run across the surface of the part if only the reference feature is held parallel. 
You are trying making sure that any point along the surface does not go above or below the tolerance zone. 
Modern CMM’s are best for measuring the part as they can create virtual planes that the true surface profile can be compared to. 
This is a 3D measurement so points must be measured across the length and width of the part to ensure the entire surface is in tolerance. 
Flatness cannot be measured by simply placing the part on a granite slab and running a height gauge or microheight over it. 
This would be measuring parallelism instead as you are fixing the bottom of the part as a datum.  

摘自  [GD&T国外网站，平整度](https://www.cnblogs.com/wj-1314/p/8547763.html)

2. >  The problem is severalfold. 
The first issue is that flatness is only measured against itself, there is no datum reference plane. 
The second issue is that how can you be absolutely sure (short of a 3D laser scan) that you have actually found the highest point as you reference. 
The three point (column) method serves to establish a starting point and not really a datum reference. 
Recall that 3 points define a plane that should in reality be a pretty good representation of the surface you are checking. 
Then you can take your indicator probe and sweep the surface with flatness.
Another method of checking flatness is to do the following. Your inspection table has a hole in it just large enough to pass a dial indicator probe through. 
You place the surface you are checking for flatness in contact with both the inspection surface (and the dial indicator probe). As you move the part over the prove it will move up and down. This reading is telling you what your flatness error is.

摘自  [国外讨论，平整度](https://www.gdandtbasics.com/flatness)

3. > The flatness control may be inspected as follows:
The part’s surface is placed on a surface plate. This surface plate represents one of the flatness control tolerance zone planes.
A dial indicator is placed in a hole in the surface plate and measures the distance from the plate’s surface to the part’s surface. 
As the part is rotated, the measuring instrument must up or down the part and the profile of the cylinder is captured.
The part’s surface is moved over the hole at random. If at any time the FIM (full indicator movement) is larger than the flatness control tolerance, the part is not within specifications.

摘自 [平整度，网址去掉https](https://www.engineeringessentials.com/gdt/flatness/flatness.htm)

4. > There are a number of ways to measure the flatness of a surface. The most common method within the Flat Lapping sector is by using a Monochromatic Sodium light unit and an Optical Flat. This gives extremely precise measurements, more accurate than most CMM measurements, in an economical way.

摘自 [光学平整度测量，国外，此网站支持计算，还支持购买](https://www.kemet.co.uk/blog/lapping/how-to-measure-flatness-technical-article)

5. > Using a height gage to evaluate flatness   
   > Evaluating flatness using digital methods
   > With the advent of digital methods of evaluating GD&T using portable CMMs and advanced 3D metrology software

摘自 [平整度测量方法比较，国外网站](https://insights.faro.com/buildit-software/how-to-evaluate-flatness-in-gd-t)

6. 小提示：在用探头进行测量时，应该将零件放在一个面上，探头从下绕过孔中穿过去测量

7.千分尺

摘自 [国内千分尺，去掉http](https://www.wmt.com.cn/list/?16_1.html)



方法：   
 1.  3米直尺法  （测量路面，可能无法测量细小的平面）
 2.  连续平整度仪法（测量路面，无法测量细小平面）
 3.  水准仪法（测量一块区域的铅锤平面）
 4.  总结：  
     1. CMM自动化机床
     2. 牛顿环干涉测量
     3. 接触式平整度测量仪
     4. 激光反射，PSD测量
       






## 准备-学习  :

***************
------------------------
### 电机：暂时不好学，先挂起。  
------------------------------
### 电机驱动：  
1. 了解剩下的线路接口的作用
2. 弄明白目前出现的两种指令不执行情况：  
	1. 使用M1，M2混合位置控制时无法正常读取编码器值
	2. 使用后退动作后，无法正常使用位置动作（也有可能是读取编码器值出现问题，可能动作指令没问题，是瞬间就结束了）  
3. 尽可能重写库中的各种动作函数，完善动作  
4. 慢慢研究透官方手册
--------------------------------------
### 测敌传感器：
1. 了解工作状态
2. 研究透官方手册
3. 稳定读数
4. 探究是否有小数形式
------------------------------------
### 红外传感器：  
1. 研究官方手册
2. 稳定读数
3. 探究是否有小数形式
4. 处理角度过大造成的无信号
------------------------------------
### 边缘传感器：
1. 工作状态
2. 官方手册
3. 摆放角度
4. 在顶部也放入，用于探测翻倒
-----------------------------------
### 控制主板：
1. 了解小型主板的工作特点，检查是否可以更换更加微小的控制主板
2. 实验在setup中时间函数是否还有用
3. 了解芯片的优劣
-----------------------------
### 爪子：
1. 尽量向前
2. 爪子上不能有齿轮凸起
3. 长度，半径待测
4. 硬度有要求
--------------------------------------------
### 软件：
1. 采取新式框架，每次都进行一次所有数据采集，进行混合判断，得出当前状态，执行对应动作，在这个期间，不能妨碍上一个的动作执行
	1. 时刻明白：敌人在哪，我在哪，我正在干什么，我之前干了什么
	2. 有些地方可能需要计时，为了方便及时，可以自己创建计时函数
2. 可能需要进行上一个动作、上一个状态的记录和覆盖用于判断
3. 数据收集速度要快
4. 可能需要进行滤波运算
5. 可以试一试近似拟合，排除异常值
6. 模仿人的处理方法：结合大量数据，得出行动
7. 也许可以将每一个硬件包装成一个类，进行面对对象编程，但是可能会造成处理速度缓慢，不确定
8. 留下方便修改的接口
9. 命名规范：
	1. 固定值：全部大写，单词之间用‘_’隔开，单词遵循以下规则：
		1. 场地数值以VALUE开头
		2. 对错、开关、有无以SWITH开头，以YES/NO,ON/OFF等结尾
		3. 动作以ACTION为开头
		4. 状态以STATE开头
		5. 时间以TIME开头
		6. 硬件数值以HARDWARE开头，测敌传感器用ENEMY_SENSOR,红外传感器用INFRARED_SENSOR，边缘传感器用EDGE_SENSOR
	2. 全局变量：全部小写，单词之间用‘_’隔开，单词遵循以下规则：
		1. 对错、开关等以swith开头
		2. 状态以state开头
		3. 时间以time开头
		4. 数据以value开头
		5. 与动作有关的以action开头
	3. 函数名：第一个单词小写，剩余单词首字母全部大写，单词遵循以下规则：
		1. 测量函数以measure开头
		2. 动作函数以action开头
		3. 返回数值函数用value开头，如果是返回传感器值，在后面紧跟传感器代号

