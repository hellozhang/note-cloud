# prometheus-query查询

参考文章

1. [官方文档 QUERYING PROMETHEUS](https://prometheus.io/docs/prometheus/latest/querying/basics/)

prometheus的webUI -> Graph 页面可以输入类似于sql的语句, 查询各job获得的指标信息. 

程序在使用prometheus提供的SDK进行日志埋点时, 会有一些通用的指标, 比如golang版本信息, 当前CPU/内存占用, GC回收情况等(这些都是可以通过profile获得), 几乎所有的`/metrics`接口都会提供这些基础信息.

那么, 当我们希望查询某个接口后的系统所使用的golang信息时, 如果不添加一些过滤条件, 将得到所有job的结果.

![](https://gitee.com/generals-space/gitimg/raw/master/94CEF94EB2114279957792C443A3DDD6.png)

上面的结果中只有一行, 是因为当前prometheus中只有一个job, 抓取的是prometheus本身的指标信息. 如果是多个job, 那么可以尝试将过滤条件写作

![](https://gitee.com/generals-space/gitimg/raw/master/16E6CCDBD225D03C4A78523B313550CF.png)

我之后又尝试查看了其他的指标, 发现结果表格中"Element"列可供使用的过滤字段只有`instance`和`job`两个, 猜测应该是因为prometheus这个job只有这两个label吧.

![](https://gitee.com/generals-space/gitimg/raw/master/B4B4C41C791DAC5F9C5E88F104DD5ED7.png)
