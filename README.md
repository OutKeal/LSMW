# LSMW高级用法

@[toc]
## 一. 概述

本文讲解用到的用例为LSMW->BATCH项目.

包含一般录屏功能和LSMW->IDOC->BAPI的功能介绍.



## 二. 录屏功能简介

### 1. 准备步骤

录屏:LSMW系统菜单 GOTO->Recording

注意点:

-   录屏过程中不允许报错.
-   不要存在无效操作

-   不允许使用F4等非直接屏幕操作

录屏完成后针对文件维护要导入的字段或者设置默认值.

![image-20230719094001974](https://img-blog.csdnimg.cn/img_convert/2aaa24e68da81ea6cc917b21c6d5ba12.png)

### 2. LSMW执行步骤及讲解

以BATCH->MD->MR21为例.

录屏步骤为:

#### 1.   Define Object Attributes(定义对象属性)

这里选择批处理记录MR21,定义名称.  	

<img src="https://img-blog.csdnimg.cn/img_convert/bd91f71bc1a49f61474f06da97731517.png" alt="image-20230719094315065" style="zoom: 33%;" />

#### 2.   Define Source Structures(定义数据源结构)

这里定义导入的数据源结构,即导入模板.
录屏结构一般只支持一层.

<img src="https://img-blog.csdnimg.cn/img_convert/75c3743c868330921e9f886d61d99924.png" alt="image-20230719094452577" style="zoom:33%;" />

#### 3.   Define Source Fields(定义数据源字段)

定义字段的名称,类型,长度,描述.详见BAPI调用高级用法.

<img src="https://img-blog.csdnimg.cn/img_convert/b35f6bc2b0f9688a8e861c2c78ebae08.png" alt="image-20230719094710105" style="zoom:33%;" />

#### 4.   Define Structure Relations(定义结构关系)

关联源结构和目标结构.若是1对1一般自动关联.多级结构需要手工关联,详见BAPI调用高级用法

![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/bc43f176efc14a0d96b6dfd6894a96f5.png#pic_center)

#### 5.   Define Field Mapping and Conversion Rules(定义字段映射和转换规则)

将源字段绑定到录屏字段,或者设置录屏字段的默认值.其它用法详见BAPI调用高级用法.

<img src="https://img-blog.csdnimg.cn/img_convert/b07c294a22914e7ecc0cfc38fe818c08.png" alt="image-20230719095240721" style="zoom:33%;" />

#### 6.   Define Fixed Values, Translations, User-Defined Routines(定义常量,转换,用户例程)

详见BAPI调用高级用法

#### 7.   Specify Files(指定上传文件)

多层导入需要创建多个文件.参考BAPI调用高级用法
一般选择TAB符作为分隔符.
选择文件按照个人习惯选择是否需要表头,这里选择不需要.

<img src="https://img-blog.csdnimg.cn/img_convert/bc6855f4e97fd06ca6dd56125ce1ead4.png" alt="image-20230719095436970" style="zoom:33%;" />

<img src="C:\Users\KEAL\AppData\Roaming\Typora\typora-user-images\image-20230719144041332.png" alt="image-20230719144041332" style="zoom:33%;" />

#### 8.   Assign Files(分配上传文件)

将上传文件分配到导入结构.若是1对1则自动分配.多对多详见BAP使用高级用法.

![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/8b2844893300454da5064b1e046fa3f3.png#pic_center)


#### 9.   Read Data(读取数据)

 将文件上传到服务器.
 测试时可以指定上传的行数.
 运行标题上的程序,该程序由LSMW自动生成及运行.
 读取完成会显示成功的行数,可检查下是否有异常.

 <img src="https://img-blog.csdnimg.cn/img_convert/44e220da102217c1f7e010dac4889012.png" alt="image-20230719100025747" style="zoom:33%;" />


#### 10.   Display Read Data(预览读取的数据)

可选择预览的行数.

<img src="https://img-blog.csdnimg.cn/img_convert/6c24d84948f9790b7d964dfd9f593e81.png" alt="image-20230719100327960" style="zoom:33%;" />

<img src="https://img-blog.csdnimg.cn/img_convert/d2e466afff9812834f10bff8df6e0125.png" alt="image-20230719100340994" style="zoom:33%;" />

#### 11.   Convert Data(转换数据)

将读取到的数据转换为录屏结构的数据.
可选则需要转换的行数.
完成后显示成功的行数,可检查下是否有异常.
标题程序由MAPPING保存时自动生成,通过该程序转换数据

<img src="https://img-blog.csdnimg.cn/img_convert/ca984afda1a1ef59497f1d35d5f9ad2d.png" alt="image-20230719100643694" style="zoom:33%;" />

#### 12.   Display Converted Data(预览转换的数据)

可选择预览的行数.

<img src="https://img-blog.csdnimg.cn/img_convert/9cf171172924fef7951617cfd8384b6d.png" alt="image-20230719101225470" style="zoom:33%;" />

<img src="C:\Users\KEAL\AppData\Roaming\Typora\typora-user-images\image-20230719140620004.png" alt="image-20230719140620004" style="zoom:33%;" />

#### 13.   Create Batch Input Session(创建批处理会话)

创建批处理会话到SM35

勾选Keep Batch Input Folder(s)后则执行脚本后不删除成功项.

<img src="https://img-blog.csdnimg.cn/img_convert/9229deee9e05224018e5bbb0caa2dbfb.png" alt="image-20230719101347212" style="zoom:33%;" />

#### 14.   Run Batch Input Session(执行批处理会话)

跳转事务码SM35执行批处理会话

一般用不可见模式执行,执行失败可以用前台模式调试查找原因.

<img src="https://img-blog.csdnimg.cn/img_convert/32839f887451ab079f3f9f9cd9ef18d5.png" alt="image-20230719101608612" style="zoom:33%;" />

<img src="https://img-blog.csdnimg.cn/img_convert/278d2be0a3c60f8424acbc77a7fe3bad.png" alt="image-20230719101644348" style="zoom:33%;" />

### 3. 常见错误

-   数值字段的小数不能超出系统内长度,例如数量一般三位,金额/单价一般两位.

-   数值字段不能包含千分位.
-   传入文件EXCEL中处理时,单元格内不能有换行符/TAB符.

### 4. 录屏处理的缺陷	

-   对于单据对象,一般只能按行去调整,效率较低.

-   某些新事务支持较差,例如MIGO,ME21N等.

## 三. BAPI调用高级用法

本方法可调用很多标准BAPI函数.本质上是调用标准BAPI所创建的IDOC接口服务.

也可以自定义一个IDOC接口服务.步骤大致如下:

1.   功能函数(SE37),需符合BAPI规范,例如必须包含参考为BAPIRET2的表结构.

2.   为其定义业务对象(SWO1),参考BAPI函数创建API方法,发布对象
3.   通过BDBG自动生成IDOC类型,段类型,处理函数
4.   检查生成的函数,一般需要微调该函数,例如绑定业务对象和IDOC对象到关系浏览器.

BATCH项目中包含了MM/SD模块常用的BAPI调用方式.

本讲解将使用BATCH->ME->ME_PO_CREATE为例,讲解创建PO的方法.

需要一定的ABAP开发理解.

### 1. 准备步骤

项目层维护IDOC全局参数.菜单Settings->Inbound IDoc Processing.

1.   WE21维护文件端口和tRFC端口.
2.   WE20维护逻辑系统的合作伙伴编号.
3.   绑定端口和合作伙伴到LSMW项目.

新导入/创建的IDOC项目都需要维护以上步骤.

<img src="https://img-blog.csdnimg.cn/img_convert/4fbd2d6d3182329492976ac2133aee68.png" alt="image-20230719103653714" style="zoom:33%;" />

### 2. LSMW BAPI调用高级用法详细述

#### 1. Define Object Attributes(定义对象属性)

定义对象的名称,使用业务对象方法(BAPI).指定其业务对象(常见业务对象见附表).
这里使用采购订单对象BUS2012的创建方法,调用IDOC消息类型PORDCR1,基本类型PORDCR103.
保存时会自动向全局配置的合作伙伴参数文件创建入站配置,可以WE20查看.

<img src="https://img-blog.csdnimg.cn/img_convert/7a9b66618521bbaa00bc92fc22fd7a2a.png" alt="image-20230719104813738" style="zoom:33%;" />

#### 2. Define Source Structures(定义数据源结构)

一般单据对象包含抬头/项目/计划行三层,业务上可理解为两层抬头项目,这里定义两个数据源.

注意项目要是抬头的子级.

<img src="https://img-blog.csdnimg.cn/img_convert/5e3e4654d699a4d28fe13bfc46e64a41.png" alt="image-20230719110603388" style="zoom:33%;" />

#### 3. Define Source Fields(定义数据源字段)

定义抬头,项目结构的字段名称/类型/长度/描述

一般标准元素字段名称,可以自动带出描述.

建议字段类型都用C,长度跟系统内部字段保持一致.

抬头/项目必须至少有一个同名字段.系统通过该字段自动将项目进行分组.

后续为每一个抬头字段创建一个IDOC分别执行.

<img src="https://img-blog.csdnimg.cn/img_convert/443774f1b3044fb096e367abf011f9f6.png" alt="image-20230719110649833" style="zoom:33%;" />

#### 4. Define Structure Relations(定义结构映射关系)

定义结构关系,内部结构为IDOC消息类型的结构.基本与BAPI结构一致.

该类型指向BAPI_PO_CREATE1功能函数.

将数据源结构指向需要传入的结构.

<img src="https://img-blog.csdnimg.cn/img_convert/629ebfb20a8019f89ab0e06d468b1dd0.png" alt="image-20230719111204282" style="zoom:33%;" />

#### 5. Define Field Mapping and Conversion Rules(定义字段映射和转换规则)

指定字段转换规则,规则有多种,最常见的为绑定源字段和指定默认值.

![image-20230719130208664](https://img-blog.csdnimg.cn/img_convert/d171b5ab61935c98ca7fa40e53d02a31.png)

除此之外针对每个字段,点击RULE后,支持多种规则.

<img src="https://img-blog.csdnimg.cn/img_convert/9923d80987dee132caf785bade97c482.png" alt="image-20230719111809057" style="zoom:33%;" />

-   Inital 初始化,清空规则
-   Constant 指定常量
-   Transfer 绑定源字段并转换,可使用自定义转换规则或者内置的数据元素转换规则
-   Prefix 增加前缀
-   Suffix 增加后缀
-   Concatenation 指定多个源字段后,连接到一起
-   Transfer Left-Aligned 转换源字段,左对齐
-   ABAP Code 自定义代码处理
-   User-Defined Routine 调用6中定义的用户例程form
-   X Field 一般判断为去掉X的结构字段有值,则赋值X,否则空
-   Move With Leading Zeros 绑定源字段并补前导0

最终所有的RULE都将生成ABAP代码,可以点击右侧代码行显示其内容,自己直接写代码结果相同.

图中为例,选择VENDOR字段绑定数据源的抬头供应商字段,再选中RULE中的补前导0.

<img src="https://img-blog.csdnimg.cn/img_convert/81e60128c6f4da9ffd317a5f22bff13a.png" alt="image-20230719130305461" style="zoom:33%;" />

保存后,系统将自动生成一个转换程序,在步骤11转换数据标题可以看到.SE38可以打开查看.

#### 6. Define Fixed Values, Translations, User-Defined Routines(定义常量,转换规则,用户例程)

-    Fixed Values(定义常量)

     可定义PROJECT级别的常量,例如这里定义PO_PRICE_TYPE,值为ZPB0,在MAPPING中PO条件类型指定该常量.

-   Translations(转换规则)

    可定义转换规则,例如当导入为米时,转换为M.一般做按单值转换或者范围值转换.

-    User-Defined Routines

     当复杂条件时,可以定义代码例程.例如这里定义REPLACE_COMMA,去除数量/金额中的逗号.

#### 7. Specify Files(指定上传文件)

多层导入需要创建多个文件.这里为抬头/项目各创建一个文件路径.

<img src="https://img-blog.csdnimg.cn/img_convert/9b6e9e5b0dec9c1ae68bc1ba6c2a65f1.png" alt="image-20230719132022660" style="zoom:33%;" />一般选择TAB符作为分隔符.
选择文件按照个人习惯选择是否需要表头,这里选择不需要.

<img src="https://img-blog.csdnimg.cn/img_convert/a3aa8d808e0cf41ee1f6454827a0de85.png" alt="image-20230719132037912" style="zoom:33%;" />

#### 8. Assign Files(分配上传文件到数据源)

这里有多个数据源结构和上传文件,所以要手工指定对应关系.

<img src="https://img-blog.csdnimg.cn/img_convert/b8f87795b2c7b83c1fd997b3bcf887b1.png" alt="image-20230719132128606" style="zoom:33%;" />

#### 9. Read Data(读取数据)

多数据源READ时,也可以指定行数,不过此时仅仅判断抬头行数.

读取后显示读到的数据:

-   ​	文件中抬头行的总行数
-   ​	文件项目行的总函数	
-   ​	抬头行的读取行数
-   ​	与抬头行匹配的项目行数

例如选择测试数据为抬头两行,对应的项目分别为2/3行

只上传1行时显示:

<img src="https://img-blog.csdnimg.cn/img_convert/fbf16228d5f2b496737d3f9852e592cd.png" alt="image-20230719133048426" style="zoom:33%;" />

全部读取时显示:

![image-20230719132946004](https://img-blog.csdnimg.cn/img_convert/8f4a519d5f4da93f649da73262b343a5.png)

#### 10. Display Read Data(预览读取数据)

支持预览指定行数的数据.

<img src="https://img-blog.csdnimg.cn/img_convert/06a05f38ca20caa2206301ef76f79a21.png" alt="image-20230719133223226" style="zoom:33%;" />

<img src="https://img-blog.csdnimg.cn/img_convert/dad175b36eb8691380d8edb86aff1ef4.png" alt="image-20230719133238206" style="zoom:33%;" />

<img src="https://img-blog.csdnimg.cn/img_convert/9a31a7903097b0df0217e0906d0b6cc2.png" alt="image-20230719133254035" style="zoom:33%;" />

#### 11. Convert Data(转换数据)

调用MAPPING维护的逻辑将上一步的数据转换为BAPI规则.

支持按抬头行数指定转换数据.

可以SE38查看抬头标题生成的自动转换程序.

此时显示的行数无法检查,因为会补充一些IDOC端的相应信息.

<img src="https://img-blog.csdnimg.cn/img_convert/254da834940258a2baebcd99d8d4511e.png" alt="image-20230719133512161" style="zoom:33%;" />

#### 12. Display Converted Data(预览转换后的数据)

可以考到除了MAPPING里维护的规则,多了EDI_DC40抬头段,其它段也多了段编号等信息.

其实这部分也在MAPPING中由系统自动生成,可以通过选择MAPPING中的LAYOUT显示技术部分查看此部分.

<img src="https://img-blog.csdnimg.cn/img_convert/0fc4f8b3388979e49e2b60b2e3f610d5.png" alt="image-20230719133545553" style="zoom:33%;" />

<img src="C:\Users\KEAL\AppData\Roaming\Typora\typora-user-images\image-20230719133729014.png" alt="image-20230719133729014" style="zoom:33%;" />

#### 13. Start IDoc Creation(开始创建IDOC)

根据转换好的数据生成IDOC.

创建完成后可以通过WE02查看生成的IDOC.

<img src="https://img-blog.csdnimg.cn/img_convert/8bdd1ca03a2ebfa840a9c453f10d6e1c.png" alt="image-20230719133921911" style="zoom:33%;" />

#### 14. Start IDoc Processing(开始执行IDOC)

开始处理IDOC,调用程序RBDAPP01程序,筛选参数为转换时间后本类型的IDOC,且状态为64未执行.
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/2e8e0c4ccf7944308176878c1fabec29.png#pic_center)

若量很大,可以选择并行处理多线程处理.例如下图选择代表30个并行线程.也可以挂后台作业多线程处理.

<img src="https://img-blog.csdnimg.cn/img_convert/731d81ce609032982ebfe7deb32b82cd.png" alt="image-20230719134216544" style="zoom:33%;" />

<img src="https://img-blog.csdnimg.cn/img_convert/df15f31ca5eb7300c82240db8b4a3427.png" alt="image-20230719134523536" style="zoom:33%;" />

#### 15. Create IDoc Overview(创建IDOC的概览)

调用WE02查看上一步过账的IDOC.
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/aa8eaa0e16f34ce4953c5d13c0f2c0f2.png#pic_center)

#### 16. Start IDoc Follow-Up(IDOC后续查看)

异常IDOC的后续处理.

入站IDOC的常用状态简述:

-   56:合作伙伴确定错误,无效IDOC

-   64:待处理IDOC
-   51:错误的IDOC
-   53:成功处理的IDOC
-   69:手工修改后的IDOC
-   70:手工修改后生成的IDOC备份,一般不用处理
-   68:作废的IDOC

可以用过程序RC1_IDOC_SET_STATUS手工转换IDOC的各种状态.

例如错误的接口数据,一般将该IDOC状态置为68.		

<img src="C:\Users\KEAL\AppData\Roaming\Typora\typora-user-images\image-20230719134652346.png" alt="image-20230719134652346" style="zoom:33%;" />

### 3. 常见业务对象清单

-   物料 BUS1001
-   零售物料 BUS1001001
-   物料BOM BUS1080
-   采购申请 BUS2009
-   采购订单 BUS2012
-   内向交货 BUS2015
-   物料凭证 BUS2017
-   销售订单 BUS2032/VBAK
-   外项交货 LIKP
-   销售发票 VBRK
-   工作中心 BUS0011
-   生产订单 BUS2005
-   生产订单确认(报工) BUS2116
-   总账科目  BUS3006
-   成本中心 BUS0012
-   成本中心组 BUS1112
-   利润中心 BUS0015
-   利润中心组 BUS1116
-   会计凭证 BKPF

