[maven教程](https://www.bilibili.com/video/BV1Ah411S7ZE)
依赖范围
依赖的jar默认是在任何地方可用，可以使用scope限定其作用范围。
作用范围：
- 主程序范围内有效
- 测试程序范围内有效
- 是否参与打包，是否在运行时用到了
  
|Scope|主程序|测试代码|是否参与打包|举例|
|---|---|---|---|---|
|compile(默认)|Y|Y|Y|log4j|
|test||Y||Junit|
|provided|Y|Y||servlet-api|
|runtime|||Y|jdbc|








