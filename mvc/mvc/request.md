HTTP 请求
=====

获取GET参数
-----
```
auto id = request.get("id");
auto id = request.get("id",null);//没有则返回默认值
```

获取POST参数
-----
```
auto id = request.post("id");
auto id = request.post("id",null);//没有则返回默认值
```

获取JSON参数
-----
获取http content-type 为application/json 的请求的json 数据
```
auto body = request.json();
```
获取某个key的数据
```
auto id = request.json!long("id");
```
获取HTTP HEADER参数
-----
```
auto key = request.header("key");
```

获取上传文件
-----
```
auto file = request.file("filename");
if(file is null)writeln("file not exist");
```

cookie操作
-----
返回cookie对象
```
auto id = request.getCookie("id");
```
返回cookie值
```
auto id = request.getCookieValue("id");
```

session操作
-----
返回session对象
```
auto id = request.getSession();
```

获取请求body
-----
```
auto body = request.Body();
```
