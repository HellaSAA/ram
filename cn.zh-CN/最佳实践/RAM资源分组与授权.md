# RAM资源分组与授权 {#concept_d2j_wdk_xdb .concept}

若您的公司购买了多种阿里云资源，您可以通过创建资源组进行云资源分组，从而实现独立管理资源组内成员、权限和资源。

## 前提条件 {#section_m72_l8e_f9v .section}

请确保您已经注册了阿里云账号。如还未注册，请先完成账号注册。详情请参见[账号注册](https://account.aliyun.com/register/register.htm)。

## 背景信息 {#section_01 .section}

某游戏公司A正在开发3个游戏项目，每个游戏项目都会用到多种云资源。公司A只有1个阿里云账号，该云账号下有超过100个ECS实例。

公司A有如下要求：

-   项目独立管理：每个管理员各自能够独立管理项目人员及其访问权限。
-   按项目分账：财务部门希望能够根据项目进行出账，以解决财务成本分摊的问题。
-   共享底层网络：客户希望云资源的底层网络默认共享。

公司A有如下解决方案：

-   多账号方案
    -   可以满足项目独立管理：公司A注册3个账号（对应3个项目），每个账号有对应项目管理员可以独立管理成员及其访问权限。
    -   可以满足按项目分账：每个账号有默认账单，可以利用阿里云提供的多账号合并记账能力来解决统一账单和发票问题。
    -   无法满足共享底层网络：账号之间是有安全边界的，不同账号之间的资源是100%隔离的，网络之间默认不通。虽然可以通过VPC-Peering来打通跨账号的VPC网络，但会带来较高的管理成本。
-   单账号给资源打标签方案
    -   无法满足项目独立管理：给资源打标签可以模拟项目分组，但无法解决项目管理员独立管理项目成员及其访问权限的问题。
    -   可以满足按项目分账：按照项目组给资源打上对应标签，根据标签实现分账。
    -   可以满足共享底层网络：公司A只用1个账号，根据项目打不同的项目标签，结合RAM提供的基于标签的条件授权能力，可以将一组资源授权给某些RAM用户，不存在打通网络所需的额外管理成本。
-   [资源组管理方案](#) 
    -   可以满足项目独立管理：每个资源组有对应的管理员，资源组管理员可以独立管理成员及其访问权限。
    -   可以满足按项目分账：账单管理功能支持按资源组进行分账，解决财务成本分摊的问题。
    -   可以满足共享底层网络：资源组属于账号内部的分组功能，同一账号下的不同资源组可以共享同一个VPC网络，节约管理成本。

## 解决方案 {#section_03 .section}

资源组是在阿里云账号下进行资源分组管理的一种机制，公司A只需使用1个账号，创建3个资源组（对应3个项目）。

![资源组解决方案](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23774/156396240814357_zh-CN.png)

1.  创建3个RAM用户：`alice@secloud.onaliyun.com`、`bob@secloud.onaliyun.com`和`charlie@secloud.onaliyun.com`。

    详情请参考：[创建RAM用户](../cn.zh-CN/用户指南/用户/创建 RAM 用户.md#)。

    **说明：** 下面的操作均以RAM用户Alice为例，介绍如何将其设为项目的管理员。

2.  登录[资源管理控制台](https://resourcemanager.console.aliyun.com/)。
3.  单击左侧导航栏的**资源组管理**，单击**新建资源组**。
4.  输入**标识**和**显示名**后，单击**确定**。

    **说明：** 创建3个资源组，分别命名为：Game1、Game2、Game3。

5.  找到创建好的资源组，单击**管理权限**。
6.  在**权限管理**页签下，单击**新增授权**。
7.  在**被授权主体**区域下，输入Alice，单击其名称。
8.  在**权限策略名称**列表下，单击`AdministratorAccess`。
9.  单击**确定**。

**说明：** 如何将Bob或Charlie设置为资源组管理员，请参考上述步骤。

## 下一步 {#section_05 .section}

由于Alice、Bob和Charlie分别是Game1、Game2、Game3的资源组管理员，将有以下权限：

-   登录ECS控制台，可以看到相应资源组，并可以创建和管理ECS实例。
-   登录资源管理控制台，可以添加其它RAM用户并授予相应的资源访问权限。

