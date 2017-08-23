---
layout: post
title: Django
date: 2017-08-23 10:56:24.000000000 +09:00
---
create submit
django-admin.py startproject submit

创立一个templates 文件夹用于保存html文件
mkdir templates

创立一个app userinfo 用于处理用户登录注册
python3 manage.py startapp userinfo
进入配置文件 导入app userinfo逻辑处理层

vim submit/urls
from django.conf.urls import patterns, include, url
from django.contrib import admin
from userinfo import views
urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'submit.views.home', name='home'),
    # url(r'^blog/', include('blog.urls')),
    #url(r'^admin/', include(admin.site.urls)),
    url(r'register',views.register),
)
patterns是一个元组 要打逗号 r正则表达式 views.register调用
views类下的register方法
vim /userinfo/views

from django.shortcuts import render
# Create your views here.

def register(request):
    return render(request,"register.html")

render用于跳转到一个静态页面 ，还可以添加一些数据

进入 setting.py
加入TEMPLATE_DIRS=(os.path.join(BASE_DIR,'templates'),)
用于告诉系统 我的html文件放于哪里

如何使用静态文件？如css js img
在末尾加上
STATICFILES_DIRS=(
    os.path.join(BASE_DIR,'templates'),
)
然后调用静态文件的时候 加上/static/前缀

进入setting。py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',        #MySQL数据库
        'NAME': 'spring',                             #库名
        'USER': 'root',                              #用户名
        'PASSWORD': '123123',                      #密码
        'HOST':'localhost',
        'PORT':'3306',
    }
}

配置好数据库信息  但是centos7里面因为mariadb问题 我们还需要在
对应 app的__init__.py加入这两行代码
import pymysql
pymysql.install_as_MySQLdb()

vim /app/models


from django.db import models

# Create your models here.
class UserInfo(models.Model):
    user=models.CharField(max_length=32)
    pwd=models.CharField(max_length=32)
~            
配置数据表 id会自动创立

vim /submit/setting.py

INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'userinfo'
)

将app放入 才能创建model

vim registe.html

action="/sys-register"

vim /submit/urls

将action加入  导向 views






