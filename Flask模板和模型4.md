# Flask的模板和模型的使用

### 1. jinja2

Flask中使用jinja2模板引擎

jinja2是由Flask作者开发，模仿Django的模板引擎, 在Jinja中，变量名是由{{ }}来表示的。这种{{ }}语法叫作变量代码块。另外还有用{% %}定义的控制代码块，可以实现一些语言层次的功能，比如循环或者if语句。

优点：

```
速度快，被广泛使用

HTML设计和后端python分离

非常灵活，快速和安全

提供了控制，继承等高级功能
```
### 2. 模板语法

#### 2.1 模板语法主要分为两种：变量和标签

模板中的变量：{{ var }}

```
视图传递给模板的数据

前面定义出来的数据

变量不存在，默认忽略
```

模板中的标签：{% tag %}

```
控制逻辑

使用外部表达式

创建变量

宏定义
```

#### 2.2 结构标签：

block

```
{% block xxx %}

{% endblock %}

块操作
	父模板挖坑，子模板填坑
```

extends

```
{% extends ‘xxx.html’ %}

继承以后保留块中的内容
{{ super() }}
```

挖坑继承体现的化整为零的操作

macro

```
{% macro hello(name) %}

	{{ name }}

{% endmacro %}

宏定义，可以在模板中定义函数，在其他地方调用
```

宏定义可导入

```
{% from 'xxx' import xxx %}
```

例子1：

在index.html中定义macro标签，定义一个方法，然后去调用方法，结果是展示商品的id和商品名称

```
{% macro show_goods(id, name) %}
    商品id：{{ id }}
    商品名称：{{ name }}
{% endmacro %}

{{ show_goods('1', '娃哈哈') }}
<br>
{{ show_goods('2', '雪碧') }}
```

例子2：

在index.html页面中定义一个say()方法，然后解析该方法：

```
{% macro say() %}

    <h3>今天天气气温回升</h3>
    <h3>适合去游泳</h3>
    <h3>适合去郊游</h3>

{% endmacro %}

{{ say() }}
```

例子3：

定义一个function.html中定义一个方法：

```
{% macro create_user(name) %}
    创建了一个用户:{{ name }}
{% endmacro %}
```

在index.html中引入function.html中定义的方法

```
{% from 'functions.html' import create_user %}

{{ create_user('小花') }}
```

#### 2.3 循环

```
{% for item in cols %}

	aa

{% else %}

	bb

{% endfor %}
```

也可以获取循环信息loop

```
loop.first

loop.last

loop.index

loop.revindex
```

例子:

在视图中定义一个视图函数：

```
@stu.route('/scores/')
def scores():

    scores_list = [21,34,32,67,89,43,22,13]

    content_h2 = '<h2>今天你们真帅</h2>'
    content_h3 = '   <h3>今天你们真帅</h3>   '

    return render_template('scores.html',
                           scores=scores_list,
                           content_h2=content_h2,
                           content_h3=content_h3)
```

(该视图函数，在下面讲解的过滤器中任然使用其返回的content_h2等参数)

首先: 在页面中进行解析scores的列表。题目要求：第一个成绩展示为红色，最后一个成绩展示为绿色，其他的不变

```
<ul>
   {% for score in scores %}
        {% if loop.first %}
            <li style="color:red;">{{ loop.revindex }}:{{ loop.index }}:{{ score }}</li>
        {% elif loop.last %}
            <li style="color:green;">{{ loop.revindex }}:{{ loop.index }}:{{ score }}</li>
        {% else %}
            <li> {{ loop.revindex }}:{{ loop.index }}:{{ score }}</li>
        {% endif %}
    {% endfor %}
</ul>
```

#### 2.4 过滤器

语法：

```
{{ 变量|过滤器|过滤器... }}
```

capitalize 单词首字母大写

lower 单词变为小写

upper 单词变为大写

title

trim 去掉字符串的前后的空格

reverse 单词反转

format

striptags 渲染之前，将值中标签去掉

safe 讲样式渲染到页面中

default

last 最后一个字母

first

length

sum

sort

例子：

```
<ul>
    <li>{{ content_h2 }}</li>
    <li>{{ content_h2|safe }}</li>
    <li>{{ content_h2|striptags }}</li>

    <li>{{ content_h3 }}</li>
    <li>{{ content_h3|length }}</li>
    <li>{{ content_h3|trim|safe }}</li>
    <li>{{ content_h3|trim|length }}</li>
</ul>
```

