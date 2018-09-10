# Flask请求与响应/错误处理

### 1.url_for重定向/反向解析

##### 1.1重定向

自定义跳转方法, 跳转到自定义的方法上.

例如:

```
@blue.route('/getredirect/')
def get_redirect():

    return redirect('getresponse')
```

return redirect是指跳转到指定的app页面, 是固定的地址的跳转



##### 1.2url_for的反向解析

url_for的作用:输入函数名-->url_for(函数名)-->得到函数头上的app.route里面的东西.

 url_for的操作对象是函数,而不是route里面的路径.

使用方法:

```
url_for('蓝图实例化的第一个参数.需要跳转的函数名')
```

例如:

```
from flask import Flask, url_for
app = Flask(\__name__)

@app.route('/')
def index():
    pass

@app.route('/login')
def LOGIN():
    pass

with app.test_request_context():
    print(url_for('index'))
    print(url_for('login'))
```

`print(url_for('index'))`没有报错，就是一个反斜杠,`print(url_for('login'))`报错，抛出BuildError异常： 

把login修改为LOGIN： 

```
with app.test_request_context():
    print(url_for('index'))
    print(url_for('LOGIN'))
```

##### 1.3 参数

`url_for()`也可以附带一些参数，比如想要完整的URL，可以设置`_external`为Ture： 

```
url_for('.static',_external=True,filename='pic/test.png')
```

这样返回的url是<http://localhost/static/pic/test.png> 

- endpoint 
  URL的端点（即函数的名字）
- values 
  URL的变量参数
- _external 
  如果设置为`True`，则生成一个绝对路径URL
- _scheme 
  一个字符串指定所需的URL方案。_external参数必须设置为True，不然会抛出ValueError。
- _anchor 
  如果设置了这个则给URL添加一个mao
- _method 
  如果设置这个则显示地调用这个HTTP方法

### 2.异常的处理与接收

##### 2.1 定义终止程序

```
@app_blue.route('/getError/')
def get_error():
    try:
        3/0
    except Exception as e:
        # 抛出一个400的错误的状态
        abort(400)

    return '计算
```

##### 2.2捕获定义的异常

```

@app_blue.errorhandler(400)

def handler(exception):

    return '捕获的异常: %s' % exception
```

接收一个错误的状态   abort抛出错误的状态, errorhandler接收错误的状态











































































