/*
Title: smssdk
Description: smssdk
*/

<p style="color: #ccc; margin-bottom: 30px;">来自于：Mob官方<a style="background-color: #95ba20; color:#fff; padding:4px 8px;border-radius:5px;margin-left:30px; margin-bottom:0px; font-size:12px;text-decoration:none;" target="_blank" href="//www.apicloud.com/mod_detail/smssdk">立即使用</a></p>

<div class="outline">

[getTextCode](#a1)

[getVoiceCode](#a2)

[commitCode](#a3)

[getSupportedCountries](#a4)

[getFriends](#a5)

[submitUserInfo](#a6)

[getVersion](#a7)

[enableWarn](#a8)

</div>

##概述

短信验证码SDK，为开发者提供全球通用的短信验证码工具，开发者可以用其在App植入短信验证码SDK、简单设置即可短信验证，集成快速便捷，且后期易于管理。

####配置集成

开发者使用本模块之前需要先到[Mob官网](http://www.mob.com)申请开发者账号，并在账号内填写相应信息创建自己的 APP，从而获取**AppKey**和**AppSecret**,然后添加SMSSDK功能,获取**模板id**。

详情参考:[快速集成获取apppkey和appSecret](http://wiki.mob.com/快速集成-11/)

如有问题请联系技术支持: 

    服务电话:   400-685-2216     
    QQ:        4006852216
    节假日值班电话:
        iOS：185-1664-1951
    Android: 185-1664-1950
    电子邮箱:   support@mob.com
    市场合作:   021-54623100
    
<br>
####模块使用攻略

<p>
**使用此模块之前android需先配置config.xml文件，方法如下：**
    

```
	<meta-data name="Mob-AppKey" value="moba6b6c6d6"/>
	<meta-data name="Mob-AppSecret" value="b89d2427a3bc7ad1aea1e1e8c1d36bf3"/>
	
```
ios 需要将plist 文件放入res目录下，文件内容内容：
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>MOBAppKey</key>
	<string>moba6b6c6d6</string>
	<key>MOBAppSecret</key>
	<string>b89d2427a3bc7ad1aea1e1e8c1d36bf3</string>
</dict>
</plist>
```

- 字段描述:
 
    **Mob-AppKey**：（必须配置）从Mob官网获取的 AppKey。AppKey 申请方法参考[快速集成获取apppkey和appSecret](http://wiki.mob.com/快速集成-11/)。

    **Mob-AppSecret**：（必须配置）从Mob官网获取的 AppSecret。AppSecret 申请方法参考[快速集成获取apppkey和appSecret](http://wiki.mob.com/快速集成-11/)。

**编译app时iOS 请配置访问联系人的权限**

### [实例widget下载地址](https://github.com/MobClub/SMSSDK-for-APICloud-Demo)

##模块接口

需要引入模块:
```
var moduleSMSSDK = api.require('smssdk');
```
<div id="a1"></div>
    
#**getTextCode**
获取文本验证码(Get text verification code)
```
getTextCode({params}, callback(ret,err))
```
###params:

phoneNumber：

- 类型：字符串
- 	默认值：无
- 	描述：手机号

zone:

- 类型：字符串
- 	默认值：无
- 	描述：区域号，不要加"+"号

tempCode:

- 类型：字符串
- 	默认值：无
- 	描述：模板id


###callback(ret,err)

ret：

- 类型：JSON 对象
- 内部字段：

```
{
	smart:0  //是否为智能验证 bool类型, ios 忽略此字段
}
```

err：

- 类型：JSON 对象
- 内部字段：

```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
``` 
        
        
###示例代码

``` 
var param = {zone:'86', phoneNumber:'18500000000',tempCode:'1319972'};
moduleSMSSDK.getTextCode(param, function(ret, err){
    if (err !== null && err !== undefined && err !== '') {
     // 错误消息示例：{"msg":"Template not exist.","code":484}
    alert("Error:\n" + JSON.stringify(err));
    } else {
        // 正常消息示例：{"smart":false}
       alert("Success:\n" + JSON.stringify(ret));
    }
    });

``` 

<div id="a2"></div>
#**getVoiceCode**

获取语音验证码(Get text verification code)
```
getVoiceCode({params}, callback(ret, err))
```

###params:

phoneNumber:

- 类型：字符串
- 	默认值：无
- 	描述：手机号

zone:

- 类型：字符串
- 	默认值：无
- 	描述：区域号，不要加"+"号



###callback(ret, err)

ret：

- 类型：JSON 对象
内部字段：
{
}

err：

- 类型：JSON 对象
- 内部字段：


```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
```

###示例代码：
 
```                  
// param中的key命名不能改变
var param = {zone:'86', phoneNumber:'18500000000'};
moduleSMSSDK.getVoiceCode(param, function(ret, err){
  if (err !== null && err !== undefined && err !== '') {
   // 错误消息示例：{"msg":"Template not exist.","code":484}
   alert("Error:\n" + JSON.stringify(err));
  } else {
     // 正常消息示例：{}
    alert("Success:\n" + JSON.stringify(ret));
    }
   });

```                    

<div id="a3"></div>
#**commitCode**

提交验证码(Commit the verification code)

```
commitCode({params}, callback(ret, err))
```


###params:

phoneNumber:

- 类型：字符串
- 	默认值：无
- 	描述：手机号

zone:

- 类型：字符串
- 	默认值：无
- 	描述：区域号，不要加"+"号

code:

- 类型：字符串
- 	默认值：无
- 	描述：验证码

###callback(ret, err)

ret：

- 类型：JSON 对象
内部字段：
{
}

err：

- 类型：JSON 对象
- 内部字段：

```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
```

###示例代码：
    
```               
// param中的key命名不能改变
var param = {zone:'86', phoneNumber:'18500000000', code:'4847'};
moduleSMSSDK.commitCode(param, function(ret, err){
if (err !== null && err !== undefined && err !== '') {
  // 错误消息示例：{"msg":"Template not exist.","code":484}
  alert("Error:\n" + JSON.stringify(err));
  } else {
                                           
  }
  });
```

<div id="a4"></div>
#**getSupportedCountries**


获取区号(Get the Area code of the country)
```
getSupportedCountries(callback(ret, err))
```

###callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```
{
	countries =
	(
		{
    	rule = "^\\d+";
    	zone = 1868;
		}
	)
}
```

err：

- 类型：JSON 对象
- 内部字段：

```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
```

###示例代码：

```                                      
// param中的key命名不能改变
moduleSMSSDK.getSupportedCountries(function(ret, err){
    if (err !== null && err !== undefined && err !== '') {
     // 错误消息示例：{"msg":"Template not exist.","code":484}
      alert("Error:\n" + JSON.stringify(err));
     } else {
      // 正常消息示例：{"countries":[{zone=590, rule=^\d+},{zone=680, rule=^\d+}]}
        alert("Success:\n" + JSON.stringify(ret));
    }
  });
  
```

<div id="a5"></div>
#**getFriends**


向服务端请求获取通讯录好友信息

```
getFriends(callback(ret, err))
```

###callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```
{
	friends =
	(
   	 {
    	lastname : "你好";
    	others =     (
     			{
            	desc = "董浩";
            	phone = 10101155;
            	type = 1;
        	}
    	);
    	phones =     (
                	{
            	desc = "董浩";
            	phone = 10101155;
            	type = 1;
        	}
    	);
    	recordid = 411;
    	specialdate =     (
                	{
            	desc = "生日";
            	date = "1988-07-08";
            	type = 1;
        	}
    	);
	}
	)
}

```
err：

- 类型：JSON 对象
- 内部字段：


```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
```

###示例代码：

```                                       
// param中的key命名不能改变
moduleSMSSDK.getFriends(function(ret, err){
   if (err !== null && err !== undefined && err !== '') {
    // 错误消息示例：{"msg":"Template not exist.","code":484}
    alert("Error:\n" + JSON.stringify(err));
   } else {
    // 正常消息示例：{"countries":[{zone=590, rule=^\d+}, {zone=680, rule=^\d+}]}
     alert("Success:\n" + JSON.stringify(ret));
    }
 });
```

<div id="a6"></div>
#**submitUserInfo**


提交用户资料(Submit the user information data)
```
submitUserInfo({params}, callback(ret, err))
```

###params:

uid:

- 类型：字符串
- 	默认值：无
- 	描述：用户id

nickname:

- 类型：字符串
- 	默认值：无
- 	描述：用户昵称

avatar:

- 类型：字符串
- 	默认值：无
- 	描述：头像地址

phoneNumber:

- 类型：字符串
- 	默认值：无
- 	描述：手机号

zone:

- 类型：字符串
- 	默认值：无
- 	描述：区域号，不要加"+"号


###callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：
{
}

err：

- 类型：JSON 对象
- 内部字段：

```
{
    code:0    //错误码（详见错误码常量）
    msg:""    //错误描述
};
```

示例代码：
```                                  
// param中的key命名不能改变
var uid = "3241241";
var nickname = "SmsSDK_Api_Cloud_User_" + uid;
var avatar = "http://download.sdk.mob.com/510/deb/0c0731ac543eb71311c482a2e2.png";
// param中的key命名不能改变
var param = {uid:uid, nickname:nickname, avatar:avatar, phoneNumber:'18500000000', zone:'86'};

moduleSMSSDK.submitUserInfo(param, function(ret, err){
    if (err !== null && err !== undefined && err !== '') {
     // 错误消息示例：{"msg":"Template not exist.","code":484}
    alert("Error:\n" + JSON.stringify(err));
     } else {
    }
});

```

<div id="a7"></div>
#**getVersion**


返回SDK版本号(Return the version number of this SDK)
```
getVersion(callback(ret, err))
```
###callback(ret,err)

ret

- 类型：JSON 对象
- 内部字段：

```
{
	version: "1.0.0"
}
```

err

- 类型：JSON 对象
- 内部字段：
{
}


示例代码：
```
// param中的key命名不能改变
moduleSMSSDK.getVersion(function(ret, err){
if (err !== null && err !== undefined && err !== '') {
  // 错误消息示例：{"msg":"Template not exist.","code":484}
  alert("Error:\n" + JSON.stringify(err));
  } else {
   // 正常消息示例：{"version":'3.2.2'}
  }
});

```
<div id="a8"></div>
#**enableWarn**


是否允许访问通讯录好友(is Allowed to access to address book)
```
enableWarn({params})
```

###params:

isWarn:

- 类型：布尔
- 	默认值：true
- 	描述：YES 代表启用 NO 代表不启用 默认为启用

示例代码：
```
// param中的key命名不能改变
var isWarn = true;
// param中的key命名不能改变
var param = {isWarn:isWarn};
moduleSMSSDK.enableWarn(param);
```