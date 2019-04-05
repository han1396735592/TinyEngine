# RTC



## API

| API              | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| RTC.open()       | 功能：打开rtc参数： 无返回值：0=ok other=fail                |
| RTC.close()      | 功能：关闭rtc参数： 无;返回值：0=ok other=fail               |
| RTC.setTime(obj) | 功能：配置rtc时间参数： obj:时间值对象，包含了年月日时分秒;  obj：时间参数，包含了时分秒年月;返回值：0=ok other=fail |
| RTC.getTime()    | 功能：读取rtc时间参数： 无;  返回值：json对象，包含了年月日时分秒; |



### 示例代码

```
print('start rtc test.....................');
RTC.open();
RTC.setTime({'year':18,'month':4,'day':29,'hour':12,'minute':57,'second':0});
setInterval(function() {
	var rtcdata = RTC.getTime(); 
	console.log(rtcdata.year+'/'+rtcdata.month+'/'+rtcdata.day+':'+rtcdata.second);	
}, 2000);
print('start end test.....................');
```

