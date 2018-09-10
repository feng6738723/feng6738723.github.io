# Django的登录/注册

### 1 .自定义的身份验证

 通过cookie和token去实现登录功能，用户在登录账号以后，随机产生一个随机数并存在cookie中，并在服务端也存储同一个数在数据库中。 当下一次url请求过来的时候，解析request中绑定的cookie信息，解锁出之前存的随机数，判断该随机数是否是存储在服务器端的数据，如果 没有查询到则表示该cookie过期，或者该cookie是伪造的，或者服务器上存储该信息的数据缓存到期被清空了。则该提示用户重新登录，并且 重新产生随机数，并存储在cookie中以及服务端，以保证下次请求和响应能够顺利。 

#### 1. 注册方法

从页面中获取账号和密码，进行创建 

```
from django.contrib.auth.hashers import make_password, check_password

def my_register(request):

    if request.method == 'GET':
        return render(request, 'register.html')
    if request.method == 'POST':
    # get到的属性值必须同HTML中的名字相同
        username = request.POST.get('username')
        password = request.POST.get('password')
        
 # make_password 进行密码的加密操作
        password = make_password(password)

        MyUser.objects.create(username=username, password=password)

        return HttpResponseRedirect(reverse('a:my_login'))
        
        
```

#### 2. 登录，并且绑定参数到cookie上

先检验用户名是否在数据库中，如果查询到则继续验证密码, 如果密码验证对，则绑定一个参数到cookie中。 解析密码，加密密码来源与一下的模块:

```
from django.contrib.auth.hashers import make_password, check_password


def my_login(request):
    if request.method == 'GET':
        return render(request, 'login.html')

    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
  # 验证用户是否存在
        if MyUser.objects.filter(username=username).exists():
            user = MyUser.objects.get(username=username)
  # check_password 检验密码是否与数据库中密码是否一致
            if check_password(password, user.password):
  # 在客户端cookie中保存一个session id(ticket)值
                res = HttpResponseRedirect(reverse('a:index'))
  # max_age=10 代表存活时间10秒 expires 代表天的时间
                ticket = get_ticket()
   # 设置cookie的值
                res.set_cookie('ticket', ticket, max_age=10 )
  # 在服务端存同样的一个session id(ticket)值
                user.ticket = ticket
                user.save()
                return res
            else:
                return HttpResponseRedirect(reverse('a:my_login'))
        else:
            return HttpResponseRedirect(reverse('a:index'))

```



### 3. 验证用户是否是登录状态

##### 3.1定义一个中间件类函数

目的是是一个轻量级的，底层的插件，可以介入Django的请求和响应的过程 

中间件的本质就是一个python类 

##### 1.3 自定义中间件流程

1. 在工程目录下创建middleware目录
2. 目录中创建一个python文件
3. 在根据功能需求，创建切入需求类，重写切入点方法
4. 启动中间件，在settings中进行配置，MIDDLEWARE中添加middleware.文件名.类名 

```
from django.core.urlresolvers import reverse

from django.http import HttpResponseRedirect

from django.utils.deprecation import MiddlewareMixin

from app.models import MyUser


class UserMiddleware(MiddlewareMixin):

    def process_request(self, request):
        # 定义中间件
        # 过滤登录界面和注册界面，免得一直重复进入登录页面
        path = ['/app/my_login/', '/app/my_register/']
        # 不经过验证
        if request.path in path:
            return None
     # 获取cookie中绑定的参数，进行数据库中的查询，进行匹配
        ticket = request.COOKIES.get('ticket')
        if ticket:
            user = MyUser.objects.filter(ticket=ticket).first()
            if user:
                request.user = user
                return None
            else:
                return HttpResponseRedirect(reverse('a:my_login'))
        else:
            return HttpResponseRedirect(reverse('a:my_login'))
```

```
settings.py

'utils.UserAuthMiddleware.UserMiddleware',
```



![django_middleware_user_auth](C:\Users\44903\Desktop\Django学习\django_middleware_user_auth.png)





#### 4. 通过定义装饰器去验证用户是否是登录状态，如果不是，则跳转到登录

也可以选择使用装饰器函数来验证登录但是方法比较繁琐，需要每个页面添加装饰器

![django_is_login](C:\Users\44903\Desktop\Django学习\django_is_login.png)

### 5. 注销登录

方式是删除cookie中的认证令牌



```
def logout(request):
    # 注销
    if request.method == 'GET':
        res = HttpResponseRedirect(reverse('a:login'))
        res.delete_cookie('ticket')
        return res
```

