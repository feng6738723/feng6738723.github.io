# Flask的session和cookie使用

### 1.Cookie

##### 1.1什么是Cookie

​	什么是cookie?如果单单从数据结构的角度来说,它可以被理解成用来保存数据的一个dictionary,由一组组键值对组成.如果从作用上来说,我们知道Http协议是一种无状态的协议.什么叫无状态呢,就是本次的客户端请求不会保留上一次客户端请求的状态,简单点说就是这样会要求我们每次在浏览器中点开一个网站的链接都会输一次账户和密码.cookie就是用来解决这个问题的.

​        为了解决上述问题,我们第一次登录web服务器,服务端就会在它的响应中的Set-Cookie字段中发送一些键值对,这就包括一个Session ID以及其他一些信息(也包括我们自定义的cookie中的键值对),并告诉客户端在本地缓存这个cookie.然后客户端以后进行链接时每次都会发送这个Session ID,服务器一看是哪个Session ID就知道是哪个客户端发起的链接了,就不会要求我们再次输账户和密码验证了.

​        我们在flask中自定义cookie,实际上就是

在响应Response的Set-Cookie字段中增加我们自定义的键值对.而获取cookie,就是通过请求Request中通过键获取其对应的值

cookie存储的数据量有限，不同的浏览器有不同的存储大小，但一般不超过4KB。因此使用cookie只能存储一些小量的数据。 

1. cookie有有效期：服务器可以设置cookie的有效期，以后浏览器会自动的清除过期的cookie。
2. cookie有域名的概念：只有访问同一个域名，才会把之前相同域名返回的cookie携带给服务器。也就是说，访问谷歌的时候，不会把百度的cookie发送给谷歌。 

##### 1.2 设置Cookie

通过响应对象的set_cookie方法我们可以设置自定义cookie: 

```
设置：set_cookie('key', value, max_ages='', expires='')
```

```
@app.route('/set_cookie')
def set_cookie():
	response = make_response('hello,world');
	response.set_cookie('Name', 'luolin')
	return response
```

我们还可以指定cookie的有效时长,下面的代码把有效时长设置成了30天.通常情况下,我们还可以在浏览器上设置cookie的有效时长,而且浏览器上配置的有效时长优先级要高于我们在代码中设置的. 

```
outdate = datetime.datetime.today() + datetime.timedelta(days=30)
response.set_cookie('Name', 'luolin', expires=outdate)


max_age：以秒为单位，距离现在多少秒后cookie会过期。

expires：为datetime类型。这个时间需要设置为格林尼治时间，也就是要距离北京少8个小时的时间。

如果max_age和expires都设置了，那么这时候以max_age为标准。

max_age在IE8以下的浏览器是不支持的。expires虽然在新版的HTTP协议中是被废弃了，但是到目前为止，所有的浏览器都还是能够支持，所以如果想要兼容IE8以下的浏览器，那么应该使用expires，否则可以使用max_age。

默认的过期时间：如果没有显示的指定过期时间，那么这个cookie将会在浏览器关闭后过期。
```

##### 1.3 获取cookie

 我们可以使用Request对象cookies字段的get方法来获取我们所需要的cookie ,

在每次请求中，url都会向服务器传递Request，在request中可以获取到cookie的信息

```
@app.route('/get_cookie')
def get_cookie():
	name=request.cookie.get('Name')
	return name
```

##### 1.4 删除Cookie

共有三种方法可以删除一个cookie: 

```
	1. 直接清空浏览器的cookie
	2. del_cookie('key') 直接使用del_cookie函数
	3. set_cookie('key','',expires=0) 重新设置key的值为空，过期时间为0
```

例子,设置cookie： 

```
import datetime

@blue.route('/setcookie/')
def set_cookie():
    temp = render_template('index.html')
    response = make_response(temp)
	outdate=datetime.datetime.today() + datetime.timedelta(days=30)
	# 设置cookie中的name的存在时长，设置为30天才过期  
    response.set_cookie('name','cocoococo',expires=outdate)
    return response
```

例子2，删除cookie中的值 

```
@blue.route('/setcookie/')
def set_cookie():
    temp = render_template('index.html')
    response = make_response(temp)
	# 第一种方式，通过set_cookie去删除
    response.set_cookie('name','',expires=0)
	# 第二种方式，del_cookie删除
	response.del_cookie('name')
    return response
```

例子3，获取cookie中的值 

```
@blue.route('/getcookie/')  
def get_cookie():
    name=request.cookies.get('name')  
    return name
```

### 2. Session

#####2.1.1Session的基本概念

​	session和cookie的作用有点类似，都是为了存储用户相关的信息。不同的是，cookie是存储在本地浏览器，session是一个思路、一个概念、一个服务器存储授权信息的解决方案，不同的服务器，不同的框架，不同的语言有不同的实现。虽然实现不一样，但是他们的目的都是服务器为了方便存储数据的。session的出现，是为了解决cookie存储数据不安全的问题的。 

##### 2.1.2 session与cookie的结合使用： 

​	session存储在服务器端：服务器端可以采用mysql、redis、memcached等来存储session信息。原理是，客户端发送验证信息过来（比如用户名和密码），服务器验证成功后，把用户的相关信息存储到session中，然后随机生成一个唯一的session_id，再把这个session_id存储cookie中返回给浏览器。浏览器以后再请求我们服务器的时候，就会把这个session_id自动的发送给服务器，服务器再从cookie中提取session_id，然后从服务器的session容器中找到这个用户的相关信息。这样就可以达到安全识别用户的需求了。 

