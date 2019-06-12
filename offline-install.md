# 安装

## 联机安装
$ pip install superset

## 脱机安装

### 联机环境下下载安装包

#### 安装pip2pi

$ pip install pip2pi

#### 下载安装包

$ pip2tgz superset_lib/ --no-binary=:all: -r superset_lib/requirements_nobinary.txt 

#### 更新索引

$ dir2pi superset_lib/

#### 下载Skeleton
$ git clone https://github.com/dpgaspar/Flask-AppBuilder-Skeleton.git

#### 压缩lib

$ tar zcfv superset_lib.tar.gz superset_lib/
$ tar zcfv Flask-AppBuilder-Skeleton.tar.gz Flask-AppBuilder-Skeleton/

#### 上传目标服务器

$ scp superset_lib.tar.gz root@ip:/target_dir
$ scp Flask-AppBuilder-Skeleton.tar.gz root@ip:/target_dir

#### 解压文件

$ tar xzvf  superset_lib.tar.gz
$ tar xzvf  Flask-AppBuilder-Skeleton.tar.gz
$ mv Flask-AppBuilder-Skeleton superset

#### 安装superset

pip install --no-index --find-links=file:///opt/superset_lib/  superset

# 联机创建app（脱机情况下可以直接跳过）
$ superset fab create-app --name superset --engine SQLAlchemy

# 创建管理员账号
$ superset fab create-admin

# 初始化数据库
$ superset db upgrade

# 加载示例数据
$ superset load_examples

# 创建角色权限
$ superset init

# 启动服务
$ superset runserver -d

# 异常的处理
* 在执行指令的时候Was unable to import superset Error: cannot import name '_maybe_box_datetimelike' from 'pandas.core.common'
是因为pandas版本高，可以卸载panda 0.24.2 安装0.23.4
```commandline
$ pip uninstall panda
$ pip install panda==0.23.4
```
* 执行superset db upgrade指令时报sqlalchemy.exc.InvalidRequestError: Can't determine which FROM clause to join from, there are multiple FROMS which can join to this entity. Try adding an explicit ON clause to help resolve the ambiguity.
是因为SQLAlchemy版本高

```commandline
$ pip list | grep -i sqlalchemy
    Flask-SQLAlchemy       2.4.0   
    marshmallow-sqlalchemy 0.16.3  
    SQLAlchemy             1.3.3   
    SQLAlchemy-Utils       0.33.11

```
```commandline
$ pip uninstall SQLAlchemy
```
然后
```commandline
$ pip install SQLAlchemy==1.2.18
```

# 离线安装报错
* 安装cryptography报错
```commandline
ERROR: Complete output from command /opt/venv/bin/python3 /opt/venv/lib/python3.7/site-packages/pip install --ignore-installed --no-user --prefix /tmp/pip-build-env-j_5h0ysq/overlay --no-warn-script-location --no-binary :none: --only-binary :none: --no-index --find-links file:///opt/superset_lib/ -- 'setuptools>=18.5' wheel 'cffi>=1.7,!=1.11.3; python_implementation != '"'"'PyPy'"'"'':
  ERROR: Looking in links: file:///opt/superset_lib/
  Collecting setuptools>=18.5
  Collecting wheel
    ERROR: Could not find a version that satisfies the requirement wheel (from versions: none)
  ERROR: No matching distribution found for wheel
  ----------------------------------------
ERROR: Command "/opt/venv/bin/python3 /opt/venv/lib/python3.7/site-packages/pip install --ignore-installed --no-user --prefix /tmp/pip-build-env-j_5h0ysq/overlay --no-warn-script-location --no-binary :none: --only-binary :none: --no-index --find-links file:///opt/superset_lib/ -- 'setuptools>=18.5' wheel 'cffi>=1.7,!=1.11.3; python_implementation != '"'"'PyPy'"'"''" failed with error code 1 in None

```

* 安装SQLAlchemy报错
```commandline
ERROR: Could not find a version that satisfies the requirement Flask-SQLAlchemy<3,>=2.4 (from flask-appbuilder>=1.12.1->superset) (from versions: 2.3.2)
ERROR: No matching distribution found for Flask-SQLAlchemy<3,>=2.4 (from flask-appbuilder>=1.12.1->superset)

```