### 3. 定义模板

#### 3.1 定义基础模板base.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>
        {% block title %}
        {% endblock %}
    </title>
    <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>

    {% block extCSS %}
    {% endblock %}
</head>
<body>

{% block header %}
{% endblock %}

{% block content%}
{% endblock %}

{% block footer%}
{% endblock %}

{% block extJS %}
{% endblock %}

</body>
</html>
```

#### 3.2 定义基础模板base_main.html

```
{% extends 'base.html' %}

{% block extCSS %}
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}">
{% endblock %}
```

### 4. 静态文件信息配置

**django**：

第一种方式：

```
{% load static %}
<link rel="stylesheet" href="{% static 'css/index.css' %}">
```

第二种方式：

```
<link rel="stylesheet" href="/static/css/index.css">
```

**flask**：

第一种方式：

```
<link rel="stylesheet" href="/static/css/index.css">
```

第二种方式：

```
<link rel="stylesheet" href="{{ url_for('static', filename='css/index.css') }}">
```

### 5. Flask-SQLAlchemy的使用

##### 5.1 简介

Web 开发中，一个重要的组成部分便是数据库了。Web 程序中最常用的莫过于关系型数据库了，也称 SQL 数据库。另外，文档数据库（如 mongodb）、键值对数据库（如 redis）近几年也逐渐在 web 开发中流行起来，我们习惯把这两种数据库称为 NoSQL 数据库。

大多数的关系型数据库引擎（比如 MySQL、Postgres 和 SQLite）都有对应的 Python 包。在这里，我们不直接使用这些数据库引擎提供的 Python 包，而是使用对象关系映射（Object-Relational Mapper, ORM）框架，它将低层的数据库操作指令抽象成高层的面向对象操作。也就是说，如果我们直接使用数据库引擎，我们就要写 SQL 操作语句，但是，如果我们使用了 ORM 框架，我们对诸如表、文档此类的数据库实体就可以简化成对 Python 对象的操作。

Python 中最广泛使用的 ORM 框架是 [SQLAlchemy](http://www.sqlalchemy.org/)，它是一个很强大的关系型数据库框架，不仅支持高层的 ORM，也支持使用低层的 SQL 操作，另外，它也支持多种数据库引擎，如 MySQL、Postgres 和 SQLite 等。

ORM： 

```
将对对象的操作转换为原生SQL
优点
	易用性，可以有效减少重复SQL
	性能损耗少
	设计灵活，可以轻松实现复杂查询
	移植性好
```

在 Flask-SQLAlchemy 中，数据库使用 URL 指定，下表列出了常见的数据库引擎和对应的 URL。 

| 数据库引擎       | URL                                              |
| ---------------- | ------------------------------------------------ |
| MySQL            | mysql://username:password@hostname/database      |
| Postgres         | postgresql://username:password@hostname/database |
| SQLite (Unix)    | sqlite:////absolute/path/to/database             |
| SQLite (Windows) | sqlite:///c:/absolute/path/to/database           |

​	上面的表格中，username 和 password 表示登录数据库的用户名和密码，hostname 表示 SQL 服务所在的主机，可以是本地主机（localhost）也可以是远程服务器，database 表示要使用的数据库。有一点需要注意的是，SQLite 数据库不需要使用服务器，它使用硬盘上的文件名作为 database。 



##### 5.2创建flask-sqlalchemy数据库

首先，我们使用 pip 安装 Flask-SQLAlchemy: 

```
pip install flask-sqlalchemy
```

安装驱动 

```
pip install pymysql
```

接下来，我们配置一个简单的 SQLite 数据库： 

```
创建models.py文件，其中定义模型

from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()


class Student(db.Model):

    s_id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    s_name = db.Column(db.String(16), unique=True)
    s_age = db.Column(db.Integer, default=1)

    __tablename__ = "student"
    
    # __tablename__是指定创建的数据库的名称