​	session存储到客户端：原理是，客户端发送验证信息过来（比如用户名和密码）。服务器把相关的验证信息进行一个非常严格和安全的加密方式进行加密，然后再把这个加密后的信息存储到cookie，返回给浏览器。以后浏览器再请求服务器的时候，就会自动的把cookie发送给服务器，服务器拿到cookie后，就从cookie找到加密的那个session信息，然后也可以实现安全识别用户的需求了。 

#####2.2 Session的使用

flask-session是flask框架的session组件，由于原来flask内置session使用签名cookie保存，该组件则将支持session保存到多个地方，如： 

* redis：保存数据的一种工具，五大类型。非关系型数据库
* memcached
* filesystem
* mongodb
* sqlalchmey：那数据存到数据库表里面

##### 2.3 安装

```
pip install flask-session
```

如果指定存session的类型为redis的话，需要安装redis 

````
pip install redis
````

#####2.4使用语法

设置session：

```
session['key'] = value
```

读取session：

```
result = session['key'] ：如果内容不存在，将会报异常

result = session.get('key') ：如果内容不存在，将返回None
```

删除session：

```
session.pop('key')
```

清空session中所有数据：

```
session.clear
```

##### 2.5 应用

一般会使用两种数据库,一种Redis,一种sqlalchemy

**redis**

```
import redis
from flask import Flask, session
from flask_session import Session

app = Flask(__name__)
app.debug = True
app.secret_key = 'xxxx'

app.config['SESSION_TYPE'] = 'redis' # session类型为redis
app.config['SESSION_PERMANENT'] = False # 如果设置为True，则关闭浏览器session就失效。
app.config['SESSION_USE_SIGNER'] = False # 是否对发送到浏览器上session的cookie值进行加密
app.config['SESSION_KEY_PREFIX'] = 'session:' # 保存到session中的值的前缀
app.config['SESSION_REDIS'] = redis.Redis(host='127.0.0.1', port='6379', password='123123') # 用于连接redis的配置
Session(app)


@app.route('/index')
def index():
session['k1'] = 'v1'
return 'xx'


if __name__ == '__main__':
app.run()
```



**sqlalchemy**

```
import redis
from flask import Flask, session
from flask_session import Session as FSession
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.debug = True
app.secret_key = 'xxxx'

# 设置数据库链接
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root:123@127.0.0.1:3306/fssa?charset=utf8'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = True

# 实例化SQLAlchemy
db = SQLAlchemy(app)



app.config['SESSION_TYPE'] = 'sqlalchemy' # session类型为sqlalchemy
app.config['SESSION_SQLALCHEMY'] = db # SQLAlchemy对象
app.config['SESSION_SQLALCHEMY_TABLE'] = 'session' # session要保存的表名称
app.config['SESSION_PERMANENT'] = True # 如果设置为True，则关闭浏览器session就失效。
app.config['SESSION_USE_SIGNER'] = False # 是否对发送到浏览器上session的cookie值进行加密
app.config['SESSION_KEY_PREFIX'] = 'session:' # 保存到session中的值的前缀FSession(app)


@app.route('/index')
def index():

session['k1'] = 'v1'
session['k2'] = 'v1'

return 'xx'


if __name__ == '__main__':
app.run()
```

##### 2.6 使用

我们在初始化文件中创建一个方法，通过调用该方法来获取到Flask的app对象 

```
def create_app():
    app = Flask(__name__)
    # SECRET_KEY 秘钥
    app.config['SECRET_KEY'] = 'secret_key'
	# session类型为redis
    app.config['SESSION_TYPE'] = 'redis'
	# 添加前缀
	app.config['SESSION_KEY_PREFIX'] = 'flask'
    
    # 加载app的第一种方式
    se = Session()
    se.init_app(app=app)
    #加载app的第二种方式
    Session(app=app)
    app.register_blueprint(blueprint=blue)

    return app
```

#####2.7 案例 

定义一个登陆的方法，post请求获取到username，直接写入到redis中，并且在页面中展示出redis中的username

a）需要先启动redis，开启redis-server，使用redis-cli进入客户端

b）定义方法

```
@blue.route('/login/', methods=['GET', 'POST'])
def login():
    if request.method == 'GET':
        username = session.get('username')
        return render_template('login.html', username=username)
    else:
        username = request.form.get('username')
        session['username'] = username

        return redirect(url_for('first.login'))
```

c）定义模板

```
<body>
<h3>欢迎:{{ username }}</h3>
<form action="" method="POST">
    用户名:<input type="text" name="username" placeholder="请输入你的名字">
    <input type="submit" value="提交">
</form>
</body>
```

d）redis中数据 

![flask_session_keys](D:\typora\typro note\图片放置\flask_session_keys.png)

注意：我们在定义app.config的时候指定了SESSION_KEY_PREFIX为flask，表示存在session中的key都会加一个前缀名flask

e) cookie和session的联系![flask_cookie_session](D:\typora\typro note\图片放置\flask_cookie_session.png)



访问者在第一次访问服务器时，服务器在其cookie中设置一个唯一的ID号——会话ID(session)。 这样，访问者后续对服务器的访问头中将自动包含该信息，服务器通过这个ID号，即可区 隔不同的访问者。然后根据不同的访问者来获取其中保存的value值信息。 









































