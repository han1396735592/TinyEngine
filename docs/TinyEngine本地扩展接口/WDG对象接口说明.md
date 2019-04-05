# WDG



## API

| API                | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| WDG.start(timeout) | 功能：启动看门狗定时器参数： timeout：喂狗超时时间，单位是ms返回值：0=ok other=fail |
| WDG.stop()         | 功能：停止看门狗定时器参数： 无返回值：0=ok other=fail       |
| WDG.feed()         | 功能：喂狗参数： 无返回值：0=ok other=fail                   |

## API接口调用示例

```
WDG.start(2000);
setInterval(function() {
	WDG.feed();
	console.log('feed the dog!\n');
}, 1000);
```

如果在规定的时间内没有进行喂狗操作，系统将自动重启。

