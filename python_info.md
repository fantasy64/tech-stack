#python常用知识

函数参数前面加* 和** 的作用
当函数要接受元组或者字典参数时，它分别使用 * 和 ** 前缀。
在变量前加 *，则多余的函数参数会作为一个元组存在args中，如：
```python
def func(*ages):

func(1,2,3)  #args表示（1，2，3）这个元组
```
如果使用 ** 前缀，多余的参数会被认为是字典
```python
def func(**args):

func(a='1',b='2',c ='3') #args表示{‘a’:'1','b':'2','c':'3'}
```

python mysql操作的几大组件
MySqLDB
MySQL-python 又叫 MySQLdb，是 Python 连接 MySQL 最流行的一个驱动，很多框架都也是基于此库进行开发，遗憾的是它只支持 Python2.x，而且安装的时候有很多前置条件，因为它是基于C开发的库，在 Windows 平台安装非常不友好，经常出现失败的情况，现在基本不推荐使用，取代的是它的衍生版本。
MySqLDB在python3里面不支持，但是可以用 mysqlclient 代替

mysqlclient
由于 MySQL-python 年久失修，后来出现了它的 Fork 版本 mysqlclient，完全兼容 MySQLdb，同时支持 Python3.x

PyMySQL
PyMySQL 是纯 Python 实现的驱动，速度上比不上 MySQLdb，最大的特点可能就是它的安装方式没那么繁琐，同时也兼容 MySQL-python

mysql-connector
mysql-connector是一个Python模块，它在Python中重新实现MySQL协议，它比较慢，但不需要C库，因此更便携。