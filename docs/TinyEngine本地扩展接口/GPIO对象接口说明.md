# GPIO

## 

| API                      | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| GPIO.open(id)            | 功能：打开gpio     <br />参数： id:和板级配置文件中的id保持一致 <br />返回值：返回资源handle |
| GPIO.close(handle)       | 功能：关闭gpio <br />参数： handle:资源handle，为GPIO.open的返回值; <br />返回值：0=ok other=fail |
| GPIO.write(handle,level) | 功能：设置gpio输出电压 <br />参数： handle:资源handle，为GPIO.open的返回值;   <br /> level：电平值，0或1 返回值：0=ok other=fail |
| GPIO.read(handle)        | 功能：获取gpio输入电压  <br />参数： handle:资源handle，为GPIO.open的返回值;   <br /> 返回值：引脚电平值 |
| GPIO.on(handle,edge,cb)  | 功能：gpio中断监听  <br />参数：  <br />handle:资源handle，为GPIO.open的返回值;  <br />edge:中断触发类型，"rising"上升沿触发,"falling"下降沿触发,"both"双边沿触发;   <br />cb：服务function;  <br />返回值：0=ok other=fail |
|                          |                                                              |

### API接口调用示例

```
print('start gled test.....................');
var gled_level = 0;
var gled_handle = GPIO.open('gled'); 
setInterval(function() {
    GPIO.write(gled_level,1-gled_level);
    gled_level = 1-gled_level; 
}, 5000);
print('end gled test........................');
```

 