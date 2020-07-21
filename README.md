# 背景  
canal的具体使用，请参考阿里官方的代码，已经有非常详细的说明，这里就不多说明了。  
地址：https://github.com/alibaba/canal  
在canal具体的使用中，遇到一些bug以及不便之处，拉了一个分支进行修改，如有兴趣，欢迎大家补充。

# 说明  

## ES初始化  
一个全新的ES无法使用，因为没有创建es index和mapping,增加了对应的功能。
ES配置文件mapping节点增加两个参数：
``` yml
  enablefieldmap: true
  fieldmap:
    id: "text"
    BuildingId: "text"
    HouseNum: "text"
    Floors: "text"
    IdProjectInfo: "text"
    HouseDigitNum: "text"
    BuildingNum: "text"
    BuildingName: "text"
    Name: "text"
    projectid: "text"
    bIdProjectInfo: "text"
    cinitid: "text"
    pCommunityId: "text"
```

enablefieldmap 是否需要自动生成fieldmap，默认为false,如果需要启动的时候就生成这设置为true,并且设置
fieldmap,类似es mapping中每个字段的类型。

## esconfig bug处理
代码中获取binlog的日志处理时，必须要获取数据库名，但是当获取binlog为type query时，是无法获取
数据库名的，此处有bug，导致出现 "Outer adapter write failed" ,且未输出错误日志，修复此bug.

## 后续计划  
增加rabbit MQ的支持  
增加redis的支持（建议实现）