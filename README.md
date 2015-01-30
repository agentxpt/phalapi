#PhalApi - 轻量级PHP后台接口开发框架 


###PhalApi是一个轻量级PHP后台接口开发框架，目的是让接口开发更简单。
#背景
过去十年，是互联网时代；如今的十年，是移动时代。  
  
在iOS、Android、Windows Phone、PC版、Web版等各种终端和各种垂直应用不停更新迭代的大背景下，显然很是需要一组乃至一系列稳定的后台接口支撑。
接口，是如此重要，正如Jaroslav Tulach在《软件框架设计的艺术》一书中说的：
```
API就如同恒星，一旦出现，便与我们永恒共存。
```

所以，这里希望通过提供一个快速可用的后台接口开发框架，可以：

```
一来，支撑各业务场景下接口开发；
二来，阐明如何进行接口开发、设计和维护，以很好支持海量访问、大数据、向前向后兼容等；
三来，顺便分享一些好的思想、技巧和有用的工具、最佳实践。
```

如果您有接口项目开发的需要，又刚好需要一个PHP接口框架，欢迎使用！    我们也争取致力于将我们的PhalApi维护成像恒星一样：  
```
不断更新，保持生气；为接口负责，为开源负责！
```


#安装
+ *请从release分支拉取稳定的代码*
+ *推荐在Linux服务器上进行开发*
+ *建议PHP >= 5.3.3*

将代码下载解压到服务器后即可，然后把根目录设置为Public。如nginx下：

```
root   /.../PhalApi/Public;
```

为验证是否安装成功，可以访问默认接口服务，如：http://localhost/PhalApi/，正常时会返回类如：
```
{
    "ret": 0,
    "data": {
        "title": "Default Api",
        "content": "PHPer您好，欢迎使用PhalApi！",
        "version": "1.0.0",
        "time": 1422118935
    },
    "msg": ""
}
```
#在线体验
```
//默认的接口服务
http://phalapi.oschina.mopaas.com/Public/

//带参数的示例接口
http://phalapi.oschina.mopaas.com/Public/?service=Demo.Test&username=oschina

//故意请求一个非法的服务
http://phalapi.oschina.mopaas.com/Public/?service=Demo.None

```

#文档
###后台接口开发就是如此简单，Write the code, enjoy yourself !

更多信息，请访问：[PhalApi - 轻量级PHP后台接口开发框架 - 让接口开发更简单](http://my.oschina.net/u/256338/blog/363288)  

#[酷！]接口参数在线查询
为了方便客户端查看最新的接口参数，特别提供此在线工具，根据接口代码实时生成接口参数报表，完全不需要后台开发编写维护额外的文档。我觉得，这很符合敏捷开发之道。
```
//接口参数在线查询工具链接
http://phalapi.oschina.mopaas.com/Public/helpers/checkApiParams.php
```
如：http://phalapi.oschina.mopaas.com/Public/helpers/checkApiParams.php ，访问效果如下：

 ![mahua](http://static.oschina.net/uploads/space/2015/0130/190225_8HRX_256338.jpg)
 因此，接口所需要的参数，对于接口开发人员，也只是简单配置一下参数规则，便可以轻松获取。
 
#[赞！]接口单元测试
不能被测试的代码，不是好代码。
在使用此框架进行接口开发时，我们强烈建议使用测试驱动开发，以便于不断积累形成接口测试体系，保证接口向前向后兼容。  
如下，是对接口 **/?service=User.GetBaseInfo&userId=1** 进行单元测试时，按： **构造-操作-检验（BUILD-OPERATE-CHECK）模式** ，即：  

```
    /**
     * @group testGetBaseInfo
     */ 
    public function testGetBaseInfo()
    {
        $str = 'service=User.GetBaseInfo&userId=1';
        parse_str($str, $params);

        Core_DI::one()->request = new Core_Request($params);

        $api = new Api_User(); 
        //自己进行初始化
        $api->initialize();
        $rs = $api->getBaseInfo();

        $this->assertNotEmpty($rs);
        $this->assertArrayHasKey('code', $rs);
        $this->assertArrayHasKey('msg', $rs);
        $this->assertArrayHasKey('info', $rs);

        $this->assertEquals(0, $rs['code']);

        $this->assertEquals('dogstar', $rs['info']['name']);
        $this->assertEquals('oschina', $rs['info']['from']);
    }
```
更多请参考：[最佳开发实践：自动化单元测试 - PHP](http://my.oschina.net/u/256338/blog/370605)
#更新日记
以下更新日记，主要是为了说明，我们一直在努力更新和维护。
###2015-01-29
```
1、examples代码重新整理，及入门文档同步更新；
2、入口文件的调整；
```

###2015-01-28
```
1、补充入门开发示例的文档，及相关的测试代码和产品代码，主要是examples；
2、提供接口参数在线查询工具；
```
###2015-01-24
```
1、PhalApi开源；
```