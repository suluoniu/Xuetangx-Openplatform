http接口
--------------------

**_domain_** http://api.ykt.io/


> 查询登录者信息

**_url_** /user/info

**_method_** GET

**_header_** 
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_response_**

```javascript
{
  "status": 0,
  "message": "ok",
  "data": {
     "loginid": 22222,
     "UserID": "int型用户id如123",
     "Name": "用户名字",
     "Nickname": "微信昵称",
     "Avatar": "微信头像的url地址,http://wx.qlogo.cn/mmopen/tnGT4YBoSbbUZmECibSLnDu2z5r2bpbDtH7zAiadRETvU8bQlTR8ObiapVUlaejbOiafmOkM8my6Q5NZ3dC3ACHIxIGKL27fxYG0/0",
     "WeixinUnionID": "微信的unionid,owHdquIH-AdQD7UMPohiIaQGjfA8",
     "AppOpenID": "用户针对此公众号的appid默认为none,oM_HWwYUcgHV9ewbAt76kWSeoL3g",
     "School": "所在院校",
     "Department": "所在院系",
     "Role": "身份,默认为0:0未填写1在校学生2老师3其他人员",
     "Position": "职别信息，默认为空",
     "YearOfBirth": "出生年份,datetime格式日期",
     "Gender": "性别,默认为0:0未填写1男2女",
     "LastLoginIP": "上次登录ip,如127.0.0.1",
     "DateJoined": "帐号注册时间datetime时间,%Y-%m-%dT%H:%M:%S格式",
     "LastLogin": "上次登录时间datetime时间,%Y-%m-%dT%H:%M:%S格式",
     "Auth": "uuid的加密,str类型",
     "Beta": {"DownloadURL": "http://b.xuetangx.com", "ChangeLog": "beta1.0.0.25\u7248", "Version": "1.0.0.25", "LaunchDate": "2016-03-31T16:15:41"},
     "Stable": {"DownloadURL": "http://rain.xuetangx.com/", "ChangeLog": "\u6295\u7968\u6700\u591a\u53ef\u9009\u9879\u6570\u76ee\u4e0d\u4e00\u81f4\u4fee\u6539", "Version": "1.0.0.39", "LaunchDate": "2016-05-10T09:52:10"}
    }
}
```



> 新建实验

**_url_** /experiment/create

**_method_** POST

**_header_**
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_body_**
```javascript
{
  "name": "测试试验",
  "target": "实现xxx",
  "requirements": "abc",
  "deadline": "140233403404",
  "
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```
> 发布实验

**_url_** /experiment/publish

**_method_** POST

**_header_**
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_body_**
```javascript
{
  "class": "1,2,3,4,10"
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```
> 上传实验行为数据

**_url_** /experiment/uploadAction

**_method_** POST

**_header_**
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_body_**
```javascript
{
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 上传实验报告数据

**_url_** /experiment/uploadData

**_method_** POST

**_header_**
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_body_**
```javascript
{
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 获取老师、班级、学生、实验的对应关系

**_url_** /user/relation

**_method_** GET

**_header_**
```javascript
{
  "X-Rain-AppKey": {appKey},
  "X-Rain-Signature": {signature},
  "X-Rain-UserId": {userId}
}
```
**_query_**
```javascript
{
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
  }
}
```

websocket接口
--------------------

**_domain_** ws://b.xuetangx.com/wsapp/

> 出二维码

**_message_**
```javascript
{
  "op": "login"
}
```
**_response_**
```javascript
{
  "op": "login",
  "status": 0,
  "message": "success",
  "loginid": 222, //雨课堂生成的登录ID
  "expire_seconds": 60, //二维码过期时间，类似微信扫码付款时1分钟自动切换二维码，客户端需要计时重新请求新的二维码
  "ticket": "https://mp.weixin.qq.com/cgi-bin/showqrcode?ticket=gQHk8DoAAAAAAAAAASxodHRwOi8vd2VpeGluLnFxLmNvbS9xL216b0pHV1RseEZHOTZrdjYweFQzAAIEVoYJWAMEAI0nAA==",  //二维码图片
  "url": "http://weixin.qq.com/q/mzoJGWTlxFG96kv60xT3"  //二维码对应的url地址，也可根据这个url串自己生成二维码
}
```
> 通知扫码成功

**_response_**
```javascript
{
  "op": "loginsuccess",
  "status": 0,
  "message": "success",
  "loginid": 222,
  "UserID": "int型用户id如123",
  "Name": "用户名字",
  "Nickname": "微信昵称",
  "Avatar": "微信头像的url地址,http://wx.qlogo.cn/mmopen/tnGT4YBoSbbUZmECibSLnDu2z5r2bpbDtH7zAiadRETvU8bQlTR8ObiapVUlaejbOiafmOkM8my6Q5NZ3dC3ACHIxIGKL27fxYG0/0",
  "WeixinUnionID": "微信的unionid,owHdquIH-AdQD7UMPohiIaQGjfA8",
  "AppOpenID": "用户针对此公众号的appid默认为none,oM_HWwYUcgHV9ewbAt76kWSeoL3g",
  "School": "所在院校",
  "Department": "所在院系",
  "Role": "身份,默认为0:0未填写1在校学生2老师3其他人员",
  "Position": "职别信息，默认为空",
  "YearOfBirth": "出生年份,datetime格式日期",
  "Gender": "性别,默认为0:0未填写1男2女",
  "LastLoginIP": "上次登录ip,如127.0.0.1",
  "DateJoined": "帐号注册时间datetime时间,%Y-%m-%dT%H:%M:%S格式",
  "LastLogin": "上次登录时间datetime时间,%Y-%m-%dT%H:%M:%S格式",
  "Auth": "uuid的加密,str类型",
  "Beta": {"DownloadURL": "http://b.xuetangx.com", "ChangeLog": "beta1.0.0.25\u7248", "Version": "1.0.0.25", "LaunchDate": "2016-03-31T16:15:41"},
  "Stable": {"DownloadURL": "http://rain.xuetangx.com/", "ChangeLog": "\u6295\u7968\u6700\u591a\u53ef\u9009\u9879\u6570\u76ee\u4e0d\u4e00\u81f4\u4fee\u6539", "Version": "1.0.0.39", "LaunchDate": "2016-05-10T09:52:10"}
}
```
> 心跳

**_message_**
```javascript
{
  "op": "heartbeat",
  "msgid": 1
}
```
**_response_**
```javascript
{
  "op": "heartbeat",
  "status": 0,
  "message": "success",
  "msgid": 1
}
```
