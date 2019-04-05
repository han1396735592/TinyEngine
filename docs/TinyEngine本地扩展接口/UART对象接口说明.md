# UART



## API

| API                    | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| UART.open(id)          | 功能：打开串口参数： id:和板级配置文件中的id保持一致返回值：返回资源handle |
| UART.read(handle，cb)  | 功能：从串口中读取数据参数： handle:资源handle，为UART.open的返回值;cb：读回调，返回读取状态值err和数据；返回值：0=ok other=fail |
| UART.on(handle，cb)    | 功能：从串口中读取数据; 参数： handle:资源handle，为UART.open的返回值; cb：监控回调，返回读取状态值err和数据； 返回值：0=ok other=fail |
| UART.write(handle,str) | 功能：串口发送数据参数： handle:资源handle，为UART.open的返回值;            str：待发送字符串返回值：0=ok other=fail |
| UART.close(handle)     | 功能：关闭串口; 参数： handle:资源handle，为UART.open的返回值; 返回值：0=ok other=fail |

## 示例代码

```
var handle=UART.open('uart2');
if(handle>0){
var value = UART.write(handle,'hello\r\n');
UART.on(handle,function(data){ 
    console.log(data);    
});
} else {
	console.log('open uart2 fail!');
}
```