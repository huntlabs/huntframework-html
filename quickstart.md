安装使用hunt
=====

安装dmd和dub等环境
-----

进入[Dlang官网](http://dlang.org/download.html)有详细安装说明,或者linux环境下直接执行如下安装脚本.

` curl -fsS https://dlang.org/install.sh | bash -s dmd`

创建dub项目
-----

使用dub 创建一个新的项目
```
mkdir myproject
cd myproject
dub init
```

编辑dub.json文件，在dependencies中添加hunt的依赖
-----
```
"targetType": "executable",
"dependencies": {
	"hunt": "~>0.8.8"					    
},
```

编辑source/app.d文件,添加如下代码
-----

```
import hunt;

void main()
{
	auto app = Application.getInstance();

	app.GET("/index",function(Request req){
		Response res = req.createResponse();
		res.html("hello world");
		res.done();
	});
			    
	app.run(parseAddress("0.0.0.0",8088));
}
```

编辑source/app.d文件,添加如下代码
-----

执行 `dub run` 命令编译代码,然后在浏览器中打开 `http://127.0.0.1:8088/index` 看见hello world 便表示运行成功


