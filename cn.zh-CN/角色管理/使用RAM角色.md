# 使用RAM角色 {#task_221553 .task}

本文针对受信实体为阿里云账号的RAM角色为您介绍RAM用户如何扮演RAM角色登录控制台。

**说明：** 为了安全起见，阿里云不允许受信云账号以自己的身份扮演角色，如果一个实体用户想扮演某个RAM角色，该实体用户必须先以自己身份登录，然后将自己从实体身份切换到RAM角色身份。

使用RAM角色前，请先完成以下操作：

1.  [创建RAM用户](cn.zh-CN/用户管理/创建RAM用户.md#)。
2.  为该RAM用户创建访问密钥或设置登录密码。
    -   关于如何创建访问密钥，请参见[为RAM用户创建访问密钥](cn.zh-CN/安全设置/访问密钥/为RAM用户创建访问密钥.md#)。
    -   关于如何设置登录密码，请参见[修改RAM用户登录密码](cn.zh-CN/安全设置/密码/修改RAM用户登录密码.md#)。
3.  [为RAM用户授权](cn.zh-CN/用户管理/为RAM用户授权.md#)。
    -   您可以为RAM用户添加系统策略`AliyunSTSAssumeRoleAccess`。
    -   您也可以为RAM用户添加自定义策略指定可以扮演哪个RAM角色。详情请参见[RAM角色和STS token常见问题](../../../../cn.zh-CN/常见问题/RAM角色和STS token常见问题.md#)。

1.  RAM用户登录[RAM控制台](https://signin.aliyun.com/login.htm)。
2.  将鼠标悬停在右上角头像的位置，单击**切换身份**。
3.  在角色切换页面，输入相应账号别名或默认域名以及角色名，单击**切换**。 

    **说明：** 切换成功后，用户将以RAM角色身份登录控制台，控制台右上角头像位置将显示角色身份（即当前身份）和登录身份，此时用户只能执行该角色身份被授权的所有操作。

4.  在扮演角色身份时，将鼠标悬停在右上角头像的位置，单击**返回登录身份**可以切换回登录身份。

RAM用户也可以通过调用API扮演RAM角色。

当RAM用户被授予`AliyunSTSAssumeRoleAccess`权限策略之后，可以使用其访问密钥调用[AssumeRole](../../../../cn.zh-CN/API 参考（STS）/操作接口/AssumeRole.md#)接口，以获取某个角色的安全令牌，从而使用安全令牌访问阿里云。

**相关文档**  


[AssumeRole](../../../../cn.zh-CN/API 参考（STS）/操作接口/AssumeRole.md#)