```

其中：

Integer表示创建的s_id字段的类型为整形，

primary_key表示是否为主键

String表示该字段为字符串

unique表示该字段唯一

default表示默认值

autoincrement表示是否自增

1. app 应用配置项 `SQLALCHEMY_DATABASE_URI` 指定了 SQLAlchemy 所要操作的数据库，这里我们使用的是 mysql，数据库 URL 以 `mysql:///` 开头，后面的 `db/stus.db` 表示数据库文件存放在当前目录的 `db` 子目录中的 `stus.db` 文件。当然，你也可以使用绝对路径，如 `/tmp/stus.db` 等。
2. db 对象是 SQLAlchemy 类的实例，表示程序使用的数据库。
3. 我们定义的 `Student` 模型必须继承自 `db.Model`，**这里的模型其实就对应着数据库中的表**。其中，类变量`__tablename__ `定义了在数据库中使用的表名，如果该变量没有被定义，Flask-SQLAlchemy 会使用一个默认名字。

##### 5.3 创建数据表

在视图函数中我们引入models.py中定义的db 

```
from App.models import db

@blue.route("/createdb/")
def create_db():
    db.create_all()
    return "创建成功"

@blue.route('/dropdb/')
def drop_db():
    db.drop_all()
    return '删除成功'
```

##### 5.4 初始化SQLALchemy

在定义的__init__.py文件中使用SQLALchemy去整合一个或多个Flask的应用

有两种方式：

````
第一种：

from flask_sqlalchemy import SQLALchemy

app = Flask(__name__)
db = SQLAlchemy(app)
````

````
第二种：

from App.models import db

def create_app():
    app = Flask(__name__)
    db.init_app(app)
    return app
````

#####5.5 配置数据库的访问地址

[官网配置参数](http://www.pythondoc.com/flask-sqlalchemy/config.html)

数据库连接的格式：

```
dialect+driver://username:password@host:port/database

dialect数据库实现

driver数据库的驱动
```

例子： 访问mysql数据库，驱动为pymysql，用户为root，密码为123456，数据库的地址为本地，端口为3306，数据库名称HelloFlask

设置如下： "mysql+pymysql://root:123456@localhost:3306/HelloFlask"

在初始化__init__.py文件中如下配置：

```
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

app.config['SQLALCHEMY_DATABASE_URI'] = "mysql+pymysql://root:123456@localhost:3306/HelloFlask"
```

### 6. 对学生数据进行CRUD操作

语法：

```
类名.query.xxx
```

获取查询集：

```
all()

filter(类名.属性名==xxx)

filter_by(属性名=xxx)
```

数据操作：

```
在事务中处理，数据插入

db.session.add(object)

db.session.add_all(list[object])

db.session.delete(object)

db.session.commit()

修改和删除基于查询
```

#### 6.1 想学生表中添加数据

```
@blue.route('/createstu/')
def create_stu():

    s = Student()
    s.s_name = '小花%d' % random.randrange(100)
    s.s_age = '%d' % random.randrange(30)

    db.session.add(s)
    db.session.commit()

    return '添加成功'
```

提交事务，使用commit提交我们的添加数据的操作

#### 6.2 获取所有学生信息

将学生的全部信息获取到，并且返回给页面，在页面中使用for循环去解析即可

```
@blue.route("/getstudents/")
def get_students():
    students = Student.query.all()
    return render_template("StudentList.html", students=students)
```

#### 6.3 获取s_id=1的学生的信息

写法1：

```
students = Student.query.filter(Student.s_id==1)
```

写法2：

```
students = Student.query.filter_by(s_id=2)
```

注意：filter中可以接多个过滤条件

写法3：

```
sql = 'select * from student where s_id=1'
students = db.session.execute(sql)
```

#### 6.4 修改学生的信息

写法1：

```
students = Student.query.filter_by(s_id=3).first()
students.s_name = '哈哈'
db.session.commit()
```

写法2：

```
Student.query.filter_by(s_id=3).update({'s_name':'娃哈哈'})

db.session.commit()
```

#### 6.5 删除一个学生的信息

写法1：

```
students = Student.query.filter_by(s_id=2).first()
db.session.delete(students)
db.session.commit()
```

写法2：

```
students = Student.query.filter_by(s_id=1).all()
db.session.delete(students[0])
db.session.commit()
```

注意：filter_by后的结果是一个list的结果集

**重点注意：在增删改中如果不commit的话，数据库中的数据并不会更新，只会修改本地缓存中的数据，所以一定需要db.session.commit()**