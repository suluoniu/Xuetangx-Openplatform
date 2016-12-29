http接口
--------------------

**_domain_** http://b.xuetangx.com/

> 服务端获取Authorization Code

**_url_** /user/authorize

**_method_** GET

**_query_**
```javascript
{
  "appid": {appid},
  "appsecret": {appsecret},
  "nonce": {nonce}	//随机数
}
```
**_response_**
```javascript
{
  "status": 0,
  "code": {code}
}
```

> 请求二维码

**_url_** /user/login

**_method_** GET

**_query_**
```javascript
{
  "code": {code}	//上一步获取到的code
}
```
**_response_**
```javascript
{
	"status": 0,
	"message": "success",
	"data": {
		"loginid": 222,		//本次登录的id，用于后续扫码成功后通知时相匹配	
		"expire_seconds": 60,	//客户端本次请求二维码的过期时间，过期后需要重新请求		
		"ticket": "https://mp.weixin.qq.com/cgi-bin/showqrcode?ticket=gQHk8DoAAAAAAAAAASxodHRwOi8vd2VpeGluLnFxLmNvbS9xL216b0pHV1RseEZHOTZrdjYweFQzAAIEVoYJWAMEAI0nAA==",	//二维码		
图片
		"url": "http://weixin.qq.com/q/mzoJGWTlxFG96kv60xT3"	//二维码实际地址	
	}
}
```

> 通知扫码成功

**_url_** {第三方注册的回调地址}

**_method_** POST

**_response_**
```javascript
{
  "action": "login",
  "login_id": 222,	//对应请求二维码时的登录id
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
  "Auth": "uuid的加密,str类型",	//后续接口中的access_token
  "Beta": {"DownloadURL": "http://b.xuetangx.com", "ChangeLog": "beta1.0.0.25\u7248", "Version": "1.0.0.25", "LaunchDate": "2016-03-31T16:15:41"},
  "Stable": {"DownloadURL": "http://rain.xuetangx.com/", "ChangeLog": "\u6295\u7968\u6700\u591a\u53ef\u9009\u9879\u6570\u76ee\u4e0d\u4e00\u81f4\u4fee\u6539", "Version": "1.0.0.39", "LaunchDate": "2016-05-10T09:52:10"}
}
```

> 新建任务

**_url_** /task/create

**_method_** POST

**_body_**
```javascript
{
  "access_token": {access_token},
  "name": "任务名称",
  "target": "任务目标",
  "category": "experiment",		//任务类别：["experiment"]
  "custom": [	//自定义项，可选
  	{
		"field": "实验要求",
		"content": "xxxxxxx"
	}
  ],
  "deadline": 1402334034,	//截止时间戳(精确到秒) 
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "task_id": "582d79f909d8fd4cc56fe7c7"  //实验id，str
  }
}
```

> 发布任务

**_url_** /task/publish

**_method_** POST

**_body_**
```javascript
{
  "access_token": {access_token},
  "task_id": {task_id},
  "class": [1,2,3,4,10] //班级id
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```
> 删除任务

**_url_** /task/delete

**_method_** POST

