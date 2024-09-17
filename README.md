# JDBCWrapper
> 封装了一些关于数据库的常用操作，以方便程序员使用Java操作数据库而不需记忆SQL语句
## 如何使用
1. 点击上面的"Code",然后选择"Download Zip"
2. 在下载的文件夹中找到你需要的版本所在的文件夹(例如JDBCWrapper-1.0.0)，然后删除你不需要的其它版本
### Intellij Idea
1. 选择File >  Project Structure，然后在左侧找到Project Settings > Libraries
2. 点击左上角的加号，然后选择Java，并选择你需要的版本所在的文件夹(例如JDBCWrapper-1.0.0)
3. 选择该Library添加到的Modules(可选)
4. 连续点击OK直至完成
### Eclipse
1. 右键项目，选择Build Path > Add Libraries，然后选择User Library，再点击Next
2. 为自己的Library起名(例如JDBCWrapper-1.0.0)，然后点击OK
3. 在右侧选择Add JARs，并在弹出窗口中选择你需要的版本所有.jar文件(例如JDBCWrapper-1.0.0.jar和mysql-connector-j-9.0.0.jar)
4. 点击OK完成设置
### 注意
1. 如果你使用的是Intellij Idea，那么添加文件时需添加整个版本文件夹；而如果你使用的是Eclipse，那么添加的则是所有的.jar文件
2. 你不需要额外下载jdbc包，因为该文件夹中已经包含了目前版本的JDBCWrapper所对应的jdbc包
# API
## DatabaseConnection
> 该类封装了一些关于数据库连接的操作
### 构造方法摘要
#### `DatabaseConnection(String url, String user, String password)`
> 构造一个DatabaseConnection对象，并指定其连接的数据库URL，以及用户和密码
### 方法摘要
#### `public Database getDatabase()`
> 获取连接到的Database对象
#### 结果
连接到的Database对象
#### 异常
SQLException
#### 从以下版本开始：
JDBCWrapper-1.0.0

#### `pulic void close()`
> 关闭与数据库的连接
#### 异常
SQLException
## Database
> 该类封装了一些数据库的相关操作
### 构造方法摘要
#### `Database(String name, Statement statement)`
> 使用指定的name和statement获取数据库对象
### 方法摘要
#### `public Table getTable(String name, Statement statement)`
> 使用指定的name和statement获取表对象
#### 参数
name - 指定的表名，必须存在，否则会抛出SQLException

statement - 用于代表该表属于哪个数据库
#### 结果
指定的Table对象
#### 异常
SQLException
#### 从以下版本开始：
JDBCWrapper-1.0.0

#### `public Table createTable(String tableName, int size, String[] columnNames, String[] columnTypes, String[] columnLengths)`
> 使用指定的tableName和字段名、字段类型、字段长度创建表对象
#### 参数
tableName - 要创建的表的名字，其中不要出现中文

size - 表的长度，后面三个String[]必须遵守该长度，短于该长度将会抛出ArrayIndexOutOfBoundsException，超过该长度的部分将被舍弃

columnNames - 要创建的表中的所有字段名称

columnTypes - 所有字段对应的类型

columnLengths - 所有字段对应的长度
#### 结果
创建的Table对象
#### 异常
ArrayIndexOutOfBoundsException,SQLException
#### 从以下版本开始：
JDBCWrapper-1.0.0

(待完善)
