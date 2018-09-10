# Flask使用

### 1. Flask的介绍

1.flask是一个基于Python实现的web开发的 ‘微’ 框架

* 微框架中的“微”意味着 Flask 旨在保持核心简单而易于扩展。Flask 不会替你做出太多决策——比如使用何种数据库。而那些 Flask 所选择的——比如使用何种模板引擎——则很容易替换。 

[可以参见中文文档地址](http://docs.jinkan.org/docs/flask/) 

2.Flask和Django一样，也是一个基于MVC设计模式的Web框架 

Flask流行的主要原因： 

````

- 有非常齐全的官方文档，上手非常方便。

- 有非常好的拓展机制和第三方的拓展环境，工作中常见的软件都有对应的拓展，自己动手实现拓展也很容易

- 微型框架的形式给了开发者更大的选择空间

````

### 2. 安装Flask

Flask 依赖两个外部库：[Werkzeug](http://werkzeug.pocoo.org/) 和 [Jinja2](http://jinja.pocoo.org/2/) 。 Werkzeug 是一个 WSGI（在 Web 应用和多种服务器之间的标准 Python 接口) 工具集。Jinja2 负责渲染模板。 如何在你的电脑上安装这一切 ？最强大的方式是 virtualenv ， 

#####2.1虚拟环境搭建

```
virtualenv --no-site-packages falskenv

激活windows下虚拟环境
cd Scripts
activate
```

#####2.2 安装

```
pip install flask
```

#####2.3 专业版pycharm的flask安装

专业版的pycharm直接创建项目时指定flask，选定虚拟环境的地址即可。



### 3.flask的最小应用

创建manage.py文件(manage的名字可以使用其他的名字或者类似的名字代替)

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
	return 'Hello World'

if __name__ == '__main__':

	app.run()
```

运行指令：python manage.py

关闭服务器指令：Ctrl+C。

```
结果：
Running on http://127.0.0.1:5000/
```

* 现在访问 <http://127.0.0.1:5000/> ，会看见 Hello World 问候。 

那这段代码代表什么意思呢？ 

1. 首先，我们导入了 [`Flask`](http://docs.jinkan.org/docs/flask/api.html#flask.Flask) 类。这个类的实例将会是我们的 WSGI 应用程序。
2. 接下来，我们创建一个该类的实例，第一个参数是应用模块或者包的名称。 如果你使用单一的模块（如本例），你应该使用 `__name__ `，因为模块的名称将会因其作为单独应用启动还是作为模块导入而有不同（ 也即是 `__main__` 或实际的导入名）。这是必须的，这样 Flask 才知道到哪去找模板、静态文件等等。详情见 [`Flask`](http://docs.jinkan.org/docs/flask/api.html#flask.Flask)的文档。
3. 然后，我们使用 [`route()`](http://docs.jinkan.org/docs/flask/api.html#flask.Flask.route) 装饰器告诉 Flask 什么样的URL 能触发我们的函数。
4. 这个函数的名字也在生成 URL 时被特定的函数采用，这个函数返回我们想要显示在用户浏览器中的信息。
5. 最后我们用 [`run()`](http://docs.jinkan.org/docs/flask/api.html#flask.Flask.run) 函数来让应用运行在本地服务器上。 其中 `if __name__ =='__main__':` 确保服务器只会在该脚本被 Python 解释器直接执行的时候才会运行，而不是作为模块导入的时候。

##### 3.1进行初始化

```
from flask import Flask

app = Flask(__name__)
```

Flask类构造函数唯一需要的参数就是应用程序的主模块或包。对于大多数应用程序，Python的__name__变量就是那个正确的、你需要传递的值。Flask使用这个参数来确定应用程序的根目录，这样以后可以相对这个路径来找到资源文件.

##### 3.2设置路由

```
@app.route('/')
```

客户端例如web浏览器发送 请求 给web服务，进而将它们发送给Flask应用程序实例。应用程序实例需要知道对于各个URL请求需要运行哪些代码，所以它给Python函数建立了一个URLs映射。这些在URL和函数之间建立联系的操作被称之为 路由 。

在Flask应程序中定义路由的最便捷的方式是通过显示定义在应用程序实例之上的app.route装饰器，注册被装饰的函数来作为一个 **路由**。

##### 3.3 编辑视图函数

在上一个示例给应用程序的根URL注册gello_world()函数作为事件的处理程序。如果这个应用程序被部署在服务器上并绑定了 [www.example.com](http://www.example.com/) 域名，然后在你的浏览器地址栏中输入 [http://www.example.com](http://www.example.com/) 将触发gello_world()来运行服务。客户端接收到的这个函数的返回值被称为 响应 。如果客户端是web浏览器，响应则是显示给用户的文档。

类似于gello_world()的函数被称作 **视图函数** 

##### 3.4 动态名称组件路由

你的Facebook个人信息页的URL是 <http://www.facebook.com/> ，所以你的用户名是它的一部分。Flask在路由装饰器中使用特殊的语法支持这些类型的URLs。下面的示例定义了一个拥有动态名称组件的路由： 

```
@app.route('/hello/<name>')

def gello_world(name):

	return 'Hello World %s' % name
```

用尖括号括起来的部分是动态的部分，所以任何URLs匹配到静态部分都将映射到这个路由。当视图函数被调用，Flask发送动态组件作为一个参数。在前面的示例的视图函数中，这个参数是用于生成一个个性的问候作为响应。

在路由中动态组件默认为字符串，但是可以定义为其他类型。例如，路由/user/int:id只匹配有一个整数在id动态段的URLs。Flask路由支持int、float

如下：

```
@app.route('/hello/<int:id>')

def gello_stu_id(id):

  return 'Hello World id: %s' % id
```

##### 3.5启动服务

```
if __name__ == '__main__':

	app.run()
```

注意： __name__ == '__main__'在此处使用是用于确保web服务已经启动当脚本被立即执行。当脚本被另一个脚本导入，它被看做父脚本将启动不同的服务，所以app.run()调用会被跳过。

一旦服务启动，它将进入循环等待请求并为之服务。这个循环持续到应用程序停止，例如通过按下Ctrl-C。

有几个选项参数可以给app.run()配置web服务的操作模式。在开发期间，可以很方便的开启debug模式，将激活 debugger 和 reloader 。这样做是通过传递debug为True来实现的。

run()中参数有如下：

````
debug 是否开启调试模式，开启后修改python的代码会自动重启

port 启动指定服务器的端口号

host主机，默认是127.0.0.1
````

#### 注意：

尽管交互式调试器在允许 fork 的环境中无法正常使用（也即在生产服务器上正常使用几乎是不可能的），但它依然允许执行任意代码。这使它成为一个巨大的安全隐患，因此它 **绝对不能用于生产环境** 。 

### 4. 修改启动方式，使用命令行参数启动服务

##### 4.1安装插件

```
pip install flask-script
```

##### 4.2启动命令

```
python manage.py runserver -h 地址 -p 端口 -d -r
```

其中：-h表示地址。-p表示端口。-d表示debug模式。-r表示自动重启 

### 5.蓝图的使用

##### 5.1蓝图的作用

在Flask项目中可以用Blueprint(蓝图)实现模块化的应用，使用蓝图可以让应用层次更清晰，开发者更容易去维护和开发项目。蓝图将作用于相同的URL前缀的请求地址，将具有相同前缀的请求都放在一个模块中，这样查找问题，一看路由就很快的可以找到对应的视图，并解决问题了。 

##### 5.2 安装蓝图

```
pip install flask_blueprint
```

#####5.3引入Blueprint模块

```
app_blueprint = Blueprint('first', __name__)

*  first 相当于一个Django的namepace
```

注意：Blueprint中传入了两个参数，第一个first是蓝图的名称，相当于一个Django的namepace, 第二个是蓝图所在的包或模块，\_\_name\_\_代表当前模块名或者包名 

##### 5.4将路由注册到app上面

```
app = Flask(__name__)

app.register_blueprint(app_blueprint, url_prefix='/app')
```

注意：第一个参数即我们定义初始化定义的蓝图对象，第二个参数url_prefix表示该蓝图下，所有的url请求必须以/app开始。这样对一个模块的url可以很好的进行统一管理 

### 6.URL变量规则

##### 6.1 route路由规则

要给 URL 添加变量部分，你可以把这些特殊的字段标记为 `<variable_name>` ， 这个部分将会作为命名参数传递到你的函数。规则可以用 `<converter:variable_name>` 指定一个可选的转换器。 

写法：<converter:variable_name >

converter类型： 

````
string 字符串

int 整形

float 浮点型

path 接受路径，接收的时候是str，/也当做字符串的一个字符

uuid 只接受uuid字符串

any 可以同时指定多种路径，进行限定

````

例如:

```
@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return 'User %s' % username

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return 'Post %d' % post_id
```

注意:`<int:post_id>`代表给网络路由传递的参数，在`<username>`中可以不用写`<string:username>`，因为默认就是一个str类型 

例如:

```
@app.route('/helloint/<int:id>/')

@app.route('/getfloat/<float:price>/')

@app.route('/getstr/<string:name>/'，methods=['GET', 'POST'])

@app.route('/getpath/<path:url_path>/')

@app.route('/getbyuuid/<uuid:uu>/'，methods=['GET', 'POST'])
```

实现对应的视图函数:

```
@blue.route('/hello/<name>/')
def hello_man(name):
    print(type(name))
    return 'hello name:%s type:%s' % (name, type(name))

@blue.route('/helloint/<int:id>/')
def hello_int(id):
    print(id)
    print(type(id))
    return 'hello int: %s' % (id)

@blue.route('/index/')
def index():
    return render_template('hello.html')

@blue.route('/getfloat/<float:price>/')
def hello_float(price):

    return 'float: %s' % price

@blue.route('/getstr/<string:name>/')
def hello_name(name):

    return 'hello name: %s' % name

@blue.route('/getpath/<path:url_path>/')
def hello_path(url_path):

    return 'path: %s' % url_path

@blue.route('/getuuid/')
def gello_get_uuid():
    a = uuid.uuid4()
    return str(a)

@blue.route('/getbyuuid/<uuid:uu>/')
def hello_uuid(uu):

    return 'uu:%s' % uu
```

#####6.2 methods请求方法

HTTP （与 Web 应用会话的协议）有许多不同的访问 URL 方法。默认情况下，路由只回应 GET 请求，但是通过 [`route()`](http://docs.jinkan.org/docs/flask/api.html#flask.Flask.route) 装饰器传递 methods 参数可以改变这个行为。 

例如:

```
@app_blueprint.route('/post_name', methods=['POST', 'GET', 'PUT'])
def post_name():
    return '我是一个超级帅的帅哥'
```

注意 : 不管请求的类型数量为多少个,methods都必须加上s,表示复数

常见的HTTP方法： 

```
GET : 浏览器告知服务器：只 获取 页面上的信息并发给我。这是最常用的方法。

POST : 浏览器告诉服务器：想在 URL 上 发布 新信息。并且，服务器必须确保 数据	  已存储且仅存储一次。这		是 HTML 表单通常发送数据到服务器的方法。

PUT : 类似 POST 但是服务器可能触发了存储过程多次，多次覆盖掉旧值。你可 能	 会问这有什么用，当然这是有原		 因的。考虑到传输中连接可能会丢失，在 这种 	 情况下浏览器和服务器之间的系统可能安全地第二次接收请		  求，而 不破坏其它	东西。因为 POST 它只触发一次，所以用 POST 是不可能的。

DELETE : 删除给定位置的信息。

OPTIONS : 给客户端提供一个敏捷的途径来弄清这个URL支持哪些 HTTP 方法.从Flask0.6开始，实现了自动处理。
```

### 7.请求request

服务端在接收到客户端的请求后，会自动创建Request对象,由Flask框架创建，Request对象不可修改.

属性： 

````
url：完整的请求地址

base_url：去掉GET参数的url

host_url：只有主机和端口号的url

path：路由中的路径

method：请求方法

remote_addr：请求的客户端的地址

args：GET请求参数

form：POST请求参数

files：文件上传

headers：请求头

cookies：请求中的cookie
````

#####7.1 args-->GET请求参数包装

a）args是get请求参数的包装，args是一个ImmutableMultiDict对象，类字典结构对象

b）数据存储也是key-value

#####7.2 form-->POST请求参数包装

a）form是post请求参数的包装，args是一个ImmutableMultiDict对象，类字典结构对象

b）数据存储也是key-value

重点：ImmutableMultiDict是类似字典的数据结构，但是与字典的区别是，可以存在相同的键。

在ImmutableMultiDict中获取数据的方式，dict['key']或者dict.get('key')或者dict.getlist('key')

##### 7.3 响应Response

注意:响应response是由开发者自己创建的

创建方法： 

```
from flask import make_response

make_response创建一个响应，是一个真正的Response对象
```

状态码：

格式：make_reponse(data，code)，其中data是返回的数据内容，code是状态码

```
a）直接将内容当做make_response的第一个参数，第二个参数直接写返回的状态码

b）直接在render后加返回的状态码
```

例子1：

定义一个获取GET请求的request的方法，并将返回成功的请求的状态码修改为200

```
@blue.route('/getrequest/', methods=['GET'])
def get_request():

    print(request)

    return '获取request', 200
```

例子2：

返回response响应，并添加返回结果的状态码200

```
@blue.route('/getresponse/')
def get_response():
    response = make_response('<h2>我是响应</h2>', 500)
    return response
```

或者：

```
@blue.route('/getresponse/', methods=['GET'])
def get_user_response():
    login_html = render_template('login.html')
    res = make_response(login_html, 200)
    return res
```

