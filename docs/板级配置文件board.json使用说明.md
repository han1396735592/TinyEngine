# 板级配置文件board.json使用说明

[目录]

[名词解释](#名词解释)

[用途](#用途)

[如何配置及使用说明](#如何配置及使用说明)

​	[1 board.json的语法描述](#1-board.json的语法描述)

​	[2  支持的type描述](#2-支持的type描述)

​	[3 芯片/模组的硬件资源对应表 esp32+developerkit](#3-芯片/模组的硬件资源对应表-esp32+developerkit)



## 名词解释

* board.json文件： 对于每一个TinyEngine应用，都有一个名为board.json的板级配置文件，用于描述对应的板级硬件配置，如UART、I2C、GPIO、ADC等的配置。
* board.json语法：使用json字段描述，其中有type，port等硬件描述概念，对于每一款硬件(通常是芯片/模组/开发板)该配置文件均可能不同。



## 用途

不同的模组/芯片，各个端口和管脚的映射可能是不一样的，有的厂家或板型，会将 ESP32 的 PIN1，PIN2，PIN3，PIN4 映射成UART1，而有的映射成UART2，甚至有的会映射成 GPIO1，GPIO2，GPIO3，GPIO4。TinyEngine的板型配置文件主要是将硬件（芯片）的物理端口映射成为统一的应用层逻辑端口。这样映射的好处是在替换不同的硬件或者芯片时，只需要替换 board_config.json  而不用修改应用程序或设备程序，从而便于应用的跨平台运行。



## 如何配置及使用说明

前面了解到board.json文件是用于跟硬件板级相关的配置的，那么该如何去配置其中的字段呢？ 是否每一种硬件版型该配置都不一样？以及在哪里打开及修改该文件呢？下面将针对以上几个问题介绍。



### 1 board.json的语法描述

从board.json的后缀可以看出，其使用json语法进行描述。格式通常如下：

```
 {
 "objectid":{    
    "type":"GPIO",  
    "port":12,
    "dir":2,
    "pull":1
  }
  }
```

解释：

* objectid：定义了一个对象，后面大括号里面则描述了该对象的类型。 定义后可以在js中直接使用。

* type: 描述了该对象的类型，可以是TinyEngine支持的硬件扩展类型，如GPIO，I2C，ADC等。

* port：描述了该对象的端口，这里需要根据实际硬件连接及芯片的端口映射关系来填写。

* dir, pull: 是GPIO类型特有的，用于描述GPIO输出输出及上拉下拉，其他如ADC类型则有sampling采样频率这种类型描述。

  

  

### 2 支持的type描述

board.json的type用于描述该对象是什么硬件端口类型，而每一种type也拥有不同的描述字段，如GPIO与ADC的描述字段是不一样的，如下将介绍每一种type的描述类型。

| type类型 | 描述字段及含义                                               | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| GPIO     | port  ： 端口值，这里跟芯片datasheet上的管脚还有一个映射关系 | Number |
|          | dir： 方向；  0="output"  1="input"  2="irq"  3="analog";    | Number |
|          | pull:  上拉下拉；   0="pulldown"  1="pullup"  2="open";      | Number |

| type类型 | 描述字段及含义                                             | 类型   |
| -------- | ---------------------------------------------------------- | ------ |
| ADC      | port  ： 端口值，这里跟芯片datasheet上管脚还有一个映射关系 | Number |
|          | sampling： 采样率； 数值                                   | Number |

| type类型 | 描述字段及含义                                             | 类型   |
| -------- | ---------------------------------------------------------- | ------ |
| DAC      | port  ： 端口值，这里跟芯片datasheet上管脚还有一个映射关系 | Number |
|          | voltage：  默认输出电压 ， 取值： 0 - 255 整数。           | Number |

| type类型 | 描述字段及含义                                             | 类型   |
| -------- | ---------------------------------------------------------- | ------ |
| I2C      | port  ： 端口值，这里跟芯片datasheet上管脚还有一个映射关系 | Number |
|          | address_width:  设备I2C地址宽度;                           | Number |
|          | freq:    I2C总线速率; 该值一般在100000-400000范围；        | Number |
|          | mode:   声明I2C的主从模式;   1=master,2=slave；            | Number |
|          | dev_addr:  声明I2C的外设的I2C地址;                         | Number |

| type类型 | 描述字段及含义                                               | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| UART     | port  ： 端口值，这里跟芯片datasheet上管脚还有一个映射关系   | Number |
|          | data_width:   串口数据宽度值;   0=5bit;1=6bit;2=7bit;3=8bit; 4=9bit; | Number |
|          | baud_rate:     串口波特率;                                   | Number |
|          | stop_bits:    串口停止位;   0=1bit停止位; 1=2bit停止位； 一般是1bit停止位 | Number |
|          | flow_control:   串口流控制;  0=禁止流控; 1=使能cts流控；2=使能rts流控;3=使能cts和rts流控; | Number |
|          | parity_config： 串口奇偶校验  ; 0=无校验;1=奇校验;2=偶校验;  | Number |

| type类型 | 描述字段及含义                                             | 类型   |
| -------- | ---------------------------------------------------------- | ------ |
| PWM      | port  ： 端口值，这里跟芯片datasheet上管脚还有一个映射关系 | Number |
|          | freq：  频率值;                                            | Number |
|          | duty： 占空比；                                            | Number |

### 3 芯片/模组的硬件资源对应表 esp32+developerkit 

| ESP32Devkitc的硬件资源 |                                                              |                                                  |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------ |
| 功能/接口              | IO/资源映射                                                  | port值                                           |
| I2C1                   | SDA(IO2) SCL(IO4)                                            | 1                                                |
| I2C2                   | SDA(IO5) SCL(IO12)                                           | 2                                                |
| ADC1                   | IO36=channel0 <br />IO37=channel1 <br />IO38=channel2 <br />IO39=channel3 <br />IO32=channel4 <br />IO33=channel5 <br />IO34=channel6 <br />IO35=channel7 | 1                                                |
| ADC2                   | GPIO2=channel0 <br />GPIO4=channel1                          | 2                                                |
| UART0                  | 默认板级log打印                                              | 0                                                |
| UART1                  | TXD(IO17) RXD(IO16) CTS(IO15) RTS(IO14)                      | 1                                                |
| UART2                  | TXD(IO32)  RXD(IO33)                                         | 2                                                |
| GPIO                   | GPIO19(IO19) GPIO21(IO21) GPIO22(IO22) GPIO23(IO23)          | pin num  <br>跟原理图datasheet上的gpio数值一致） |
| DAC1                   | IO25=channelx(`请流蜂补充`)                                  | 1                                                |
| DAC2                   | IO26=channelx(`请流蜂补充`)                                  | 2                                                |
| PWM0                   | PWM(IO4) <br />`请流蜂补充channel的映射关系`                 | 0                                                |
| PWM1                   | PWM(IO35)<br />`请流蜂补充channel的映射关系`                 | 1                                                |
| WIFI                   | 内置                                                         |                                                  |
| BT                     | 内置                                                         |                                                  |
| WDG                    | 内置                                                         |                                                  |
| SD                     | SD0(SD0) SD1(SD1) SD2(SD2) SD3(SD3) CMD(CMD) CLK(CLK)        |                                                  |
| SPI                    | 待定                                                         |                                                  |

| **DevelopKit的硬件资源对应表** |                                                              |                                                              |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 功能/接口                      | IO/资源映射                                                  | port值                                                       |
| I2C1                           | SCL(PB6)  SDA(PB9)                                           | 1                                                            |
| I2C2                           | SCL(PB13)  SDA(PB14)                                         | 2                                                            |
| I2C3                           | SCL(PC0)  SDA(PC1)                                           | 3                                                            |
| ADC3                           | 暂不支持                                                     | 暂不支持                                                     |
| ADC4                           | 暂不支持                                                     | 暂不支持                                                     |
| UART1                          | TX(PA2)  RX(PA3)                                             | 1                                                            |
| UART3                          | TX(PC4)  RX(PC5)                                             | 3                                                            |
| CAN1                           | TX(PD1) RX(PD0)                                              | 1                                                            |
| IIS                            | FS(PB12) DA(PB15) MCLK(PC6) BCLK(PD10)                       |                                                              |
| IR                             | RX(PD6) CTL(PD5)                                             |                                                              |
| GPIO                           | developerkit使用的是STM32系列，有特定的port映射关系 [点击stm32port表](#STM32系列芯片的port端口映射表) | 见stm32port映射关闭表[点击stm32port表](#STM32系列芯片的port端口映射表) |

#### STM32系列芯片的port端口映射表

说明：适用于developerkit及其他stm32系列芯片/模组

| STM32上的管脚名称 (每16个为一组)              | TinyEngine映射的port值 |
| --------------------------------------------- | ---------------------- |
| PA0 - PA15                                    | 0 - 15                 |
| PB0 - PB15                                    | 16 - 31                |
| PC0 - PC15                                    | 32 - 47                |
| PD0 - PD15                                    | 48 - 63                |
| PE0 - PE15                                    | 64 - 79                |
| PF0 - PF15                                    | 80 - 95                |
| PG0 - PG15                                    | 96 - 111               |
| PH0 - PH15                                    | 112 - 127              |
| 举例：PD15对应的port值为63，PE9对应port值为73 |                        |



