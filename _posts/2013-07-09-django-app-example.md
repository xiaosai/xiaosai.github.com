---
layout: default
title: "django 实例"
category: "python"
tags: ["python", "django"]
---
<h2>{{ page.title }}</h2>
<h3>1. 创建一个应用模块</h3>
<pre>
	<code>
		python manage.py startapp report
	</code>
</pre>
<p>得到文件目录结构如下：</p>
<pre>
	<code>
report/
     __init__.py
     admin.py
     models.py
     tests.py
     views.py
    </code>
</pre>

<h3>2. 连接数据库</h3>
<p>
修改 mysite/settings.py 文件中 <strong>DATABASES</strong> 对象，加入数据库引擎（例如mysql为：django.db.backends.mysql），名称、用户名、密码等。
</p>

<h3>3. 设置页面和方法对应关系</h3>
<p>
修改 mysite/urls.py 文件中 urlpatterns 对象，加入页面、地址对应关系，如：
</p>
<pre>
	<code>
import report.views as report 
url(r'^report/contract$', report.contract)
	</code>
</pre>

<h3>4. 设置数据模型 models.py</h3>
<p>
比如 contract 如下：
</p>
<pre>
	<code>
class Contract(models.Model):
    id = models.CharField(max_length=36, primary_key=True)
    contract_num = models.CharField(max_length=30)
    contract_name = models.CharField(max_length=255)
     class Meta:  # 自定义表名
            db_table = "contract"
	</code>
</pre>

{% include JB/setup %}