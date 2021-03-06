DjangoCaptcha 
=======================

![image](https://travis-ci.org/tianyu0915/DjangoCaptcha.png)
[![PyPI version](https://badge.fury.io/py/DjangoCaptcha.png)](http://badge.fury.io/py/DjangoCaptcha)

介绍
----
在django中生成英文单词验证码,提供验证码图片生成,检查验证码等功能
原用于[pythoner.net](http://pythoner.net)的验证码,现整理出来打包发布到pypi.

#### 新特性
+ 新增数字验证码模式
+ 字体尺寸根据图片长宽自适应


Usage
---
####Install####
```
pip install DjangoCaptcha
or
easy_install DjangoCaptcha
```
####Display(views.py)####
```
from DjangoCaptcha import Captcha
def code(request):
    ca =  Captcha(request)
    ca.words = ['hello','world','helloworld']
    ca.type = 'word'
    return ca.display()
```
or 

```
from DjangoCaptcha import Captcha
def code(request):
    figures         = [2,3,4,5,6,7,8,9]
    ca              = Captcha(request)
    ca.words        = [''.join([str(random.sample(figures,1)[0]) for i in range(0,4)])]
    ca.type         = 'word'
    ca.img_width    = 100
    ca.img_height   = 30
    return ca.display()

```

####Check user input(views.py)####
```
from DjangoCaptcha import Captcha
def index(request):
    _code = request.GET.get('code') or ''
    if not _code:
        return render('index.html',locals())

    ca = Captcha(request)
    if ca.check(_code):
        return HttpResponse('验证成功')
    else:
        return HttpResponse('验证失败')
```

Custom
-----
##### width of image
`ca.img_width` = 150
##### height of image 
`ca.img_height` = 30
##### type fo code ('number'/'word')
`ca.type = 'number'`


More
----
+ <http://pythoner.net>
