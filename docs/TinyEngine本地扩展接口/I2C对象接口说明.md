# I2C



## API

| API                    | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| I2C.open(id)           | 功能：打开i2c端口参数： id:和板级配置文件中的id保持一致返回值：ok=资源handle，fail=-1; |
| I2C.close(handle)      | 功能：关闭i2c端口参数： handle:资源handle，为I2C.open的返回值;返回值：0=ok other=fail |
| I2C.write(handle,buff) | 功能：向某I2C设备写入数据参数： handle:资源handle，为I2C.open的返回值;  buff：需要写入数据，类型是array;返回值：0=ok other=fail |
| I2C.read(handle,size)  | 功能：读取寄存器值； 参数： handle:资源handle，为I2C.open的返回值;  size：需要读取的数据长度; 返回值：read返回值，类型是array; |

## 示例代码

 ```
var delay = function(val){
  var i = 0;
  var tmp = 0;
  for(i=0;i<val;i++){
    tmp = 0;
  }
};

var tmp102 = function(id) {
  this.handle = I2C.open(id);
  this.openFlag = 0;
  this.regRead = function(reg){
    var data = [0x00];
    data[0] = reg;
    I2C.write(this.handle,data);
    var val = I2C.read(this.handle,1);
    return val[0];

  };

  this.init = function(){
    var data = [0x00,0x00];
    data[0] = 0x70;
    data[1] = 0xa0;
    I2C.write(this.handle,data);
  };

  this.getTemperature = function(){

    if(0 == this.openFlag){
      this.init();
      this.openFlag = 1;
    }

    var data = [0x00];
    I2C.write(this.handle,data);
    var val = I2C.read(this.handle,2);
    var temp = ((val[0]<<8) | (val[1])) >> 4;
    temp = temp * 0.0625;
    return temp;
  };
};
 ```

