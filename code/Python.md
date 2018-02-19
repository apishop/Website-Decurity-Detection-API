## 网站安全检测 - Python调用示例代码

#### 网站安全检测
检测假冒伪劣网站，识别钓鱼网站

#### 该产品拥有以下APIs：
1. 网站安全性检测

**注意，该示例代码仅适用于 [www.apishop.net](www.apishop.net "www.apishop.net") 网站下API**
**使用该产品前，您需要通过 [https://www.apishop.net/#/api/detail/?productID=111](https://www.apishop.net/#/api/detail/?productID=111 "https://www.apishop.net/#/api/detail/?productID=111") 申请API服务**

---

#### 1.网站安全性检测

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# 测试环境: python2.7
# 安装requests依赖 => pip install requests/ easy_install requests

# 导入requests依赖
import requests
import json
import sys

reload(sys)
sys.setdefaultencoding('utf-8')


def apishop_send_request(method, url, params=None, headers=None):
    '''
    转发请求到目的主机
    @param method str 请求方法
    @param url str 请求地址
    @param params dict 请求参数
    @param headers dict 请求头
    '''
    method = str.upper(method)
    if method == 'POST':
        return requests.post(url=url, data=params, headers=headers)
    elif method == 'GET':
        return requests.get(url=url, params=params, headers=headers)
    else:
        return None


method = "POST"
url = "https://api.apishop.net/common/verify/verifyURL"
headers = None
params = {			
		"URL":"" #待验证的url，如“https://apistore.eolinker.com”			
		"version":"" #版本（1：原始版本，速度较慢但准确率较高；2：新版本，速度快但准确率低），默认为版本2
}
result = apishop_send_request(method=method, url=url, params=params, headers=headers)
if result:
    body = result.text
    response = json.loads(body)
    status_code = response["statusCode"]
    if (status_code == '000000'):
        # 状态码为000000, 说明请求成功
        print('请求成功：%s' % (body,))
    else:
        # 状态码非000000, 说明请求失败
        print('请求失败: %s' % (body,))
else:
    # 返回内容异常，发送请求失败
    print('发送请求失败')


```