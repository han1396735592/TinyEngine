# WIFI对象接口说明

* 说明：该对象用于连接WIFI和获取IP的操作。

* 支持的对象方法有：
  * WIFI.getip
  * WIFI.connect



* WIFI.getip()方法说明

  * 功能：获取当前系统的IP地址。

  * 参数说明：无

  * 返回值：WIFI连接成功，成功获取IP则返回ip STRING字符串。

    ​               WIFI连接失败，未获取到IP则返回NULL。

  

* WIFI.connect(ssid,password,function(state){})方法说明

  * 功能：连接指定的WIFI AP

  * 参数说明：ssid为AP的WIFI名称，类型为STRING。

    ​		  passwd为AP的WIFI密码，类型为STRING。

    ​		 function()为连接的回调函数，其参数state为'CONNECTED'时代表WIFI连接成功。

    ​		其参数state为'DISCONNECT'时代表WIFI连接失败。

  * 返回值：调用成功返回0，失败返回-1.

    ​		注意：WIFI连接的成功与否需要根据回调函数function的参数state判断。



__JS 调用WIFI模块示例：__

```javascript
var ssid = "Xiaomi_296E_rock";
var passwd = "rockzhou";

//连接 AP
WIFI.connect(ssid,passwd,function(state){console.log('wifi state:'+state);

//取 IP 地址
var ip = WIFI.getip();
console.log('WIFI state getip ='+ip);

//网络初始化成功，联网
if (state == 'CONNECTED'){
	HTTP.request("http://www.baidu.com",function(result){
		console.log('http requst reulst=:'+result);
	});
}
});
```

运行结果log如下：

```plain
# I (3033) wifi: n:10 0, o:1 0, ap:255 255, sta:10 0, prof:1
I (4023) wifi: state: init -> auth (b0)
I (4063) wifi: state: auth -> assoc (0)
I (4093) wifi: state: assoc -> run (10)
I (4373) wifi: connected with Xiaomi_296E_rock, channel 10

BoneEngine > wifi state:CONNECTED 
BoneEngine > WIFI state getip =192.168.8.140 
```

