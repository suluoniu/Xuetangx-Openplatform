第三方开发者需要申请用户，分配`appKey`(eg: **_rain2103jds_**)和`appSecret`(eg: **_fea98ca429a311a2de3c60a356c29211_**)

将请求参数和提交的body(需要包含appKey)按照字典排序，然后跟uri和`&appSecret`拼接，没有则为空，做base64编码，将编码后的字符串中的'/'和'+'分别替换为‘_’和'-'，然后进行HMAC1-SHA1加密，将得到的值再做base64编码和替换，最后通过url(GET)或者body(POST)传递过来。

appSecret不要出现在url里

> 示例1

假设请求为GET `/api/test?user=123&role=student&op=submit`

则参数按字典排序后为`appkey=rain2103jds&op=submit&role=student&user=123`

然后与`/api/test?`和`fea98ca429a311a2de3c60a356c29211`连接后为`/api/test?appkey=rain2103jds&op=submit&role=student&user=123&fea98ca429a311a2de3c60a356c29211`,做base64编码和替换得到`L2FwaS90ZXN0P2FwcGtleT1yYWluMjEwM2pkcyZvcD1zdWJtaXQmcm9sZT1zdHVkZW50JnVzZXI9MTIzJmZlYTk4Y2E0MjlhMzExYTJkZTNjNjBhMzU2YzI5MjEx`，然后计算HMAC1-SHA1 `hmac_sha1('L2FwaS90ZXN0P2FwcGtleT1yYWluMjEwM2pkcyZvcD1zdWJtaXQmcm9sZT1zdHVkZW50JnVzZXI9MTIzJmZlYTk4Y2E0MjlhMzExYTJkZTNjNjBhMzU2YzI5MjEx')`得到`GSlMLwhf5XZ1OJt6Yd/GXcjGkfQ=`，将其再进行base64编码和替换，得到最终的签名 `R1NsTUx3aGY1WFoxT0p0NllkL0dYY2pHa2ZRPQ==`。

最后将`R1NsTUx3aGY1WFoxT0p0NllkL0dYY2pHa2ZRPQ==`作为参数一起发送到服务器`/api/test?user=123&role=student&op=submit&appKey=rain2103jds&signature=R1NsTUx3aGY1WFoxT0p0NllkL0dYY2pHa2ZRPQ==`
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
与GET请求一样进行编码加密等操作，将最后的结果添加到body中。

发送请求`/api/test?test=123`到服务器

```javascript 
{
  "user": 123,
  "role": "student",
  "op": "submit",
  "signature": "MEFtQlA4T3VFcTJEdUhCakpGNzF6YVJndlNrPQ=="
}
```

下面是Node.js版本的签名算法
```
import crypto from 'crypto';

/**
 * 签名工具
 *
 * @param options
 *          options= {
 *              path: '',
 *              query: {},
 *              body: {},
 *              appSecret: ''
 *          }
 * @constructor
 */
class SignUtil {
    constructor(options = {}) {
        this.query = options.query;
        this.body = options.body;
        this.path = options.path;
        this.appSecret = options.appSecret || 'openplat';
    }
    /**
     * 计算签名
     *
     * @param appSecret APP密钥
     * @param path
     * @param query
     * @param body
     * @return 签名后的字符串
     */
    buildStringToSign () { 	
        //todo: 编码处理
        let queryStr = raw(this.query);
        let bodyStr = raw(this.body);
        let signStr = this.path + '?' + (queryStr ? (queryStr + '&') : '') + (bodyStr ? (bodyStr + '&') : '') + this.appSecret;

		let encodedFlags = this.urlsafeBase64Encode(signStr);
        let sign = this.hmacSha1(encodedFlags, this.appSecret);
	
        return this.urlsafeBase64Encode(sign);
    }

	urlsafeBase64Encode (str) {
		let encoded = new Buffer(str).toString('base64');
		return this.base64ToUrlSafe(encoded);
	}

	base64ToUrlSafe (v) {
		return v.replace(/\//g, '_').replace(/\+/g, '-');
	}

	hmacSha1 (encodedFlags, secretKey) {
		let hmac = crypto.createHmac('sha1', secretKey);
		hmac.update(encodedFlags);
		return hmac.digest('base64');
	}
	/**
     * 检查签名
     * @param signature 签名
     * @returns {boolean} 签名是否正确
     */
    checkSgin (signature = '') {
        return this.buildStringToSign() === signature;
    }

}

/*!
 * 排序查询字符串
 */
var raw = function (args) {
    if(!args || !Object.keys(args).length){
        return '';
    }
    let keys = Object.keys(args),  str = '';
    keys.sort().forEach(function (key) {
        str += '&' + key + '=' + args[key];
    });

    return str.slice(1);
};

```

