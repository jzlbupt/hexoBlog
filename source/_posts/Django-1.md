title: Django_FirstApp1
date: 2017-01-08 11:11:08
tags: Django
categories: 技术
---
利用Django搭建Web应用 - Part1 & Part 2

<!--more-->

# virtualenv

- [virtualenv 官网](https://virtualenv.pypa.io/en/stable/userguide/)
- 相关目录：`~/.virtualenvs`
- 启用某一个环境：`source PATH_TO_ENV/bin/activate`, 对于我的Django环境：`source ~/.virtualenvs/djangodev/bin/activate`, 然后命令行会显示：
``` bash
JZL ~/prod/Django $ source ~/.virtualenvs/djangodev/bin/activate
(djangodev) JZL ~/prod/Django $
```
- 停止使用某一个环境：`deactivate`
- 删除一个环境：
```bash
(ENV)$ deactivate
$ rm -r /path/to/ENV
```

我是在djangodev环境下安装的django, 因此可以看到：
```bash
JZL ~/prod/Django $ python -m django --version
/usr/bin/python: No module named django
```
```bash
JZL ~/prod/Django $ source ~/.virtualenvs/djangodev/bin/activate
(djangodev) JZL ~/prod/Django $ python -m django --version
1.11.dev20161217152408
```

# Part 1

## Start a project

- 在code location下输入：`django-admin startproject mysite` (`~/DjangoWorkspace/myFirstApp`)
```bash
(djangodev) JZL ~/DjangoWorkspace/myFirstApp $ django-admin startproject mysite
```
- 有关 python里的 package 描述： [详见官网相关文档](https://docs.python.org/3/tutorial/modules.html#tut-packages)
 - 下面这种形式只能import 某个package或者Module，且引用的时候必须带上全部的路径
``` python
import sound.effects.echo
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
```
 - 另一种引用的方式可以饮用某个package或者module, 也可以是某个module下的具体的方法或者变量
```python
from sound.effects import echo
echo.echofilter(input, output, delay=0.7, atten=4)
```
```python
from sound.effects.echo import echofilter
echofilter(input, output, delay=0.7, atten=4)
```

## Start an app: poll

- 在`manage.py`相同的目录下执行：
```python
python manage.py startapp polls
```
- 在`polls`目录下添加`urls.py`
- 在`mysite`目录下的`urls.py`添加相应的`url`地址

# Part2

## 使用models
- 根据 `mysite/settings.py`里`INSTALLED_APPS`配置的应用列表，在数据库里建立相应的表格以供后续使用：
```bash
(djangodev) JZL ~/DjangoWorkspace/myFirstApp/mysite $ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying sessions.0001_initial... OK
```
- 在polls程序里添加 `Question`和`Choice` model
在 `polls/models.py`里继承`django.db.models`建立两个类
- 激活这个 poll 应用的两个model
同样在`mysite/settings.py`的`INSTALLED_APPS`里添加，找到`polls/apps.py` 对应的类名为 `polls.apps.PollsConfig`
```python
INSTALLED_APPS = [
	'polls.apps.PollsConfig',
    ...
]
```
执行对应的`makemigrattions`操作创建对应的migrations可看到：
```bash
(djangodev) JZL ~/DjangoWorkspace/myFirstApp/mysite $ python manage.py makemigrations polls
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Choice
    - Create model Question
    - Add field question to choice
```
- 然后执行`migrate`操作将变化应用到数据库中去：
```bash
(djangodev) JZL ~/DjangoWorkspace/myFirstApp/mysite $ python manage.py migrateOperations to perform:
  Apply all migrations: admin, auth, contenttypes, polls, sessions
Running migrations:
  Applying polls.0001_initial... OK
```
- 总结起来，一共是三个部分：
 - 修改models (在`models.py`)
 - 执行`makemigrations`为这些变化创建migrations
 - 执行`migration`将这些变化同步到数据库中

## 使用 admin 系统
```bash
(djangodev) JZL ~/DjangoWorkspace/myFirstApp/mysite $ python manage.py createsuperuser
Username (leave blank to use 'jzl'): admin
Email address: jzl_bupt@163.com
Password: ##(Yusheng0924)
Password (again):
Superuser created successfully.
```

- 给poll应用添加admin接口 (在polls/admin.py)
```python
from .models import Question
admin.site.register(Question)
```

