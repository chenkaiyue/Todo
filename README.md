Todo
======

a todo web app use python2.7 based on flask and mongodb

### Enviroment: `macOX`,`python2.7`

#### 1.事前准备
```shell
brew install python
```

```shell
pip install flask
```

```shell
pip install flask-mongoengine
```

```shell
pip install flask-script
```


#### 2.单元测试(python2)自带
```shell
python -m unittest discover
```


#### 3.覆盖
```shell
pip install coverage
```
>* 3.1 测试覆盖
```shell
coverage run -m unittest discover
```
>* 3.2 查看覆盖率
```shell
coverage report
```

#### 4.部署web服务器
```shell
pip install gunicorn
```
```shell
gunicorn -b 127.0.0.1:8080 run:app
```

#### 5.部署代码
>* 5.1 [nginx使用](http://arccode.net/2015/02/27/Nginx%E9%85%8D%E7%BD%AE%E5%B0%8F%E8%AE%B0/)
```shell
brew install nginx
```
nginx配置
```shell
cd /usr/local/etc/nginx
mkdir conf.d
vim /usr/local/etc/nginx/nginx.conf
```

在nginx.conf中进行修改, 大致配置可如下
```shell
user  your_username staff;
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    include conf.d/*.conf;
}
```




```shell
gunicorn -b 127.0.0.1:8080 run:app
```
>* 5.2 supervisor[mac版部署](http://liyangliang.me/posts/2015/06/using-supervisor/)
copy他的代码,貌似里面的`;`是注解,记得要打开。
拷贝`supervisord.conf` 到 `/etc/supervisord.conf`,
拷贝`todo.conf` 到 `/etc/supervisor/conf.d/todo.conf`。

查看 supervisord 是否在运行：
```shell
ps aux | grep supervisord
```

```shell
supervisorctl -c /etc/supervisord.conf
```
上面这个命令会进入 supervisorctl 的 shell 界面，然后可以执行不同的命令了：
```shell
> status    # 查看程序状态
> stop usercenter   # 关闭 usercenter 程序
> start usercenter  # 启动 usercenter 程序
> restart usercenter    # 重启 usercenter 程序
> reread    ＃ 读取有更新（增加）的配置文件，不会启动新添加的程序
> update    ＃ 重启配置文件修改过的程序
```

```shell
[include]
files = /etc/supervisor/*.conf
```


## 后记

注意:
附件都放在`other_configuration`文件夹里

参考:
[Nginx配置小记](http://arccode.net/2015/02/27/Nginx%E9%85%8D%E7%BD%AE%E5%B0%8F%E8%AE%B0/)
supervisor[mac版部署](http://liyangliang.me/posts/2015/06/using-supervisor/)


#### 坑爹的地方[解决安装flask-mongoengine](http://stackoverflow.com/questions/18958508/sslerror-the-read-operation-timed-out-when-using-pip)
```shell
pip --default-timeout=100 install flask-mongoengine
```