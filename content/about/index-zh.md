# 边俊宇

+86 15830955187｜junyu.bian@gmail.com

# 个人总结

在云原生软件开发领域具有三年工作经验；在英特尔中国参与Smart Edge、Intel Edge Platform等边缘计算平台的开发，主要开发语言为Go，辅助结合Python、Shell等工具；如，在云端设计并搭建完整、稳定的可观测性平台工具，使整体研发效率大幅提升，并应公司内外要求在3次内部论坛、2次外部论坛进行宣讲；

做事严谨认真、积极主动，具有创新精神，以目标为导向，能够在具有压力以及不确定环境中工作，具有优秀的团队影响力及责任心，且曾获评英特尔年度最佳员工。

**云原生开发:** 熟练使用k8s、docker、containerd等工具，拥有包括集群管理、云配置中心、资源调度、链路监控、故障诊断、等模块架构设计及开发经验，主要开发语言为Go，并结合Python、shell 完成无人值守管控系统的构建。

**后端开发:** 有丰富的企业中台后端开发经验，主要开发语言为Java，并结合Spring、SpringMVC以及Mybatis。有前后端完整系统独立搭建经验，主要使用Python作为开发语言，结合Django框架进行开发。

**客户端开发:** 熟悉增强现实（AR）、虚拟现实（VR）开发，主要开发语言为C#。通过Unity3D游戏开发引擎，完成PC端以及移动端APP开发，包括游戏开发、混合现实应用软件开发，使用Java在Android Studio平台上完成安卓APP开发，熟悉Android源码、模拟器源码开发经验，同时具有单元测试用例、安卓UI自动化用例编写经验。

**机器学习:** 有机器学习开发经验，使用TensorFlow及Pytorch框架，利用Python语言进行支持向量机等项目实践。

**其他技能:** 熟练C++开发，熟悉相关底层实现；有使用Python结合Django框架进行服务端开发经验；熟练使用Git等版本控制软件，熟练使用Postman、Mocks等后端调试软件；熟练使用LaTex、Markdown等技术文档编写工具，具有优秀的写作能力。

# 工作经历及项目经验

## 英特尔中国研究院｜云计算软件开发工程师｜2021.03 - 今
- 设计并实现了Edge Platform的可观察性系统，主要应用了Grafana、fluent-bit等工具；使用户可以通过统一的UI界面（依靠Grafana Loki以及Mimir实现）来访问并查询系统从provisioning之前到启动之后的log及metric，提升了100%的系统可见性。
- Intel Smart Edge Open DEK以及PWEK的关键贡献者，比如，在kubernetes集群上利用Calico插件为Smart Edge 平台从零开发了分离网络的功能，该功能上线后减少了50%来自用户的需求单，使得平台网络利用效率、访问安全性大大提升。
- 使用virsh等工具，以虚拟化方式在OpenNESS边缘计算平台上使能了OpenVINO智慧城市负载，并借助Grafana页面向用户展示处理结果，以达到用户快速搭建demo的目的，相较于在物理机器上搭建，节省50%以上时间。
- 在Smart Edge边缘计算平台上使能私有网络体验套件（Private Wireless Experience Kit All in One），打通gNodeB\phy\DU\CU层级单元之间通信，并用Python参与设计实现CPU manager模块，使得CPU利用率提升50%。
- 使用Go语言在Intel Edge Platform上设计status handler, maestro handler并通过gRPC以及RESTful API两种方式进行实现，使provisioning controller的运行效率提升100%。
- 同时在团队中担任scrum master，包括：主持与印度合作伙伴每周3次的scrum meeting，通过Jira Board来追踪进度，并记录Meeting Minutes；主持每两周一次的队内innovation meeting，搜寻创新相关会议信息，并整理、准备内容与团队共享，主持会议期间，团队创新产出同比增长100%。

