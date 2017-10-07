HTTP 视图
=====

视图是使用D模板来实现的,所以编译完成后,后续每次请求都只是调用编译好的方法.

基本用法
-----
修改`dub.json`,添加如下代码
```
"stringImportPaths": ["./resources/views",]
```
添加模板文件目录
```
website
  config
  source
  resources
    views
```

添加一个简单的视图文件`resources/views/index.html`

```
hello, {{ var.name }}
```

在控制器中使用视图文件,并传递参数
```
@Action
void index()
{
	view.name = "world";
	view.render!"index.html"();
}
```

视图嵌套
-----
在实际开发中,一个web站点,header和footer可能是不更改的,更新的只是content部分

我们可以使用如下方法,做到视图嵌套

首先定义框架页面 `resources/views/main.html`
```
<html>
{{ render!"header.html"}}
{{ yield }}
{{ render!"footer.html"}}
</html>
```

接着定义header和footer页面

`resources/views/header.html`
```
here is header html 
```
`resources/views/footer.html`
```
here is footer html 
```

然后定义content页面

`resources/views/content.html`
```
here is body html {{ var.name }}
```

最后在控制器中使用这几个页面
```
view.name = " world ";
view.setLayout!"main.html"();
view.render!"content.html"();
```

视图标签
-----
现在有如下三种标签
- {{ }} 输出标签,用在视图中显示内容,标签内的语句,返回值一定要是string类型的
- {% %} 控制标签,可以在标签内实现判断,循环等控制,语法和d的语法一样
- {{ yield }} 模板嵌套标签,用在模板嵌套时
