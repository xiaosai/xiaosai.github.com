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

<h3>5. 设置页面模板地址</h3>
<p>
在 mysite/setting.py 文件下修改对象，如下：
</p>
<pre>
	<code>
TEMPLATE_DIRS = (
    '/Users/saiyongzhang/WorkSpace/python/mysite/template',
)
	</code>
</pre>

<h3>6. 页面report/views.py</h3>
<pre>
	<code>
def contract(request) :
    ct = Contract.objects.get(id = '0e3305a9-e219-11e2-95cc-00222822153f')
    return render_to_response('report/contract_list.html', {'contract': ct})
	</code>
</pre>

<h3>7. 编写页面 </h3>
<p>
template/report/contract_list.html如下：
</p>
<pre>
	<code>
		{ % extends "base.html" %}
		{ % block title %}合同列表{ % endblock %}
		{ % block content %}
		&lt;p&gt;contractId:{ {contract.id}}&lt;/p&gt;
		{ % endblock %}
	</code>
</pre>
<p>
template/base.html 如下：
</p>
<pre>
	<code>
		&lt;!DOCTYPE&nbsp;HTML&nbsp;PUBLIC&nbsp;&quot;-//W3C//DTD&nbsp;HTML&nbsp;4.01//EN&quot;&gt;
		&lt;html&gt;
		&lt;head&gt;
		&nbsp;&nbsp;&nbsp;&nbsp;&lt;title&gt;{&nbsp;%&nbsp;block&nbsp;title&nbsp;%}{&nbsp;%&nbsp;endblock&nbsp;%}&lt;/title&gt;
		&lt;/head&gt;
		&lt;body&gt;
		&nbsp;&nbsp;&nbsp;&nbsp;&lt;h1&gt;我的报表工具&lt;/h1&gt;
		&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;%&nbsp;block&nbsp;content&nbsp;%}{&nbsp;%&nbsp;endblock&nbsp;%}
		&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;%&nbsp;block&nbsp;footer&nbsp;%}
		&nbsp;&nbsp;&nbsp;&nbsp;&lt;hr&gt;
		&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;Thanks&nbsp;for&nbsp;visiting&nbsp;my&nbsp;site.&lt;/p&gt;
		&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;%&nbsp;endblock&nbsp;%}
		&lt;/body&gt;
		&lt;/html&gt;
	</code>
</pre>
<h3>8. 浏览器输入<a target="_blank"  href="http://localhost:8000/report/contract">http://localhost:8000/report/contract</a></h3>
<img src="http://i1333.photobucket.com/albums/w631/zhangsaiyong/ct-list_zps7d76391b.png?t=1373357165"/>

<p>{{ page.date | date_to_string }}</p>

