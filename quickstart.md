# 安装使用hunt
## step 1 安装dmd和dub等环境

###### 进入[Dlang官网](http://dlang.org/download.html)有详细安装说明,或者直接执行如下安装脚本.

#### ` curl -fsS https://dlang.org/install.sh | bash -s dmd`

## step 2 创建基于hunt的应用

###### 使用dub 创建一个新的项目【hello-dlang】脚本如下。
```
git clone https://github.com/huntlabs/hunt-skeleton.git myproject
cd myproject
dub run
```
###### 编辑dub.json文件，在dependencies中添加hunt的依赖
```
"hunt": "~>0.8.5"
```

## step 3 编译运行 

```
dub run
```

## 更多的使用请参考 hunt example样例

