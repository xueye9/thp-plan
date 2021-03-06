#山西规划服务展示电网图

##需求明确
1. 共需要多少张专题图，例如需要轻重载、负载率两个着色；
2. 每张专题图的出图规范，例如：负载率着色专题图需求格式如下：
	1. 架空线、电缆按负载率着色
	2. 变电站、箱变、台边等组合设备按内部负载率最大的变压器着色；
	3. 不要求的设备显示为灰色；
	4. 轻载设备(小于20%)显示为绿色，重载设备(大于80%)显示为橙色，过载设备（大于100%）显示为红色，
	无负载率的设备显示为灰色、其他负载率的设备显示为蓝色
	5. 设备有分区的概念（类似广西的A、B、C、D、E、F六个分区）

##需求猜测
下面我针对2016年4月5日下午的会议，和山西规划项目的脑图文件猜测的需求，准确的
需求需要项目牵头人确定；

需要根据脑图"运行数据的应用(B/S)"进行推断。

脑图文件截图:
![BS展现脑图](./images/山西_BS展现.png)

##专题图分类
有四张专题图，分别在下文阐述可能的需求。

###配变的负载率着色专题图
1. 配变根据负载率着色;
2. 其他设备着为灰色;
3. 可以只对过载或轻载配变进行着色，也可以同时对过载和轻载的配变进行着色；

疑问：
1. 负载率如何获取，是计算好的负载率灌到服务的实时态中，还是需要服务进行二次计算，
如果需要服务器二次计算，那么计算公式和计算变准是怎样的？；
2. 轻载，过载是如何界定的；
3. 获取负载率的过程中使用对的属性是来自配变自身还是来自配变所属的线路的属性呢？
3. 着色规则是怎样的，是否为轻载绿色，重在红色等。
4. 分区的着色是否向广西的一样不区分分区，也就是A区和B区的超标配变着同样的颜色；

###以后的类似轻重载专题图

需求：

1. 设备依据所属线路rowbuffer字段[AREALEVEL] 属性分类；
2. 依据设备所属线路负载率着色；
3. 负载率在实时数据的第二个槽位；
4. 负载率单位 %,例如负载率80%实时数据中的数为80；
5. "高压负荷集中负荷"负载率来自rowbuffer字段[LOAD_RATIO]属性值，属性值规则实时数据规则一致；
6. 着色的类别可多选；
7. 未选中类别的设备默认着色；
8. 选中的类别但没有规定值的设备默认着色
9. 负载情况可多选，可控制着轻载、重在、过载的一个或多个；

着色规则:
1. 不区分类别
2. 负载率值分类和着色：

| 类别    | 负载率 |颜色|
|---|:---|---|
| 轻载    | 小于20%           |![蓝色](./images/b.png)|
| 重在    | 大于等于80% 且 小于100% |![橙色](./images/orange.png)|
| 过载    | 大于等于100%         |![红色](./images/red.png)|
|正常| 大于等于20% 且 小于80% |![绿色](./images/green.png)|

默认数据颜色: ![222,225,228](./images/light_gray.png)

异常数据颜色: ![0,0,0](./images/black.png)

####讨论结果

谭展辉、王金浩、薛冰冰、崔九东

平均负载率、高峰时段、最大的时段

复用广西的负载率

-------------------

###线路分析
线路主线和支线的重过载分析（用配变的负载率计算潮流，然后和导线的线经对比）；

对这个需求疑问较多，目前服务程序对线路是不区分主线路和分支线路概念的。

------------------

###低电压和高电压分析(脑图文件过电压写错了）
这个需求需要两张专题图，一张用于显示配变电压分析、一张用于显示低压用户的电压分析

####配变分析
1. 何为低电压;
2. 何为高电压;
3. 低电压配变着什么颜色；
4. 高电压配变着什么颜色;
5. 其他设备着什么颜色，例如架空线、电缆等；
6. 获取不到电压的设备着什么颜色；

####配变下的低压用户分布分析
??确认是配变下的低压用户分布分析，不是配变下的落火点分布分析？？

1. 什么是低电压
2. 什么是高电压
3. 着色规则；
4. 其他设备着什么颜色，例如架空线、电缆等；
5. 获取不到电压的设备着什么颜色；
6. 展示效果要求是什么样子？的是服务给出静态的不同颜色，还是客户端使用高亮或者闪烁效果进行显示；
7. 是对配变下的落火点进行着色还是对低压用户进行着色