* 安装pyhs2过程中报错
```commandline
ERROR: Complete output from command /opt/venv/bin/python3 -u -c 'import setuptools, tokenize;__file__='"'"'/tmp/pip-install-o532mpvp/sasl/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record /tmp/pip-record-s37zb9in/install-record.txt --single-version-externally-managed --compile --install-headers /opt/venv/include/site/python3.7/sasl:
    ERROR: running install
    running build
    running build_py
    creating build
    creating build/lib.linux-x86_64-3.7
    creating build/lib.linux-x86_64-3.7/sasl
    copying sasl/__init__.py -> build/lib.linux-x86_64-3.7/sasl
    running egg_info
    writing sasl.egg-info/PKG-INFO
    writing dependency_links to sasl.egg-info/dependency_links.txt
    writing requirements to sasl.egg-info/requires.txt
    writing top-level names to sasl.egg-info/top_level.txt
    reading manifest file 'sasl.egg-info/SOURCES.txt'
    reading manifest template 'MANIFEST.in'
    writing manifest file 'sasl.egg-info/SOURCES.txt'
    copying sasl/saslwrapper.cpp -> build/lib.linux-x86_64-3.7/sasl
    copying sasl/saslwrapper.h -> build/lib.linux-x86_64-3.7/sasl
    copying sasl/saslwrapper.pyx -> build/lib.linux-x86_64-3.7/sasl
    running build_ext
    building 'sasl.saslwrapper' extension
    creating build/temp.linux-x86_64-3.7
    creating build/temp.linux-x86_64-3.7/sasl
    gcc -pthread -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -fPIC -Isasl -I/usr/local/include/python3.7m -c sasl/saslwrapper.cpp -o build/temp.linux-x86_64-3.7/sasl/saslwrapper.o
    In file included from sasl/saslwrapper.cpp:254:0:
    sasl/saslwrapper.h:22:23: 致命错误：sasl/sasl.h：没有那个文件或目录
     #include <sasl/sasl.h>
                           ^
    编译中断。
    error: command 'gcc' failed with exit status 1
    ----------------------------------------
ERROR: Command "/opt/venv/bin/python3 -u -c 'import setuptools, tokenize;__file__='"'"'/tmp/pip-install-o532mpvp/sasl/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record /tmp/pip-record-s37zb9in/install-record.txt --single-version-externally-managed --compile --install-headers /opt/venv/include/site/python3.7/sasl" failed with error code 1 in /tmp/pip-install-o532mpvp/sasl/

```
```commandline
$ yum install cyrus-sasl-lib.x86_64 cyrus-sasl-devel.x86_64 libgsasl-devel.x86_64 -y

```


* 运行superset报numpy.ufunc

```commandline
Traceback (most recent call last):
  File "/opt/venv/bin/superset", line 6, in <module>
    from superset.cli import create_app
  File "/opt/venv/lib/python3.7/site-packages/superset/__init__.py", line 16, in <module>
    from superset import config, utils
  File "/opt/venv/lib/python3.7/site-packages/superset/utils.py", line 30, in <module>
    import pandas as pd
  File "/opt/venv/lib/python3.7/site-packages/pandas/__init__.py", line 26, in <module>
    from pandas._libs import (hashtable as _hashtable,
  File "/opt/venv/lib/python3.7/site-packages/pandas/_libs/__init__.py", line 4, in <module>
    from .tslib import iNaT, NaT, Timestamp, Timedelta, OutOfBoundsDatetime
  File "__init__.pxd", line 872, in init pandas._libs.tslib
ValueError: numpy.ufunc has the wrong size, try recompiling. Expected 192, got 216

```
升级numpy
```commandline
$ pip uninstall numpy
$ pip install numpy

```
* 运行superset报no pysqlite2、pysqlite3

```commandline
Traceback (most recent call last):
  File "/opt/venv/lib/python3.7/site-packages/sqlalchemy/dialects/sqlite/pysqlite.py", line 338, in dbapi
    from pysqlite2 import dbapi2 as sqlite
ModuleNotFoundError: No module named 'pysqlite2'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/venv/bin/superset", line 6, in <module>
    from superset.cli import create_app
  File "/opt/venv/lib/python3.7/site-packages/superset/__init__.py", line 115, in <module>
    utils.pessimistic_connection_handling(db.engine)
  File "/opt/venv/lib/python3.7/site-packages/flask_sqlalchemy/__init__.py", line 937, in engine
    return self.get_engine()
  File "/opt/venv/lib/python3.7/site-packages/flask_sqlalchemy/__init__.py", line 956, in get_engine
    return connector.get_engine()
  File "/opt/venv/lib/python3.7/site-packages/flask_sqlalchemy/__init__.py", line 561, in get_engine
    self._engine = rv = self._sa.create_engine(sa_url, options)
  File "/opt/venv/lib/python3.7/site-packages/flask_sqlalchemy/__init__.py", line 966, in create_engine
    return sqlalchemy.create_engine(sa_url, **engine_opts)
  File "/opt/venv/lib/python3.7/site-packages/sqlalchemy/engine/__init__.py", line 431, in create_engine
    return strategy.create(*args, **kwargs)
  File "/opt/venv/lib/python3.7/site-packages/sqlalchemy/engine/strategies.py", line 87, in create
    dbapi = dialect_cls.dbapi(**dbapi_args)
  File "/opt/venv/lib/python3.7/site-packages/sqlalchemy/dialects/sqlite/pysqlite.py", line 343, in dbapi
    raise e
  File "/opt/venv/lib/python3.7/site-packages/sqlalchemy/dialects/sqlite/pysqlite.py", line 341, in dbapi
    from sqlite3 import dbapi2 as sqlite  # try 2.5+ stdlib name.
  File "/usr/local/lib/python3.7/sqlite3/__init__.py", line 23, in <module>
    from sqlite3.dbapi2 import *
  File "/usr/local/lib/python3.7/sqlite3/dbapi2.py", line 27, in <module>
    from _sqlite3 import *
ModuleNotFoundError: No module named '_sqlite3'
```
```
$ yum install sqlite-devel -y
```
然后重新编译安装python

* 执行superset fab create-app --name superset --engine SQLAlchemy
```commandline
Something went wrong <urlopen error [Errno 110] Connection timed out>
Try downloading from https://github.com/dpgaspar/Flask-AppBuilder-Skeleton/archive/master.zip
```
# 使用
执行superset --help可查看支持的指令
