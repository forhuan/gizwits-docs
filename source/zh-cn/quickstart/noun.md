title:  机智云名词定义解释
---
# 说明
此文档将对机智云相关的术语进行定义与解析。如果在开发过程中遇到一些术语不太理解的可以参阅此文档。
# 云端名词定义
## 1.ProductKey
定义：产品标识码，开发者通过机智云后台创建新产品后，自动生成的一个32位字符串。在机智云的数据库中是一个唯一的号码，开发者将ProductKey写入设备主控MCU后，机智云通过此标识码对设备进行识别并自动完成注册。

解析：设备接入机智云的前提是，需要机智云认同这个设备。Productkey是设备接入机智云的一个重要参数，该参数的基本含义是：一款设备识别码。例如某公司生产空调、热水器，空调和热水器是不同款设备，该公司设备接入机智云，至少需要两个Productkey参数。在开发MCU过程中，需要使用到该参数。Product Key在机智云官网上可以查看到，请参考下图：

![Alt text](/assets/zh-cn/quickstart/noun/图片1.png)

Productkey在开发过程中的角色：

![Alt text](/assets/zh-cn/quickstart/noun/图片2.png)

## 2.Product Secret
定义：产品密钥，在生成Productkey的时候云端会对应生成一个Product Secret，该参数为关键性机密参数，不应向第三方泄露。该参数在绑定远程设备（一般为GPRS接入方案）的时候会使用到。

## 3.DID

定义：设备号，当一个设备初次接入机智云时，机智云自动根据ProductKey以及设备Wi-Fi模块MAC地址为此设备注册一个did，此did全网唯一，用于与用户的绑定及后续操作。

![Alt text](/assets/zh-cn/quickstart/noun/图片3.png)

## 4.AppID

定义：应用标识码，当开发者需要为一款智能产品开发应用（包括iOS、Android、Web应用等）时，后台会自动生成一个AppID，并与此设备进行关联。应用开发时需要填入此AppID。

解析：在云端创建一个产品的同时需要在该产品下添加一个应用，并区分Android与iOS等。AppID主要在开发APP的时候用到。并且在app中注册的所有用户绑定在该Appid下。Appid可以在机智云官网上可以查看到。

![Alt text](/assets/zh-cn/quickstart/noun/图片4.png)

![Alt text](/assets/zh-cn/quickstart/noun/图片5.png)


## 5.App Secret

定义：应用密钥，在云端生成AppID的时候，会对应生成一个App Secret，该参数在APP端SDK注册手机用户时，获取手机短信验证码的时候会用到。

## 6.小循环
定义：智能设备与手机、智能设备与智能设备之间，通过连接同一个路由器实现局域网内部的通信（查看状态或控制），我们称之为小循环。


## 7.大循环
定义：智能设备通过路由器或直接接入互联网以实现用户的远程监测与控制，我们称为大循环。

![Alt text](/assets/zh-cn/quickstart/noun/图片6.png)


# 设备端名词定义

## 1.Gagent
定义：全称Gizwits Agent，运行于Wi-Fi模块中，设备通过GAgent接入机智云服务器。 目前已兼容国内主流的Wi-Fi模块， 开发者也可以通过获取GAgent二次开发包实现自定义的模块接入机智云。

解析：Gagent是机智云运行在Wi-Fi模组的应用程序，Gagent主要作用是使得wifi模块主动连接机智云服务器，并实现与云端的TCP/UDP通信。因此，在开发者产品的控制电路板上集成Wifi模块，只需要实现与Wifi模组的串口通信，即可直接接入机智云服务器，而不需要处理底层的网络传输处理。如图所示：

![Alt text](/assets/zh-cn/quickstart/noun/图片7.png)

## 2.PassCode
定义：设备通行证，用于校验用户的绑定/控制权限。当用户发起设备绑定时，只要是合法操作即可拿到此通行证，通过此通行证绑定设备并对设备进行有效期内的查看、控制等操作。GAgent首次运行时生成随机数作为设备通行证，生成后保存在非易失性存储器上。设备上线时需要上报给服务器。

![Alt text](/assets/zh-cn/quickstart/noun/图片8.png)

## 3.Onboarding

定义：也叫配置入网，用户将一款基于Wi-Fi的物联网设备配置连接上路由器的过程称为Onboarding。新设备第一次使用时需要知道路由器的账号和密码，以通过路由器连接互联网。由于大多数的物联网设备没有自带的屏幕和键盘，所以需要通过智能手机向设备发送路由器的SSID和密码，这个过程机智云称为Onboarding。机智云提供的Wi-Fi设备接入SDK中已经内置了此配置的功能。

![Alt text](/assets/zh-cn/quickstart/noun/图片9.png)

## 4.Station模式

Station模式（简称sta）, 类似于无线终端，sta本身并不接受无线的接入，它可以连接到AP，一般无线网卡即工作在该模式。

## 5.AP模式
AP模式: Access Point，提供无线接入服务，允许其它无线设备接入，提供数据访问，一般的无线路由/网桥工作在该模式下。AP和AP之间允许相互连接。

## 6.AirLink
定义：机智云对各种SmartConfig、SmartLink这种UDP广播报方式对设备配置入网的技术统称，兼容了多个Wi-Fi模块厂商的配置协议，总结了一套良好用户体验的标准Onboarding操作流程，机智云的Wi-Fi 设备接入SDK已经内置AirLink技术。

## 7.SoftAP

定义：由于目前各个Wi-Fi模块厂商的Smart Config协议均未完全成熟，也不支持5G路由器信号。机智云在提供了AirLink配置模式的同时也支持SoftAP模式配置设备接入路由器。当设备进入SoftAP配置模式时，设备本身将成为一个AP，智能手机可直接与设备进行连接，然后在手机上的界面上输入路由器的SSID和密码，设备接收到信息的时候会自动尝试连接路由器，连接成功则自动切换到正常使用的模式。
