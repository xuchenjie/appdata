使用微信公众账号与树莓派通讯。可以扩展利用微信发送指令，树莓派返回相应数据。

因树莓派大多使用ADSL或者内网，不进行相关网络设置的情况下微信公众平台无法直接POST数据到树莓派。而且微信公众平台接口只能
使用80端口而且处理时间不能超过5秒，同时电信运营商也屏蔽了80端口，为解决这些问题因此而增加了服务器端。此处的架构设计是树
莓派主动连接服务器，连接和验证成功后使用心跳包维持持久连接。

用户的指令由微信公众平台POST到服务器端，服务器端将指令转发到树派。树莓派接受到指令后将处理结果返回服务器端，服务器端再
将结果处理后返回给微信。

服务器端分为http接口和socket接口，http接口和微信通讯，socket接口和树莓派通讯。socket接口采用多线程处理，同时连接多个客户
端，一台服务器可以同时为多个树莓派提供服务。

本系统可以扩展为通过树莓派获取室内温湿度，通过315M模块控制继电器从而控制电器开关，通过摄像头实时传回视频或图片，更多应
用各位自己想象扩展。

服务器端编译运行：
    
    gcc server.c -o server -lpthread
    
    ./server
    
树莓派客户端编译运行：
    
    gcc client.c -o client
    
    ./client
    
指令测试编译运行：
    
    gcc ipc.c -o ipc
    
    ./ipc
    
http服务器端：
将api.php文件部署到网站下，如http://www.xxx.com/api.php
    
在微信公众平台中将模式改为开发模式，填写URL和Token并修改api.php文件中的Token和填写的Token一致。
    
=======

appdata
