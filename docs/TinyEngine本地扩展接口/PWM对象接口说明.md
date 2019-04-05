# PWM



## API

| API                       | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| PWM.start(id)             | 功能：配置和启动PWM参数： id:和板级配置文件中的id保持一致          freq:频率          duty:占空比返回值：成功:返回资源handle,失败:-1 |
| PWM.getDuty(handle)       | 功能：获取当前pwm周期 参数：handle:资源handle，为PWM.open的返回值; 返回值：占空比值 |
| PWM.setDuty(handle，duty) | 功能：配置duty 参数： handle:资源handle，为PWM.open的返回值;  duty:占空比值返回值：0=ok other=fail |
| PWM.getFreq(handle)       | 功能：获取当前pwm频率  参数：handle:资源handle，为PWM.open的返回值;      返回值：频率值 |
| PWM.setFreq(handle, freq) | 功能：配置freq 参数： handle:资源handle，为PWM.open的返回值; freq:频率 返回值：0=ok other=fail |
| PWM.stop(handle)          | 功能：停止PWM 参数： handle:资源handle，为PWM.open的返回值;返回值：0=ok other=fail |



## API调用示例

```
/*samples/js/buzzer.js*/
print('buzzer uart test.....................');
var buzzer_handle=PWM.start('buzzer'); 
var cur_duty = PWM.getDuty(buzzer_handle);
console.log('cur_duty:'+cur_duty);
setInterval(function() {
	cur_duty += 1;
	if(cur_duty >= 100)cur_duty=0;
	PWM.setDuty(buzzer_handle,cur_duty);
}, 500);
print('end buzzer test........................');
```