## 腾讯｜客户端开发实习生｜2020.09 - 2021.03
- 工作于Daas模拟器平台搭建项目，主要负责基于AOSP来构建适用于腾讯内部云原生平台的安卓镜像，从而保证手机QQ和微视两款软件可以以虚拟化形式运行，k8s、docker等容器管理及虚拟化技术进行模拟器配置。
- 在k8s的集群负载中使能了音频流在应用与虚拟系统之间的流通，由于微视以及QQ通话极大程度依赖于音频流，使能该能力后，解决了AOSP在适配时的关键问题。
- 预研Android以及Android Emu源码，针对模拟器平台需求修改源码接口，编译定制化镜像。 如，新增10+调用API、修改10+调用逻辑，以更加适配腾讯内部云原生平台。
- 使用Mockito、Junit等工具编写单元测试用例以及自动化用例。

## 阿里巴巴集团｜软件开发实习生｜2020.06 - 2020.09
- 参与面向企业低代码平台搭建，主要工作在后端代码开发，通过Git与团队协作，并完成后端接口设计、接口测试、前后端协同开发、跨部门平台联调等， 使用Java进行开发，配合使用Spring、SpringMVC、Mybatis开发框架以及阿里内部中间件，负责工具类编写以及调研性工作，如完成DSL输入参动态更新工具编写、Groovy预编译效率调研等。
- 从定义API到DAO层实现最终落实数据库查询语句，使用Java编写了20余条完整API，并通过优化数据库查询语句逻辑使最终查询效率提高了20%。
- 独立设计并实现了平台的Groovy代码预编译工作，使其以tar ball形式被利用，从而减少了10%的项目构建时间。

## 西门子中国研究院｜混合现实开发实习生｜2019.04 - 2019.08
- 独立完成里混合现实应用开发，在跨平台设备上实现了虚拟现实与增强现实的结合，如，安卓设备、HTC VIVE、诺亦腾Hi5手套以及Windows主机。
- 独立使用C#和Java两种编程语言在Unity游戏引擎以及Android Studio平台上开发了可交互增强现实(AR)软件，实现了通过Windows机器对于安卓虚拟UR5、UR10机械臂的实时关节级控制。
- 创新性地将HTC VIVE虚拟现实(VR)设备、诺亦腾Hi5 VR手套和安卓AR系统整合在一起而建立了混合现实连接，实现了使用物理虚拟现实设备，比如诺亦腾手套，来控制AR物品。

## 基于主动攻击信号消除策略的超声波防御方法｜软件开发｜2017.08 - 2019.08
2019年完成基于主动攻击信号消除策略的超声波防御方法，论文发表于通信领域**顶级会议MobiCom2019**并获得**国家级专利**，本项目研究了一种应对对于声控系统的超声波攻击的防御机制，能够检测出攻击信号，并在理解正常语音指令的同时，对攻击进行滤除。
- 系统模型设计开发：对攻击与防御系统进行模型设计，并在树莓派上使用Python语言对完整的超声波攻击与防御算法系统进行开发，以证明防御系统的便携性。
- 移动应用开发：在安卓平台上，独立使用JAVA利用Android Studio软件，结合亚马逊AWS、讯飞语音技术平台TTS软件包，对主要防御算法进行实践验证。
- 图像与声音处理：利用Matlab软件完成基带语音信号在超声波信号上的调制与解调，并对防御算法进行建议模拟仿真，对处理后的语音信号进行滑窗处理，并生成图像用以验证信号处理结果。
- 电路搭建：对超声波发生电路进行了设计，并使用C语言控制单片机对主要电路进行了焊接与制作。
- 论文撰写：对最终发表于Mobicom2019的论文以及国家专利声明书进行撰写，包括背景知识整理总结、相关示意图片绘制、算法内容说明等职责。

## 基于超声波的无线广播通信方法｜软件开发｜2017.10 - 2018.11
2018年完成基于超声波的无线广播通信方法，论文发表于WCSP2018并获得**国家级专利**，本项目提供了一种基于超声波的无线通讯方式，包括如下特点：采用基于超声波方向性的SDMA（space division multiple access）方案；利用幅度调制进行语音信号传输，以及频率调制进行数字信号传输，利用支持向量机对调制方法进行识别。
- 仿真算法开发：利用Matlab平台，对频移键控FSK算法进行模拟仿真，并计算信号传输速率，同时负责信号的调制与与处理等工作。
- 文档撰写：对最终发表于WCSP2018的论文以及国家专利声明书进行撰写，包括原理解释、实验结果整理验证、创新点阐述与论证等职责。
  
