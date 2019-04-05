# DAC



## API

| API                    | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| DAC.open(id)           | 功能：打开dac参数： id:和板级配置文件中的id保持一致返回值：成功：回资源handle，失败：-1 |
| DAC.close(handle)      | 功能：关闭dac 参数： handle:资源handle，为DAC.open的返回值; 返回值：0=ok other=fail |
| DAC.setVol(handle,vol) | 功能：设置dac输出电压 参数： handle:资源handle，为DAC.open的返回值;                vol：电压值 返回值：0=ok other=fail |
| DAC.getVol(handle)     | 功能：获取当前dac电压; 参数： handle:资源handle; 返回值：电压值; |

## 示例代码

```
var lm358 = function(id) {
  this.handle = DAC.open(id);
  this.setVal = function(val) {
    DAC.setVol(this.handle,val);
  };
  this.getVal = function() {
    var val = DAC.getVol(this.handle);
    return val;
  };
};
```

 