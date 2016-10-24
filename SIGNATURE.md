第三方开发者需要申请用户，分配appKey(eg: **_rain2103jds_**)和appSecret(eg: **_fea98ca429a311a2de3c60a356c29211_**)

将请求参数和提交的body按照字典排序，然后跟uri和appSecret拼接，没有则为空，做md5加密，将得到的值通过`X-Rain-Signature` header参数传递过来。注意：如果参数中有特殊字符，需要做utf8的encode处理。

appSecret不需要出现在url里

> 示例1

假设请求为GET `/api/test/?user=123&role=student&op=submit`

则参数按字典排序后为`op=submit&role=student&user=123`

然后与`/api/test/?`和`fea98ca429a311a2de3c60a356c29211`连接后做32位MD5计算`md5('/api/test/?op=submit&role=student&user=123fea98ca429a311a2de3c60a356c29211')`得到`f9ecc6196fc51f73a6a05cc8c9032d14`

最后添加如下header：
```
X-Rain-Signature: f9ecc6196fc51f73a6a05cc8c9032d14
X-Rain-AppKey: rain2103jds
```
发送请求`/api/test/?user=123&role=student&op=submit`到服务器

> 示例2

假设请求为POST `/api/test?test=123`
```javascript
{
  "user": 123,
  "role": "student",
  "op": "submit"
}
```
则参数按字典排序后拼接为`test=123`

body按字典排序后拼接为`op=submit&role=student&user=123`

然后与`/api/test`和`fea98ca429a311a2de3c60a356c29211`连接后做32位MD5计算`md5('/api/test?test=123&op=submit&role=student&user=123fea98ca429a311a2de3c60a356c29211')`得到`5aad8474bc04cffdc456bb947a43585a`

最后添加如下header：
```
x-Rain-Signature: 5aad8474bc04cffdc456bb947a43585a
x-Rain-AppKey: rain2103jds
```
发送请求`/api/test?test=123`到服务器

```javascript 
{
  "user": 123,
  "role": "student",
  "op": "submit"
}
```
