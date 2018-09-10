#Flask的models与一对多关系 

```
- 深入数据库的增删改查，查询数据filter和filter_by
- 运算符--contains、startswith、__gt__等
- 筛选--offset、limit、get、first、paginate等
- 逻辑运算符--and_、or_、not_
- 模型之间的一对多的关联关系的定义
```

###1. 数据库的深入操作(增删改查)

定义模型，并定义初始化的函数：

```
class Student(db.Model):

    s_id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    s_name = db.Column(db.String(16), unique=True)
    s_age = db.Column(db.Integer, default=1)

    __tablename__ = "student"

    def __init__(self, name='', age=''):
        self.s_name = name
        self.s_age = age
```

#### 1.1 增--批量增加

第一种方式：

```
@blue.route('/createstus/')
def create_users():
    stus = []
    for i in range(5):
		# 实例化Student的对象
        s = Student()
		# 对象的属性赋值
        s.s_name = '张三%s' % random.randrange(10000)
        s.s_age = '%d' % random.randrange(100)
        stus.append(s)
	# 添加需要创建的数据
    db.session.add_all(stus)
	# 提交事务到数据库
    db.session.commit()

    return '创建成功'
```

注：在创建单条数据的时候使用db.session.add()，在创建多条数据的时候使用db.session.add_all()

第二种方式：

```
@blue.route('/createstus/')
def create_users():
    stus = []
    for i in range(5):
		# 使用类的初始化去创建Student对象
        s = Student('张三%s' % random.randrange(10000),
                    '%d' % random.randrange(100))
        stus.append(s)

    db.session.add_all(stus)
    db.session.commit()

    return '创建成功'
    
    
    
@app_blue.route('/create_init_stu/', methods=['GET', 'POST'])
def create_init_stu():
    for i in range(10):
        # 第一个参数i代表名字的编号, 第二个参数的i代表年龄
        stu = Student('美女%s' % i, age=i)
        stu.save_update()
    return '批量创建成功'
```

#### 1.2 查--使用运算符

######1.2.1获取查询集

```
filter(类名.属性名.运算符(‘xxx’))

filter(类名.属性 数学运算符  值)
```

######1.2.2运算符：

```
contains： 包含
startswith：以什么开始
endswith：以什么结束
in_：在范围内
like：模糊
__gt__: 大于
__ge__：大于等于
__lt__：小于
__le__：小于等于
```

######1.2.3筛选：

```
offset()

limit()

order_by()

get()

first()

paginate()
```

######1.2.4逻辑运算：

```
与
	and_
	filter(and_(条件),条件…)

或
	or_
	filter(or_(条件),条件…)

非
	not_
	filter(not_(条件),条件…)
```

例子1：

1. 查询学生的id为3，4，5，6，16的的学生信息，使用**in_逻辑运算**

   ```
    @blue.route('/getstubyids/')
    def get_stu_by_ids():
   
    	students = Student.query.filter(Student.s_id.in_([3,4,5,6,16]))
    	return render_template('StudentList.html', students=students)
   ```

2. 查询学生的年龄小于18岁的学生的信息

   ```
    Student.query.filter(Student.s_age < 18)
   ```

3. 查询学生的年龄小于18岁的学生的信息，**__lt__小于**

   ```
    students = Student.query.filter(Student.s_age.__lt__(15))
   ```

4. 查询学生的年龄小于等于18岁的学生的信息，**__le__小于等于**

   ```
    students = Student.query.filter(Student.s_age.__le__(15))
   ```

5. 查询学生的姓名以什么开始或者以什么结尾的学生的信息**startswith和endswith**

   ```
    students = Student.query.filter(Student.s_name.startswith('张'))
    students = Student.query.filter(Student.s_name.endswith('2'))
   ```

6. 查询id=4的学生的信息

   ```
    Student.query.get(4)
    获取的结果是学生的对象
   ```

7. 模糊搜索like

   ```
    %：代表一个或者多个
    _：代表一个
    
    Student.query.filter(Student.s_name.like('%张%')) 
   ```

8. 分页，查询第二页的数据4条

   ```
    第一个参数是那一页，第二个参数是一页的条数，第三个参数是是否输出错误信息
    students = Student.query.paginate(2, 4, False).items
   ```

例子2：

跳过offset几个信息，截取limit结果的几个值

```
# 按照id降序排列
stus = Student.query.order_by('-s_id')

# 按照id降序获取三个
stus = Student.query.order_by('-s_id').limit(3)

# 获取年龄最大的一个
stus = Student.query.order_by('-s_age').first()

# 跳过3个数据，查询5个信息
stus = Student.query.order_by('-s_age').offset(3).limit(5)

# 跳过3个数据
stus = Student.query.order_by('-s_age').offset(3)

# 获取id等于24的学生
stus = Student.query.filter(Student.s_id==24)
stus = Student.query.get(24)
```

例子3：

1. 查询

   from sqlalchemy import and_, or_, not_

   **查询多个条件**

   stus = Student.query.filter(Student.s_age==18, Student.s_name=='雅典娜')

   **and_ 并且条件**

   stus = Student.query.filter(and_(Student.s_age==18, Student.s_name=='雅典娜'))

   **or_ 或者条件**

   stus = Student.query.filter(or_(Student.s_age==18, Student.s_name=='火神'))

   **not_ 非**

   stus = Student.query.filter(not_(Student.s_age==18), Student.s_name=='火神')

