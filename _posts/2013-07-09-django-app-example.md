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

{% include JB/setup %}