**_body_**
```javascript
{
  "access_token": {access_token},
  "task_id": {task_id}
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 获取任务信息

**_url_** /task/info

**_method_** GET

**_query_**
```javascript
{
  "access_token": {access_token},
  "task_id": {task_id}
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "task_id": {task_id},
    "published": 1,					//0:未发布，1：已发布 
    "publish_time": 1402334034,	  
  	"teacher_id": 1,
    "name": "任务名称",
    "target": "任务目标",
    "deadline": 1402334034,	//截止时间戳(精确到秒)
	"custom": [{
		"field": "任务要求",
		"content": "xxxxx"
	}]
  }
}
```
> 上传任务行为数据

**_url_** /task/actions

**_method_** POST

**_body_**
```javascript
{
    "access_token": {access_token},
    "task_id": 1,
    "class_id": 12,
    "action": "开始实验"
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```
> 获取任务行为数据

**_url_** /task/actions

**_method_** GET

**_query_**
```javascript
{
  "access_token": {access_token},
  "task_id": {task_id}
}
```
**_response_**
```javascript
{
	"status": 0, 
	"message": 'ok',
	"data": [{
		"action_time": 140233403404,		//时间戳
		"action_describe": "开始实验"
	}, {
		"action_time": 140233403404,
		"action_describe": "操作电路板"
	}, {
		"action_time": 140233403404,
		"action_describe": "调整电路板"
	},{
		"action_time": 140233403404,
		"action_describe ":"提交实验数据"
	},{
		"action_time": 140233403404,
		"action_describe":"结束实验"
	}]
}
```

> 上传（提交）任务报告数据

**_url_** /task/data

**_method_** POST

**_body_**
```javascript
{
	"access_token": {access_token},
	"finished": 1,					//0:暂存，1:完成实验(即提交)  
	"task_id": "xxxxxx",
	"class_id": 12,
	"partners": [1,2,12,56],	//实验成员
	"data": [{		//实验数据，每个{}是一个group
		"title": "仿真实验",
		"content": [{
			"type": "image",	//取值：image图片，text文字，wave波形数据		
			"value": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
		}, {
			"type": "text",
			"value": "分布式的部分可使肌肤看电视不发顺丰不数据库的"
		}]
	}, {
		"title": "波形数据",
		"content": [{
			"type": "wave",
			"value": [{
				"unit": ["s", "V"],
				"axis": [[0, 0], [0.2, 0.12533323356430426], [0.4, 0.24868988716485482], [0.6, 0.36812455268467797], [0.8, 0.48175367410171532]]
			}, {
				"unit": ["s", "V"],
				"axis": [[0, 0], [0.2, 0.080000000000000002], [0.4, 0.16, 0.24000000000000002], [0.8, 0.32000000000000001], [1.6, 0.40000000000000002]]
			}]
		}]
	}]
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 获取任务报告数据

**_url_** /task/data

**_method_** GET

**_query_**
```javascript
{
    "access_token": {access_token},
    "task_id": "xxxx"
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "uid": 1,
    "uname": "李磊",
    "task_id": "xxxxx",
    "finished": 1,					//0:未完成， 1：已完成(不可再编辑)
    "partners":"李磊，韩梅梅",
    "finish_time": 1479806204,				//报告完成时间
    "created_time": 1479806204,				//首次提交报告时间
    "score": -1,					//-1: 未批改，0及以上为已批改的得分  
    "data": [{		//任务数据，每个{}是一个group
		"title": "仿真实验",
		"content": [{
			"type": "image",	//取值：image图片，text文字，wave波形数据		
			"value": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
		}, {
			"type": "text",
			"value": "分布式的部分可使肌肤看电视不发顺丰不数据库的"
		}]
	}, {
		"title": "波形数据",
		"content": [{
			"type": "wave",
			"value": [{
				"unit": ["s", "V"],
				"axis": [[0, 0], [0.2, 0.12533323356430426], [0.4, 0.24868988716485482], [0.6, 0.36812455268467797], [0.8, 0.48175367410171532]]
			}, {
				"unit": ["s", "V"],
				"axis": [[0, 0], [0.2, 0.080000000000000002], [0.4, 0.16, 0.24000000000000002], [0.8, 0.32000000000000001], [1.6, 0.40000000000000002]]
			}]
		}]
	}],
	"finished": 1
  }  
}
```

> 上传图片

**_url_** /upload

**_method_** POST

**_header_** Content-Type: multipart/form-data

**_body_**

```javascript
{
  "access_token": {access_token},
  "file": {$file}
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
      "url": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg",
      "time": 1402334034 
  }
}
```


> 获取我的任务

**_url_** /user/my_task/

**_method_** GET

**_query_**
```javascript
{
  "access_token": {access_token},
  "role": "student"	//角色取值为[teacher, student]
}
```
**_response_**
```javascript
{
    "status": 0,
    "message": "ok",
	//========教师身份========
    "data": {
		"courses": [{	//下面的课程
			"classrooms": [{	//该课程下面的班级
				"students_count": 8,
				"id": 2509,	//班级id
				"name": "658"	//班级名
			}],
			"name": "吧123",	//课程名
			"id": 217	//课程id
		}, {
			"classrooms": [{
				"students_count": 4,
				"id": 2407,
				"name": "测试"
			}, {
				"students_count": 2,
				"id": 2464,
				"name": "1"
			}],
			"name": "多选投票测试",
			"id": 159
		}],
		"tasks": [{		//创建的任务		
			"task_id": "xxxx",
			"name": "xxxx",
			"created_time": 1479955316,
			"publish_time": 1479955316,
			"deadline": 1479955316
		}]
	},
	//======学生身份======
	"data": [{	//存在任务的班级和任务详情
		"id": 2500,
		"name": "还把",
		"tasks": [	//实验数据，可选
			{
				"experiment_id": "582d79f909d8fd4cc56fe7c7",
				"name": "测试实验",
				"deadline": 1479955316,
				"publish_time": 1479720278
			}
		]
	}]
}
```
> 推送微信

> 批改实验报告

websocket接口
--------------------

**_domain_** ws://b.xuetangx.com/openws/

> 出二维码

**_message_**
```javascript
{
  "op": "login"
  "code": {code},
  "appid": {appid},
  "nonce": {nonce}	//随机数
}
```
**_response_**
```javascript
{
  "op": "login",
  "status": 0,
  "message": "success",
  "loginid": 222,
  "expire_seconds": 60,
  "ticket": "https://mp.weixin.qq.com/cgi-bin/showqrcode?ticket=gQHk8DoAAAAAAAAAASxodHRwOi8vd2VpeGluLnFxLmNvbS9xL216b0pHV1RseEZHOTZrdjYweFQzAAIEVoYJWAMEAI0nAA==",
  "url": "http://weixin.qq.com/q/mzoJGWTlxFG96kv60xT3"
}
```
> 通知扫码成功

**_response_**
```javascript
{
  "op": "loginsuccess",
  "status": 0,
  "message": "success",
  "login_id": 222,
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
  "Auth": "uuid的加密,str类型",	//后续接口中的access_token
  "Beta": {"DownloadURL": "http://b.xuetangx.com", "ChangeLog": "beta1.0.0.25\u7248", "Version": "1.0.0.25", "LaunchDate": "2016-03-31T16:15:41"},
  "Stable": {"DownloadURL": "http://rain.xuetangx.com/", "ChangeLog": "\u6295\u7968\u6700\u591a\u53ef\u9009\u9879\u6570\u76ee\u4e0d\u4e00\u81f4\u4fee\u6539", "Version": "1.0.0.39", "LaunchDate": "2016-05-10T09:52:10"}
}
```