#### 1.3分页显示

![flask_sqlalchemy_paginate](D:\typora\typro note\图片放置\flask_sqlalchemy_paginate.png)

后端数据处理：

```
# 查询第几页的数据	
page = int(request.args.get('page', 1))

# 每一页的条数多少，默认为10条
per_page = int(request.args.get('per_page', 10))

# 查询当前第几个的多少条数据
paginate = Student.query.order_by('-s_id').paginate(page, per_page, error_out=False)

stus = paginate.items
```

前端数据展示：

```
{% extends 'base.html' %}


{% block content %}
    <table>
        <tr>
            <th>姓名</th>
            <th>年龄</th>
            <th>班级</th>
            <th>操作</th>
        </tr>
        {% for stu in stus %}
            <tr>

                <td>{{ stu.id }}</td>
                <td>{{ stu.s_name }}</td>
                <td>{{ stu.s_age }}</td>
                <td>{{ stu.grade.g_name}}</td>
                <td>
                    <a href="/app/stu_add_grade/{{ stu.id }}">添加班级</a>
                </td>
            </tr>
        {% endfor %}
    </table>

        总页数: {{ paginate.pages }}
        <br>
        <!--进行分页的展示-->
        {% if paginate.has_prev %}
            <a href="/app/selstu/?page={{ paginate.prev_num }}">上一页</a>
        {% endif %}

        <!--使用循环展示中间的页数码-->
        {% for i in paginate.iter_pages() %}
            <a href="/app/selstu/?page={{ i }}">{{ i }}</a>
        {% endfor %}


        {% if paginate.has_next %}
            <a href="/app/selstu/?page={{ paginate.next_num }}">下一页</a>
        {% endif %}
        <br>
        当前页数: {{ paginate.page}}
{% endblock %}
```

### 2. 关联关系

#### 2.1 一对多建立模型

学生模型：

```
class Student(db.Model):

    s_id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    s_name = db.Column(db.String(20), unique=True)
    s_age = db.Column(db.Integer, default=18)
    s_g = db.Column(db.Integer, db.ForeignKey('grade.g_id'), nullable=True)

    __tablename__ = 'student'
```

班级模型：

```
class Grade(db.Model):

    g_id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    g_name = db.Column(db.String(10), unique=True)
    g_desc = db.Column(db.String(100), nullable=True)
    g_time = db.Column(db.Date, default=datetime.now)
    students = db.relationship('Student', backref='stu', lazy=True)

    __tablename__ = 'grade'
```

官网解释有如下几个lazy的参数：

lazy 决定了 SQLAlchemy 什么时候从数据库中加载数据:，有如下四个值:

**select**/True: (which is the default) means that SQLAlchemy will load the data as necessary in one go using a standard select statement.

**joined**/False: tells SQLAlchemy to load the relationship in the same query as the parent using a JOIN statement.

**subquery**: works like ‘joined’ but instead SQLAlchemy will use a subquery.

**dynamic**: is special and useful if you have many items. Instead of loading the items SQLAlchemy will return another query object which you can further refine before loading the items. This is usually what you want if you expect more than a handful of items for this relationship

```
那么 backref 和 lazy 意味着什么了？backref 是一个在 Address 类上声明新属性的简单方法。您也可以使用 my_address.person 来获取使用该地址(address)的人(person)。lazy 决定了 SQLAlchemy 什么时候从数据库中加载数据:

'select' (默认值) 就是说 SQLAlchemy 会使用一个标准的 select 语句必要时一次加载数据。
'joined' 告诉 SQLAlchemy 使用 JOIN 语句作为父级在同一查询中来加载关系。
'subquery' 类似 'joined' ，但是 SQLAlchemy 会使用子查询。
'dynamic' 在有多条数据的时候是特别有用的。不是直接加载这些数据，SQLAlchemy 会返回一个查询对象，在加载数据前您可以过滤（提取）它们。
```

#### 2.2 查询对象之间的关联关系

1. 通过班级查询学生信息

   ```
    @grade.route('/selectstubygrade/<int:id>/')
    
    def select_stu_by_grade(id):
        grade = Grade.query.get(id)
    	# 通过班级对象.定义的relationship变量去获取学生的信息
        stus = grade.students
    
        return render_template('grade_student.html',
                               stus=stus,
                               grade=grade
                               )
   ```

2. 通过学生信息查询班级信息

   ```
    @stu.route('/selectgradebystu/<int:id>/')
   
    def select_grade_by_stu(id):
   
        stu = Student.query.get(id)
    	# 通过学生对象.定义的backref参数去获取班级的信息
        grade = stu.stu
    
        return render_template('student_grade.html',
                               grade=grade,
                               stu=stu)
   ```

注意：表的外键由db.ForeignKey指定，传入的参数是表的字段。db.relations它声明的属性不作为表字段，第一个参数是关联类的名字，backref是一个反向身份的代理,相当于在Student类中添加了stu的属性。例如，有Grade实例dept和Student实例stu。dept.students.count()将会返回学院学生人数;stu.stu.first()将会返回学生的学院信息的Grade类实例。一般来讲db.relationship()会放在一这一边。