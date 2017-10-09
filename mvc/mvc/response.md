HTTP 响应
=====

设置http头
-----
```
response.setHeader("Content-Type","text/html");
```

设置http body
-----
```
response.setContext("hello world");
```

设置http 状态码
-----
```
response.setHttpStatusCode(200);
```

发送json
-----
```
JSONValue json;
response.json(json);
response.json(json.toString);
```

发送html
-----
```
response.html("hello world");
```

发送plain
-----
```
response.plain("plain");
```

发送文件
-----
```
response.download(string filename,ubyte[] file);
```

设置cookie
-----
```
response.setCookie(string name, string value, int expires = 0, string path = "/", string domain = null);
```

发送数据
```
response.done();
```
