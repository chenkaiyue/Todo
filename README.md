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


#### 4.坑爹的地方[解决安装flask-mongoengine](http://stackoverflow.com/questions/18958508/sslerror-the-read-operation-timed-out-when-using-pip)
```shell
pip --default-timeout=100 install flask-mongoengine
```