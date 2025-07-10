## 前言

对于一门新的学科我们首先就要明确我们的学习流程。做到从一而终贯彻全文，要将知识串连起来。有一个好的学习思路有利于将碎片化的知识联系起来。本篇文章首先从[RFID](https://so.csdn.net/so/search?q=RFID&spm=1001.2101.3001.7020)整理了解入手，先学习了RFID的基础知识，然后学习了在整个RFID系统中进行通讯的流程，讲述了在整个通信中用到的一些技术，之后对RFID系统重要部件进行了一一介绍包括，天线、射频前端、电子标签、阅读器（读写器）。接下来我门就按照顺序开始学习。  

#### 目录

- [前言](https://blog.csdn.net/weixin_47323733/article/details/123950092#_0)
- [第 1 节 RFID技术概述](https://blog.csdn.net/weixin_47323733/article/details/123950092#_1_____RFID_3)
- - [1.1 RFID技术特点](https://blog.csdn.net/weixin_47323733/article/details/123950092#11_RFID_4)
    - [1.2 RFID系统组成](https://blog.csdn.net/weixin_47323733/article/details/123950092#12_RFID_16)
    - - [1.2.1 硬件组件](https://blog.csdn.net/weixin_47323733/article/details/123950092#121__19)
        - - [阅读器](https://blog.csdn.net/weixin_47323733/article/details/123950092#_20)
            - [电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#_40)
        - [1.2.2 软件组件](https://blog.csdn.net/weixin_47323733/article/details/123950092#122__50)
        - - [中间件](https://blog.csdn.net/weixin_47323733/article/details/123950092#_51)
            - [RFID应用系统软件](https://blog.csdn.net/weixin_47323733/article/details/123950092#RFID_59)
    - [1.3 RFID系统特征](https://blog.csdn.net/weixin_47323733/article/details/123950092#13_RFID_61)
    - [1.4 RFID技术现状和面临的问题](https://blog.csdn.net/weixin_47323733/article/details/123950092#14_RFID_62)
    - [1.5 RFID技术涉及到的物理知识](https://blog.csdn.net/weixin_47323733/article/details/123950092#15_RFID_63)
    - - [1.5.1 RFID用到的电磁场理论](https://blog.csdn.net/weixin_47323733/article/details/123950092#151_RFID_64)
        - [1.5.2 能量耦合和数据传输](https://blog.csdn.net/weixin_47323733/article/details/123950092#152__65)
        - [1.5.3 反向散射调制的能量传输](https://blog.csdn.net/weixin_47323733/article/details/123950092#153__66)
        - - [读写器到射频标签的能量传输](https://blog.csdn.net/weixin_47323733/article/details/123950092#_67)
            - [射频标签到读写器的能量传输](https://blog.csdn.net/weixin_47323733/article/details/123950092#_68)
- [第 2 节 RFID涉及技术的基础讲解](https://blog.csdn.net/weixin_47323733/article/details/123950092#_2__RFID_69)
- - [2.1 数字通信基础](https://blog.csdn.net/weixin_47323733/article/details/123950092#21__72)
    - - [2.1.1 通信系统模型](https://blog.csdn.net/weixin_47323733/article/details/123950092#211__73)
        - [2.1.2 数字通信系统模型](https://blog.csdn.net/weixin_47323733/article/details/123950092#212__84)
        - [2.1.3 RFID通信模型](https://blog.csdn.net/weixin_47323733/article/details/123950092#213_RFID_93)
    - [2.2 信号的编码与调制](https://blog.csdn.net/weixin_47323733/article/details/123950092#22__102)
    - - [2.2.1 信号与信道](https://blog.csdn.net/weixin_47323733/article/details/123950092#221__103)
        - - [信号](https://blog.csdn.net/weixin_47323733/article/details/123950092#_105)
            - [信道](https://blog.csdn.net/weixin_47323733/article/details/123950092#_128)
        - [2.2.2 编码](https://blog.csdn.net/weixin_47323733/article/details/123950092#222__144)
        - - [编码的定义](https://blog.csdn.net/weixin_47323733/article/details/123950092#_145)
            - [信源编码](https://blog.csdn.net/weixin_47323733/article/details/123950092#_147)
            - [信道编码](https://blog.csdn.net/weixin_47323733/article/details/123950092#_150)
            - [编码划分](https://blog.csdn.net/weixin_47323733/article/details/123950092#_154)
        - [2.2.3 RFID常用的编码方式](https://blog.csdn.net/weixin_47323733/article/details/123950092#223_RFID_160)
        - [2.2.4 调制](https://blog.csdn.net/weixin_47323733/article/details/123950092#224__192)
        - - [什么是调制](https://blog.csdn.net/weixin_47323733/article/details/123950092#_194)
            - [为什么要调制](https://blog.csdn.net/weixin_47323733/article/details/123950092#_196)
            - [调制方法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_197)
        - [2.2.5 RFID常用的调制方式](https://blog.csdn.net/weixin_47323733/article/details/123950092#225_RFID_198)
    - [2.3 RFID数据传输的完整性](https://blog.csdn.net/weixin_47323733/article/details/123950092#23_RFID_199)
    - - [2.3.1 RFID数据校验方法](https://blog.csdn.net/weixin_47323733/article/details/123950092#231_RFID_200)
        - - [差错与差错控制](https://blog.csdn.net/weixin_47323733/article/details/123950092#_202)
            - [奇偶校验法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_214)
            - [冗余校验法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_219)
        - [2.3.2 RFID系统中的碰撞](https://blog.csdn.net/weixin_47323733/article/details/123950092#232_RFID_229)
        - - [碰撞的概念](https://blog.csdn.net/weixin_47323733/article/details/123950092#_230)
            - [碰撞的类型](https://blog.csdn.net/weixin_47323733/article/details/123950092#_233)
            - [防碰撞机制](https://blog.csdn.net/weixin_47323733/article/details/123950092#_246)
        - [2.3.3 RFID标签防碰撞技术——标签控制法](https://blog.csdn.net/weixin_47323733/article/details/123950092#233_RFID_256)
        - - [纯ALOHA算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#ALOHA_260)
            - [时隙ALOHA算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#ALOHA_264)
            - [帧时隙ALOHA算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#ALOHA_268)
            - [动态帧时隙ALOHA算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#ALOHA_272)
        - [2.3.4 RFID标签防碰撞技术——读写器控制法](https://blog.csdn.net/weixin_47323733/article/details/123950092#234_RFID_275)
        - - [二进制搜索算法要素](https://blog.csdn.net/weixin_47323733/article/details/123950092#_277)
            - [树分叉算法基本思想](https://blog.csdn.net/weixin_47323733/article/details/123950092#_282)
            - [搜索过程展示](https://blog.csdn.net/weixin_47323733/article/details/123950092#_287)
        - [2.3.5 RFID读写器防碰撞算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#235_RFID_290)
        - - [产生碰撞原因——密集读写器环境](https://blog.csdn.net/weixin_47323733/article/details/123950092#_294)
            - [读写器防碰撞机制的选择](https://blog.csdn.net/weixin_47323733/article/details/123950092#_296)
            - [读写器防碰撞算法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_299)
    - [2.4 RFID数据安全](https://blog.csdn.net/weixin_47323733/article/details/123950092#24_RFID_306)
    - - [2.4.1 RFID系统安全漏洞](https://blog.csdn.net/weixin_47323733/article/details/123950092#241_RFID_307)
        - [2.4.2 RFID系统面临的攻击手段](https://blog.csdn.net/weixin_47323733/article/details/123950092#242_RFID_311)
        - [2.4.3 安全与隐私问题的解决方法](https://blog.csdn.net/weixin_47323733/article/details/123950092#243__327)
        - - [物理方法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_328)
            - [逻辑方法](https://blog.csdn.net/weixin_47323733/article/details/123950092#_335)
- [第 3 节 RFID系统之——线技术](https://blog.csdn.net/weixin_47323733/article/details/123950092#_3__RFID_346)
- - [3.1 天线概述](https://blog.csdn.net/weixin_47323733/article/details/123950092#31__347)
    - - [3.1.1 天性定义](https://blog.csdn.net/weixin_47323733/article/details/123950092#311__348)
        - [3.1.2 天线基本形式](https://blog.csdn.net/weixin_47323733/article/details/123950092#312__349)
        - - [线圈型天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_350)
            - [微带贴片天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_354)
            - [偶极子天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_358)
        - [3.1.3 3种形式线圈的特点](https://blog.csdn.net/weixin_47323733/article/details/123950092#313_3_361)
        - [3.1.4 天线类别](https://blog.csdn.net/weixin_47323733/article/details/123950092#314__366)
    - [3.2 低频和高频RFID天线技术](https://blog.csdn.net/weixin_47323733/article/details/123950092#32_RFID_382)
    - [3.3 微波RFID天线技术](https://blog.csdn.net/weixin_47323733/article/details/123950092#33_RFID_391)
    - - [3.3.1 天线技术（用到了哪种天线）](https://blog.csdn.net/weixin_47323733/article/details/123950092#331__395)
        - - [弯曲偶极子天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_396)
            - [微带天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_397)
            - [阵列天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_398)
            - [非频变天线](https://blog.csdn.net/weixin_47323733/article/details/123950092#_399)
        - [3.3.2 天线特点](https://blog.csdn.net/weixin_47323733/article/details/123950092#332__400)
        - [3.3.3 应用方式](https://blog.csdn.net/weixin_47323733/article/details/123950092#333__407)
    - [3.4 RFID天线的制造工艺](https://blog.csdn.net/weixin_47323733/article/details/123950092#34_RFID_413)
    - - [3.4.1 线圈绕制法](https://blog.csdn.net/weixin_47323733/article/details/123950092#341__415)
        - [3.4.2 蚀刻法](https://blog.csdn.net/weixin_47323733/article/details/123950092#342__422)
        - [3.4.3 印刷法](https://blog.csdn.net/weixin_47323733/article/details/123950092#343__429)
        - [3.4.4 工艺使用对象](https://blog.csdn.net/weixin_47323733/article/details/123950092#344__434)
- [第 4 章 RFID系统之——射频前端](https://blog.csdn.net/weixin_47323733/article/details/123950092#_4__RFID_438)
- - [4.1 射频前端概述](https://blog.csdn.net/weixin_47323733/article/details/123950092#41__442)
    - [4.2 信号收发技术——谐振概述](https://blog.csdn.net/weixin_47323733/article/details/123950092#42__444)
    - - [4.2.1 谐振简介](https://blog.csdn.net/weixin_47323733/article/details/123950092#421__445)
        - [4.2.2 谐振应用](https://blog.csdn.net/weixin_47323733/article/details/123950092#422__447)
        - [4.2.3 谐振电路](https://blog.csdn.net/weixin_47323733/article/details/123950092#423__451)
    - [4.3 谐振电路应用——阅读器天线电路](https://blog.csdn.net/weixin_47323733/article/details/123950092#43__455)
    - - [4.3.1 阅读器天线电路的选择](https://blog.csdn.net/weixin_47323733/article/details/123950092#431__456)
        - [4.3.2 串联谐振回路](https://blog.csdn.net/weixin_47323733/article/details/123950092#432__458)
        - - [电路组成](https://blog.csdn.net/weixin_47323733/article/details/123950092#_459)
            - [谐振条件](https://blog.csdn.net/weixin_47323733/article/details/123950092#_463)
            - [谐振特性](https://blog.csdn.net/weixin_47323733/article/details/123950092#_482)
            - [谐振曲线和通频带](https://blog.csdn.net/weixin_47323733/article/details/123950092#_497)
    - [4.4 谐振电路应用——应答器天线电路](https://blog.csdn.net/weixin_47323733/article/details/123950092#44__520)
    - - [4.4.1 应答器天线电路的选择](https://blog.csdn.net/weixin_47323733/article/details/123950092#441__521)
        - [4.4.2 并联谐振回路](https://blog.csdn.net/weixin_47323733/article/details/123950092#442__524)
        - - [电路组成](https://blog.csdn.net/weixin_47323733/article/details/123950092#_525)
            - [谐振条件](https://blog.csdn.net/weixin_47323733/article/details/123950092#_529)
            - [谐振特性](https://blog.csdn.net/weixin_47323733/article/details/123950092#_540)
            - [谐振曲线和通频带](https://blog.csdn.net/weixin_47323733/article/details/123950092#_541)
        - [4.4.3 串、并联等效替换](https://blog.csdn.net/weixin_47323733/article/details/123950092#443__542)
    - [4.5 阅读器和应答器之间的电感耦合](https://blog.csdn.net/weixin_47323733/article/details/123950092#45__543)
    - - [4.5.1 阅读器线圈的交变磁场](https://blog.csdn.net/weixin_47323733/article/details/123950092#451__544)
        - [4.5.2 应答器线圈的感应电压](https://blog.csdn.net/weixin_47323733/article/details/123950092#452__545)
        - [4.5.3 应答器谐振回路端电压](https://blog.csdn.net/weixin_47323733/article/details/123950092#453__546)
- [第 5 章 RFID系统之——电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#_5__RFID_547)
- - [5.1 一位电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#51__552)
    - - [5.1.1 基本介绍](https://blog.csdn.net/weixin_47323733/article/details/123950092#511__553)
        - [5.1.2 工作原理](https://blog.csdn.net/weixin_47323733/article/details/123950092#512__570)
    - [5.2 采用声表面波技术的标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#52__582)
    - - [5.2.1 什么是声表面波](https://blog.csdn.net/weixin_47323733/article/details/123950092#521__583)
        - [5.2.2 声表面波器件](https://blog.csdn.net/weixin_47323733/article/details/123950092#522__585)
        - [5.2.3 声表面波标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#523__589)
    - [5.3 含有芯片的电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#53__593)
    - [5.4 具有存储功能的电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#54__594)
    - [5.5 含有微处理器的电子标签](https://blog.csdn.net/weixin_47323733/article/details/123950092#55__595)
    - [5.6 电子标签的发展趋势](https://blog.csdn.net/weixin_47323733/article/details/123950092#56__596)
- [第 6 章 RFID系统之——读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#_6__RFID_597)
- - [6.1 读写器的组成](https://blog.csdn.net/weixin_47323733/article/details/123950092#61__601)
    - - [6.1.1 读写器的软件](https://blog.csdn.net/weixin_47323733/article/details/123950092#611__603)
        - [6.1.2 读写器的硬件](https://blog.csdn.net/weixin_47323733/article/details/123950092#612__604)
    - [6.1 读写器的设计](https://blog.csdn.net/weixin_47323733/article/details/123950092#61__630)
    - [6.2 低频读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#62__635)
    - - [6.2.1 U2270B芯片](https://blog.csdn.net/weixin_47323733/article/details/123950092#621_U2270B_636)
        - [6.2.2 考勤系统的读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#622__637)
        - [6.2.3 汽车防盗系统的读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#623__638)
    - [6.3 高频读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#63__639)
    - - [6.3.1 MF RC500 芯片](https://blog.csdn.net/weixin_47323733/article/details/123950092#631_MF_RC500__640)
        - [6.3.2 基于MF RC500芯片的读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#632_MF_RC500_641)
    - [6.4 微波读写器](https://blog.csdn.net/weixin_47323733/article/details/123950092#64__642)
    - [6.5 读写器的发展趋势](https://blog.csdn.net/weixin_47323733/article/details/123950092#65__643)

## 第 1 节 RFID技术概述

### 1.1 RFID技术特点

RFID技术是从20世纪90年代兴起的一项自动识别技术。它是通过磁场或者电磁场，利用无线射频方式进行非解接触双向通信以达到识别的目的并交换数据，可以识别高速运动物体并可同时识别多个目标。自动识别技术主要有：条形码识别、生物识别、射频识别（RFID）、智能卡识别（IC）、光学符号识别。  
RFID自动识别的优势极特点主要有：

- 快速扫描
- 体积小型化、形状多样化
- 抗污染能力和耐久性
- 可重复使用
- 穿透性和无屏障阅读
- 数据的记忆内容量大
- 安全性

经过多年的发展，13.65MHz以下的RFID技术已经相对成熟，目前发展最快的是中高频的RFID技术，尤其是在860~960MHz的远距离RFID技术发展的最快；2.45GHz和5.8GHz频段因为产品拥挤，容易受干扰，技术相对复杂，故相关研究和应用仍处于探索阶段。

### 1.2 RFID系统组成

典型的RFID系统主要由**阅读器、电子标签、RFID中间件、应用系统软件**4部分组成，一般把中间件和应用软件统称为应用系统。  简化来讲，RFID系统由 **应用系统(RFID中间件+应用系统软件) 、阅读器、电子标签3部组成**
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/31790f518900c5c0abd7cb7a4e5d0ced.png)


>注意：



#### 1.2.1 硬件组件

##### 阅读器

**阅读器主要负责与电子标签的双向通信，同时接受来自主机系统的控制指令。阅读器的频率决定了RFID系统工作的频段，其功率决定了射频识别的有效距离**。阅读器根据使用的结构和技术不同可以是读或读写装置，它是RFID系统信息控制和处理中心。**阅读器通常由射频接口、逻辑控制单元、天线，3部分组成。**  
![在这里插入图片描述|724](https://i-blog.csdnimg.cn/blog_migrate/df17f818f783d3c28f2bbf1f31629fdd.png)

- 射频模组  
    在射频接口中有两个分隔开的信号通道，分别用来往电子标签与阅读器两个方向的数据传输。传送往电子标签的数据通过发射器分支通道发射，来自于电子标签的数据通过接收分支通道接收。**射频模块具有以下主要任务：**  
    1.产生高频发射能量，激活电子标签并为其提供能量。  
    2.对发射信号进行调制，将数据传输给电子标签。  
    3.接收并调制来自电子标签的射频信号
- 逻辑控制单元  
    **逻辑控制单元也称为读写模块，其具有以下主要任务：**  
    1.与应系统软件进行通信，并执行从应用系统软件发来的指令  
    2.控制阅读器与电子标签的通信过程  
    3.信号的编码与解码  
    4.对阅读器和标签之间传输的数据进行加密和解密  
    5.执行防碰撞算法  
    6.对阅读器和标签的身份进行验证
- 天线  
    天线是一种能将接收到的电子电磁波转换为电流信号，或将电流信号转换成电磁波发射出去的装置。在RFID系统中，阅读器必须通过天线发射能量，形成电磁场，通过电磁场对电子标签进行识别，因此阅读器上的天线所形成的电磁场范围就是阅读器的可读区域。


>提示：某些先进的芯片比如ST25R3911B芯片完成了**射频接口与逻辑控制单元的二合一**，使设计者仅需要考虑光天线一个即可


##### 电子标签

电子标签（Electronic Tag）也称为智能标签（Smart Label），是指由IC芯片和无线通信天线组成的超微型的小标签，其内置的射频天线用于和阅读器进行通信。**系统工作时，阅读器发出查询（能量）信号，标签（无源）在收到查询（能量）信号后将其一部分整流为直流电源供电子标签内的电路工作；另一部分能量信号被电子标签内保存的数据信息调制后反射回阅读器。电子标签是射频识别系统真正的数据载体**  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a8ad73ae704f9e92433882a86252078f.png)  
电子标签内部各个模块功能描述

- 天线：用来接收阅读器送来的信号，并把要求的数据送回给阅读器
- 电压调节器：把阅读器送来的射频信号转换为直流电源，并加大电容存储能量，在经稳压电路以提供稳定的电源。
- 调节器：逻辑控制电路送出的数据经过调制电路调制后加载到天线送给阅读器
- 解调器：把载波去除以取出真正的调制信号。
- 逻辑控制单元：用来译码阅读器送来的信号，并依照其要求送回数据给阅读器。
- 存储单元：包括EEPROM与ROM，作为系统运行及存放识别数据的位置。

#### 1.2.2 软件组件

##### 中间件

中间件位于客户机、服务机的操作系统之上，管理计算机资源和网络通信。RFID中间件扮演着电子标签和应用程序之间的中介角色，从应用程序端使用中间提供的一组通用的应用程序接口，即能连接到RFID阅读器，读取电子标签数据。这样即使存储电子标签信息的数据库软件或后端应用程序增加或改由其他软件取代，或者RFID阅读器种类增加等情况发生时，应用端不需要修改也能处理。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4a4034c420aa065bb985007cacc2ddfb.png)  
RFID主要包括以下四个功能

- 阅读器协调控制
- 数据过滤预与处理
- 数据路由与集成
- 进程管理

##### 应用系统软件

RFID应用系统软件是针对不同行业的特定需求开发的应用软件，可以有效地控制阅读器对电子标签信息进行读写，并且对收集到的目标信息进行集中的统计与处理。RFID应用系统软件可以集成到现有的电子商务和电子政务平台中，**与ERP、CRM以及SCM等系统结合以提高各行业的生产效率**。

### 1.3 RFID系统特征

### 1.4 RFID技术现状和面临的问题

### 1.5 RFID技术涉及到的物理知识

#### 1.5.1 RFID用到的电磁场理论

#### 1.5.2 能量耦合和数据传输

#### 1.5.3 反向散射调制的能量传输

##### 读写器到射频标签的能量传输

##### 射频标签到读写器的能量传输

## 第 2 节 RFID涉及技术的基础讲解

章节导读：  
==由通信系统到数字通信系统的说明，来引入与之结构类似的RFID通信系统模型，来加深印象。对RFID通信系统中，编码和调制过程进行了讲解。并追加讲解了如何保证信息在无线信道中的传输完整性和传输安全性==。

### 2.1 数字通信基础

#### 2.1.1 通信系统模型

人类在生活、生产和社会活动中总是伴随着消（或信息）的传递，这种传递消息（或信息）的过程就叫做通信。通信系统是指完成通信这一过程的全部设备和传输媒介，包含三个主要的功能块：发送端、信道和接收端。如下图所示：  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5570036463d14ccc7fbe0ac41599259e.png)

在通信系统模型中，如下图所示：

- 信息源：简称信源，可分为模拟信源和数字信源。把各种消息转换成原始电信号，如话筒。
- 发送设备：产生适合于在信道中传输的信号。
- 信道：将来自发送设备的信号传送到接收端的物理媒质。分为有线信道和无线信道两大类。
- 接收设备：从受到减损的接收信号中正确恢复出原始电信号。
- 受信者（信宿）：把原始电信号还原成相应的信息，如扬声器  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/24a51785039d3e6d72fc586f97b6be00.png)

#### 2.1.2 数字通信系统模型

	思考：该模型是在前面的基础上深化而来的

数字通信系统是指利用数字信号来传递信息的通信系统。  
在数字通信系统模型中，如下图所示：

- 信源编码与解码目的：提高信息传输的有效性以及完成模/数转换；
- 信道编码与译码目的：增强抗干扰能力；
- 加密与解密目的：保证所传信息的安全；
- 数字调制与解调目的：形成适合在信道中传输的带通信号  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/9ceedfc219381eea9217744489f6a178.png)

#### 2.1.3 RFID通信模型

RFID系统常采用数字信号，其基本结构主要包含：读写器、天线和电子标签。  
与数字通信系统的模型相类似。在RFID系统内的数据传输有两个方面的内容：RFID读写器向电子标签方向的数据传输、RFID电子标签向读写器方向的数据传输  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0299522872a8f8a8a2c50a6e8b2e6d2d.png)

按RFID读写器到电子标签的数据传输方向，RFID系统的通信模型主要由

- 读写器（发送器）中的信号编码（信号处理）和调制器（载波电路）、
- 传输介质（射频前端、天线和自由空间）、
- 电子标签（接收器）中的解调器（载波回路）和信号译码（信号处理）组成

### 2.2 信号的编码与调制

#### 2.2.1 信号与信道

信号是消息的载体，在通信系统中消息以信号的形式从一点传送到另一点。信道是信号的传输媒介，信道的作用是把携有信息的信号从它的输入端传递到输出端（你可以把它想象成水管）。RFID中为无线信道

##### 信号

**1.模拟信号和数字信号**  
信号是数据的电表现形式，分为模拟信号和数字信号两种

- 模拟信号在时间上和数值上连续的信号。
- 数字信号在时间上和数值上不连续（即离散）的信号。通常用信号的两个稳态电平来表示二进制的“0”和“1”。

RFID系统传输数字信号。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/46835373644d79c545f3669cdb73bbc3.png)  
**2.时域和频域**

- 时域的自变量是时间，时域表达信号随时间的变化
- 频域的自变量是频率，频域表达信号随频率的变化

**3.信号工作方式**

- 时序系统：  
    在时序系统中，从电子标签到读写器的信息传输是在电子标签能量供应间歇进行的，读写器写与带脑子标签不同时发射。
- 全双工系统  
    电子标签与读写器之间可以在同一时刻互相传送信息
- 半双工系统  
    电子标签和读写器之间可以双向传送信息，但在同一时刻只能向一个方向传送信息

**4.通信握手**  
通信握手是指读写器与电子标签双方在通信开始、结束和通信过程中的基本沟通，其要解决通信双发的工作状态、数据同步、信息确认等问题。

##### 信道

信道有无线信道、有线信道。RFID的信道是具有各种传播特性的自由空间，所以RFID采用无线信道。

**1.信道带宽**  
信号所拥有的频率范围叫做信号的频带宽度，简称带宽。为信号在信道中能通过的最高频率减去最低频率。最低频和最高频都是由信道的物理特性决定的，当组成信道的电路制成了，信号的带宽就决定了。

**2.信道传输速率**  
信道传输速率就是数据在传输介质上的传输速率，数据传呼速率在数值上等于每秒钟传输数据代码的二进制比特数，数据传输速率的单位为比特/秒（b/s）。

**3.波特率和比特率**

- 波特率：在信息传输通道中，携带数据信息的断源叫码元，每秒钟通过信道传输的码元数称为码元传输速率，简称比特率。
- 比特率：每秒钟通过信道传输的信息量称为位传输速率，简称比特率，比特率是数据传输速率，表示单位时间内可传输二进制位的位数。
- 波特率和波特率的关系：假如一个码元用M个离散电平表示则有  
    比特率=波特率×1bM

**4.信道容量**

#### 2.2.2 编码

##### 编码的定义

把数字数据或模拟数据转换为数字信号都称为编码

##### 信源编码

模拟数据的数字化，又称信源编码，是对信源信息进行加工处理，模拟数据经过采样、量化和编码变换为数字信号。流程如下图  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/ecd2b5f764bf9fa7690272e33938cbf3.png)

##### 信道编码

数字数据的编码，即信道编码，是将数字数据编码成适合于在数字信道上传输的数字信号。信道编码的主要目的是向前纠错，以增强数字信号的抗干扰能力。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/9db7ec7625ae3346e94e0e770ade2dc7.png)

##### 编码划分

按数字编码方式，可以划分为以下几种：

- 单极性码：数字信号最简单的编码方法，通常只用一个电平来表示两个二进制
- 极性码：用负电平表示一个二进制值，正电平表示另一个二进制值
- 双极性码：无线路信号表示一种状态，正负电平交替表示另一种

#### 2.2.3 RFID常用的编码方式

**为什么要编码**

1. 在RFID系统中使用的电子标签常常是无源的，而无源标签需要在读写器的通信过程中获得自身的能量供应。
2. 可以根据码型的变化来判断是否发生误码或有电子标签冲突发生。**曼彻斯特编码、差动双向编码、单极性归零编码具有较强的编码检错能力**。
3. 在电子标签芯片中，一般不会有时钟电路，电子标签芯片一般需要在读写器发来的码流中提取时钟

**反向不归零编码**  
高电平表示二进制1，低电平表示二进制0  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8aaff55dc135364a8d929dec3bdf01d8.png)

**曼彻斯特编码**  
高到低为1，低到高为0  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/4791755261defa8db35f018c1b81f218.png)

**单极性归零编码**  
1发出一个正电流脉冲，0不动  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/78068c3ff1ee55eea3a3fcbff3680449.png)

**差动双向编码**  
半个周期任意边缘跳变表示0，1不变。此外在每个比特周期开始时，电平都要反相。因此，对于接收器来说，位节拍比较容易重建。