# 教育背景

2019.08 - 2021.05｜硕士｜纽约大学｜计算机工程｜Top10%

2015.08 - 2019.08｜工学学士｜上海交通大学｜电子计算机工程｜**上海交通大学优秀毕业生**

2016.08 - 2019.06｜文学学士｜上海交通大学｜动画｜双学位

# 相关论文与会议

Junyu Bian, Simon Li, “Intelligent Traffic Searching on Intel Edge Native Software Platform Enabled 5G”, 2023 China KubeCon, Demo and Presentation.

Junyu Bian, “Smart Edge Accelerating 5G Deployment”, 2022 Intel DTTC, Demo and Presentation.

Junyu Bian, Qianli Zhao, “Build 5G Private Network Base On SEO”, 2022 SDNLab, Presentation.

Junyu Bian, Jingyi Zhu, “PWEK AIO Speeding 5G Edge”, 2021 China KubeCon, Demo and Presentation.

<!-- ## 关于我
Hi，我是赵化冰，服务网格技术布道者及实践者，[腾讯云](https://cloud.tencent.com/product/tcm)工程师，曾担任[中兴通讯](https://www.zte.com.cn/)技术专家，Linux 基金会开源项目 [ONAP](https://www.onap.org/) 项目 leader，甲骨文中间件高级顾问等。我创建了服务网格开源项目 [Aeraki Mesh](https://aeraki.net)（CNCF Sandbox 项目），可以在 Istio 中管理 Dubbo、Thrift、Redis 以及任意私有协议的流量。

工作联系： zhaohuabing@gmail.com

## 出版物
| 标题       |类型        |出版社   |链接        |
| ----------- |----------- |----------- |----------- |
|[深入理解 Istio — 云原生服务网格进阶实战](https://www.zhaohuabing.com/post/2021-08-26-istio-handbook/)|实体书籍|电子工业出版社|[购买链接](https://item.jd.com/13200745.html)|
|[Distributed Tracing with Jaeger, Kubernetes, and Istio](https://www.zhaohuabing.com/post/2021-09-08-distributed-tracing-with-jaeger-kubernetes-and-istio/)|在线教程|[曼宁出版社（美）](https://www.manning.com/)|[30% 折扣](https://www.manning.com/liveprojectseries/distributed-tracing-ser)|
|[云原生数据中心网络](https://zhaohuabing.com/post/2021-08-27-cloud-native-data-center)|翻译书籍|中国电力出版社|[购买链接](https://item.jd.com/12929975.html)|
|[Istio 运维实战](https://istio-operation-bible.aeraki.net)|电子书籍||[在线阅读](https://istio-operation-bible.aeraki.net)|


## 演讲分享 (部分)
|年份          |城市        |会议         | 分享主题    |讲稿         |视频       |
| ----------- |----------- |----------- |----------- |----------- |----------- |
|2022|线上|[IstioCon](https://events.istio.io/istiocon-2022)|[Istio + Aeraki 在腾讯音乐的服务网格落地](https://events.istio.io/istiocon-2022/sessions/tencent-music-aeraki/)|[下载](/slides/tencent-music-service-mesh-practice-with-istio-and-aeraki.pdf)|[观看](https://www.youtube.com/watch?v=6t_yPsq4Pi4)|
|2022|线上|[A2M](https://a2m.msup.com.cn/course?aid=2699&cid=15382)|[全栈服务网格 - Aeraki Mesh 助你在 Istio 服务网格中管理任何七层流量](https://a2m.msup.com.cn/course?aid=2699&cid=15382)|[下载](/slides/full-stack-service-mesh-a2m-20220422.pdf)||
|2022|线上|[云原生正发声](https://cloud.tencent.com/developer/salon/live-1403)| [Areaki Mesh 在 2022 冬奥会视频直播应用中的服务网格实践](https://mp.weixin.qq.com/s/zp9q99mGyH2VD9Dij2owWg) | [下载](http://localhost:1313/img/2022-03-30-aeraki-mesh-winter-olympics-practice/slides.pdf)|[观看](https://youtu.be/uXxatQTKzW8)|
|2021|线上|[IstioCon](https://events.istio.io/istiocon-2021/)| [How to manage any layer-7 traffic in an Istio service mesh?](https://events.istio.io/istiocon-2021/sessions/how-to-manage-any-layer-7-traffic-in-an-istio-service-mesh/) | [下载](/slides/how-to-manage-any-layer-7-traffic-in-istio.pdf)|[观看](https://www.youtube.com/watch?v=sBS4utF68d8)|
|2020|线上|[CNBPS](https://www.cnbpa.org/)|[Istio 流量管理原理与协议扩展](https://cloud.tencent.com/developer/article/1723804)|[下载](/slides/cnbps2020-istio-aeraki.pdf)|[观看](https://www.youtube.com/watch?v=lB5d4qbZqzU)|
|2019|成都|[Service Mesher Meetup](https://cloudnative.to/blog/service-mesh-meetup-chengdu-20191028/)|[Service Mesh是下一代SDN吗？](https://cloudnative.to/blog/service-mesh-meetup-chengdu-20191028/)|[下载](/slides/what-can-service-mesh-learn-from-sdn-servicemesher-meetup-20191026.pdf)|[观看](https://youtu.be/nGkxp-2OsKg)|
|2019|西安|ONAP Workshop|基于 5G 网络管理系统的服务网格实践|[下载](/slides/service-mesh-practice-with-5g-management-system-lfn.pdf)|
|2018|南京|[GNTC](https://www.bagevent.com/event/1624048?aId=)|[ONAP 服务网格实践](https://www.sdnlab.com/22596.html)|
|2017|圣克拉拉|[NAP Developer Forum](https://wiki.onap.org/display/DW/ONAP+Beijing+Release+Developer+Forum%2C+Dec.+11-13%2C+2017%2C+Santa+Clara%2C+CA+US)|[MSB to Support Carrier Grade ONAP Microservice Architecture with Service Mesh](https://onapbeijing2017.sched.com/event/D5q2)|[下载](https://wiki.onap.org/display/DW/MSB+Service+Mesh+Planning?preview=%2F20873876%2F20873874%2FMSB+to+Support+Carrier+Grade+ONAP+Microservice+Architecture+with+Service+Mesh.pdf)|
|2017|圣克拉拉|[ONS](https://wiki.onap.org/display/DW/ONAP@ONS2017)|Microservice Powered Orchestration|[下载](https://wiki.onap.org/display/DW/ONAP@ONS2017?preview=%2F3245268%2F3245309%2FMicroservice+Powered+Orchestration+Architecture.pdf)|
|2017|新泽西|[ONAP Developer Event](https://wiki.onap.org/display/DW/ONAP+Project+Developer+Event%3A+May+2+-+5%2C+2017%2C+Middletown%2C+NJ%2C+USA)|MSB Technical Deep Dive and ONAP Use Cases|[下载](https://www.slideshare.net/HuabingZhao/msb-depp-dive/)|
|2017|巴黎|[ONAP Developer Event](https://wiki.onap.org/display/DW/ONAP+Developer+Event+September+25-28%2C+2017%2C+Paris-Saclay%2C+France)|[Microservice Bus Tutorial](https://wiki.onap.org/display/DW/September+26-28+Topics#September2628Topics-M2)|[下载](https://www.slideshare.net/HuabingZhao/microservice-bus-tutorial)|

## 开源项目
|项目         |角色        |  网站   | GitHub     |
| ----------- |----------- |----------- |----------- |
| Aeraki Mesh | 创建者    | https://aeraki.net  | http://github.com/aeraki-mesh |
| Istio       | Contributor| https://istio.io    | https://github.com/istio/istio|
| Envoy       | Contributor| https://www.envoyproxy.io |https://github.com/envoyproxy/envoy|
| ONAP        | 项目 Leader        | https://www.onap.org||
| hugo-theme-cleanwhite | 创建者    | https://themes.gohugo.io/themes/hugo-theme-cleanwhite  | https://github.com/zhaohuabing/hugo-theme-cleanwhite | -->
