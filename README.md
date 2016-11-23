http接口
--------------------

**_domain_** http://b.xuetangx.com/

> 新建实验

**_url_** /experiment/create

**_method_** POST

**_body_**
```javascript
{
  "appkey": {appkey},
  "signature": {signature},
  "uid": {uid}, //老师id，int
  "uname": "老师名字",
  "name": "实验名称",
  "target": "实验目标",
  "requirements": "实验要求",
  "deadline": 1402334034,	//截止时间戳(精确到秒) 
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "experiment_id": "582d79f909d8fd4cc56fe7c7"  //实验id，str
  }
}
```

> 发布实验

**_url_** /experiment/publish

**_method_** POST

**_body_**
```javascript
{
  "appkey": {appkey},
  "signature": {signature},
  "uid": {uid},
  "experiment_id": {experiment_id},
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
> 取消发布实验

**_url_** /experiment/cancel

**_method_** POST

**_body_**
```javascript
{
  "appkey": {appkey},
  "signature": {signature},
  "uid": {uid},
  "experiment_id": {experiment_id}
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 获取实验信息

**_url_** /experiment/info

**_method_** GET

**_query_**
```javascript
{
  "appkey": {appkey},
  "signature": {signature},
  "uid": {uid},
  "experiment_id": {experiment_id}
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "experiment_id": {experiment_id},
    "published": 1,					//0:未发布，1：已发布 
    "publish_time": 1402334034,	  
  	"teacher_id": 1,
    "name": "实验名称",
    "target": "实验目标",
    "requirements": "实验要求",
    "deadline": 1402334034,	//截止时间戳(精确到秒)		
    "classes": [{									//学生角色没有该字段，该字段老师使用
      "id": 1,
      "name": "class1",
      "finished_num": 20, 
      "total_num": 50, 
    },{
      "id": 2,
      "name": "class2",
      "finished_num": 20, 	//已完成人数
      "total_num": 50, 		//总人数
    }]
  }
}
```
> 上传实验行为数据

**_url_** /experiment/actions

**_method_** POST

**_body_**
```javascript
{
    "appkey": {appkey},
    "signature": {signature},
    "uid": 9,
    "uname": "xxx",
    "experiment_id": 1,  
    "action_logs": [{
      "action_time": 1402334034,		//时间戳
      "action_describe": "开始实验"
    }, {
      "action_time": 1402334034,
      "action_describe": "操作电路板"
    }, {
      "action_time": 1402334034,
      "action_describe": "调整电路板"
    },{
      "action_time": 1402334034,
      "action_describe": "提交实验数据"
    },{
      "action_time": 1402334034,
      "action_describe": "结束实验"
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
> 获取实验行为数据

**_url_** /experiment/actions

**_method_** GET

**_query_**
```javascript
{
  "appKey": {appKey},
  "signature": {signature},
  "uid": 9,
  "experiment_id": 1
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": {
    "experiment_id": 1,  
    "action_logs": [{
      "action_time": "140233403404",		//时间戳
      "action_describe": "开始实验"
    }, {
      "action_time": "140233403404",
      "action_describe": "操作电路板"
    }, {
      "action_time": "140233403404",
      "action_describe": "调整电路板"
    },{
      "action_time":"140233403404",
      "action_describe ":"提交实验数据"
    },{
      "action_time":"140233403404",
      "action_describe":"结束实验"
    }]
  }  
}
```

> 上传（提交）实验报告数据

**_url_** /experiment/data

**_method_** POST

**_body_**
```javascript
{
	"appKey": {appKey},
	"signature": {signature},
	"uid": {uid},
	"uname": "李磊",
	"finished": 1,					//0:暂存，1:完成实验(即提交)  
	"experiment_id": 1,
	"partners": "李磊，韩梅梅",	//实验成员
	"theory": "分布式的部分可使肌肤看电视不发顺丰不数据库的",	//原理分析
	"simulation": [{	//仿真实验
		"type": "image",	//图片
		"content": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
	}, {
		"type": "text",		//文字
		"content": "分布式的部分可使肌肤看电视不发顺丰不数据库的"
	}],
	"processes": [{		//实验过程记录
		"type": "image",
		"content": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
	}, {
		"type": "text",
		"content": "分布式的部分可使肌肤看电视不发顺丰不数据库的"
	}],
	//实验结论分析
	"analysis": "分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不不数据库的",
	//反思与收获
	"achievement": "分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不发据库的" 
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok'
}
```

> 获取实验报告数据

**_url_** /experiment/data

**_method_** GET

**_query_**
```javascript
{
    "appKey": { appKey },
    "signature": { signature },
    "uid": { uid },
    "experiment_id": 1
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
    "experiment_id": 1,
    "finished": 1,					//0:未完成， 1：已完成(不可再编辑)
    "partners":"李磊，韩梅梅",
    "score": -1,					//-1: 未批改，0及以上为已批改的得分  
    "theory":"分布式的部分可使肌肤看电视不发顺丰不数据库的",
    "simulation": [{
      "type": "image",
      "content": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
    },{
      "type": "text",
      "content": "分布式的部分可使肌肤看电视不发顺丰不数据库的" 
    }],
    "processes":[{
      "type": "image",
      "content": "http://img.kanzhun.com/images/logo/20150906/f4ff637d692de37199c8665cf70746fa.jpg"
    },{
      "type": "text",
      "content": "分布式的部分可使肌肤看电视不发顺丰不数据库的" 
    }],
     "analysis": "分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不不数据库的",
     "achievement": "分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使肌肤看电视不发顺丰不数据库的分布式的部分可使",
     "score": -1,	//-1表示未批改
     "finished": 1
  }  
}
```

> 搜索学生实验报告

**_url_** /experiment/search

**_method_** GET

**_query_**
```javascript
{
    "appKey": { appKey },
    "signature": { signature },
    "uid": { uid },
    "experiment_id": 1,
    "name": "李磊"
}
```
**_response_**
```javascript
{
  "status": 0, 
  "message": 'ok',
  "data": [{
    "uid":1,
    "name": "lilei",
    "finished_time": "140233403404"
  },{
    "uid":2,
    "name": "lilei2",
    "finished_time": "140233403404"
  }]
}
```

> 上传图片

**_url_** /upload

**_method_** POST

**_header_** Content-Type: multipart/form-data

**_body_**

```javascript
{
  "appKey": {appKey},
  "signature": {signature},
  "uid": {uid}
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


> 获取老师、班级、学生、实验的对应关系

**_url_** /user/relation

**_method_** GET

**_query_**
```javascript
{
  "appKey": {appKey},
  "signature": {signature},
  "uid": "用户id"
}
```
**_response_**
```javascript
{
    "status": 0,
    "message": "ok",
    "data": {
		"courses": [{	//教师身份，下面的课程
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
		"classrooms": [{	//学生身份，所在的全部班级
			"course": {	//班级所属课程
				"name": "雷测试",	//课程名
				"id": 133	//课程id
			},
			"students_count": 6,
			"id": 2370,	//班级id
			"name": "2"	//班级名
		}, {
			"course": {
				"name": "新版测试",
				"id": 213
			},
			"students_count": 5,
			"id": 2500,
			"name": "还把",
			"experiments": [	//实验数据，可选
				{
					"experiment_id": "582d79f909d8fd4cc56fe7c7",
					"name": "测试实验",
					"deadline": 1479955316,
					"publish_time": 1479720278
				}
			]
		}, {
			"course": {
				"name": "123新的测试课程",
				"id": 191
			},
			"students_count": 2,
			"id": 2469,
			"name": "测试日志合并"
		}]
	} 
}
```
> 推送微信

> 批改实验报告




websocket接口
--------------------

**_domain_** http://ws.ykt.io/

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
  "loginid": 222,
  "expire_seconds": 100,
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
  "Auth": "uuid的加密,str类型",
  "Beta": {"DownloadURL": "http://b.xuetangx.com", "ChangeLog": "beta1.0.0.25\u7248", "Version": "1.0.0.25", "LaunchDate": "2016-03-31T16:15:41"},
  "Stable": {"DownloadURL": "http://rain.xuetangx.com/", "ChangeLog": "\u6295\u7968\u6700\u591a\u53ef\u9009\u9879\u6570\u76ee\u4e0d\u4e00\u81f4\u4fee\u6539", "Version": "1.0.0.39", "LaunchDate": "2016-05-10T09:52:10"}
}
```
