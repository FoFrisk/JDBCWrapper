# JDBCWrapper

> 封装了一些关于数据库的常用操作，以方便程序员使用Java操作数据库而不需记忆SQL语句

## 如何使用

1. 点击上面的"Code",然后选择"Download Zip"
2. 在下载的文件夹中找到你需要的版本所在的文件夹(例如JDBCWrapper-1.1.1)，然后删除你不需要的其它版本

### Intellij Idea

1. 选择File >  Project Structure，然后在左侧找到Project Settings > Libraries
2. 点击左上角的加号，然后选择Java，并选择你需要的版本所在的文件夹(例如JDBCWrapper-1.1.1)
3. 选择该Library添加到的Modules(可选)
4. 连续点击OK直至完成

### Eclipse

1. 右键项目，选择Build Path > Add Libraries，然后选择User Library，再点击Next
2. 为自己的Library起名(例如JDBCWrapper-1.1.1)，然后点击OK
3. 在右侧选择Add JARs，并在弹出窗口中选择你需要的版本所有.jar文件(例如JDBCWrapper-1.1.1.jar和mysql-connector-j-9.0.0.jar)
4. 点击OK完成设置

### 注意

1. 如果你使用的是Intellij Idea，那么添加文件时需添加整个版本文件夹；而如果你使用的是Eclipse，那么添加的则是所有的.jar文件
2. 你不需要额外下载jdbc包，因为该文件夹中已经包含了目前版本的JDBCWrapper所对应的jdbc包

# API

## class DatabaseConnection

> 该类封装了一些关于数据库连接的操作

### 构造方法摘要

`DatabaseConnection(String url, String user, String password)`

> 构造一个DatabaseConnection对象，并指定其连接的数据库URL，以及用户和密码

### 方法摘要

`public Database getDatabase() throws SQLException`

> 获取连接到的Database对象

`pulic void close() throws SQLException`

> 关闭与数据库的连接

## class Database

> 该类封装了一些数据库的相关操作

### 构造方法摘要

`Database(String name, Statement statement)`

> 使用指定的name和statement获取Database对象

### 方法摘要

`public Table getTable(String name, Statement statement)`

> 使用指定的name和statement获取Table对象

- 参数<br>
  name - 指定的表名，必须存在，否则会抛出SQLException<br>
  statement - 用于代表该表属于哪个数据库
```
@Deprecated
public Table createTable(String tableName, int size, String[] fieldNames, String[] fieldTypes, String[] fieldLengths) throws SQLException
```

> 使用`create table`命令创建指定名称、字段名、字段类型、字段长度的Table对象，该方法于1.1.0版本后被标记为过时

- 参数<br>
  tableName - 要创建的表的名字，其中不要出现中文<br>
  size - 表的长度，后面三个String[]
  必须遵守该长度，短于该长度将会抛出ArrayIndexOutOfBoundsException，超过该长度的部分将被舍弃<br>
  fieldNames - 要创建的表中的所有字段名称，1.1.0以前被命名为columnNames<br>
  fieldTypes - 所有字段对应的类型，1.1.0以前被命名为columnTypes<br>
  fieldLengths - 所有字段对应的长度，1.1.0以前被命名为columnLengths

`public Table createTable(String tableName, FieldList fieldList) throws SQLException`

> 使用`create table`命令创建字段列表为fieldList的Table对象，该方法添加于1.1.0版本

- 参数<br>
  tableName - 要创建的表的名字，其中不要出现中文<br>
  fieldList - 指定的字段列表

`public void chooseDatabase(String name) throws SQLException`

> 使用`use`命令选择指定名称的数据库

- 参数<br>
  name - 指定的数据库名称，必须存在，否则会抛出SQLException

`public static void createDatabase(String name) throws SQLException`

> 使用`create database`命令创建指定名称的数据库，默认字符集utf8，该方法于1.1.1版本后添加了static修饰符

- 参数<br>
  name - 要创建的数据库的名称，不要出现中文

`public static void createDatabase(String name, String charset) throws SQLException`

> 使用`create database`命令创建指定名称的数据库，可设置字符集，该方法于1.1.1版本后添加了static修饰符

- 参数<br>
  name - 要创建的数据库的名称，不要出现中文<br>
  charset - 要创建的数据库的字符集，如utf8,gbk等

`public static void deleteDatabase(String name) throws SQLException`

> 使用`drop database`命令删除指定名称的数据库，该方法于1.1.1版本后添加了static修饰符

- 参数<br>
  name - 要删除的数据库的名称

`public static void showDatabases() throws SQLException`

> 使用`show databases`命令输出所有数据库名称，该方法于1.1.1版本后添加了static修饰符

`public void showTables() throws SQLException`

> 使用`show tables`命令输出目前选中的数据库中的所有表格名称

## class Table

> 该类封装了一些表的相关操作

### 构造方法摘要

`Table(String name, Statement statement)`

> 使用指定的name和statement获取Table对象

### 方法摘要

`public void describeTable() throws SQLException`

> 使用`desc`命令描述表

`public void deleteTable() throws SQLException`

> 使用`drop table`命令删除当前表格

`public void addColumn(String columnName, String columnType, String columnLength) throws SQLException`

> 使用`alter table`命令为当前表格添加列

- 参数<br>
  columnName - 要添加的列的名称<br>
  columnType - 要添加的列每个值的类型<br>
  columnLength - 要添加的列每个值的长度

`public void deleteColumn(String columnName) throws SQLException`

> 使用`alter table`命令为当前表格删除指定的列

- 参数<br>
  columnName - 要删除的列的名称

`public void add(Object... values) throws SQLException`

> 使用`insert into`命令向当前表格中添加数据，1.1.0版本后支持使用`"default"`将插入数据的某个字段设置为默认值

- 参数<br>
  values - 要添加的数据，必须与表格创建时的每个字段类型、长度相对应，否则会抛出SQLException

`public void delete(String condition) throws SQLException`

> 使用`delete from`命令删除符合指定条件的数据

- 参数<br>
  condition - 指定的条件，如id=1

`public void update(String condition, String fieldName, Object value) throws SQLException`

> 使用`update`命令修改符合指定条件的数据

- 参数<br>
  condition - 指定的条件，如id=1<br>
  fieldName - 要修改的字段的名称，必须存在，否则会抛出SQLException<br>
  value - 要修改成的值，必须符合创建时的类型和长度，否则会抛出SQLException

`public ResultSet search(boolean isOutput) throws SQLException`

> 使用`select`命令搜索表，默认搜索整张表

- 参数<br>
  columnName - 选中的列名，在1.0.0版本中为fieldName，该参数仅存在于1.1.1版本以前<br>
  isOutput - true则会将结果输出在控制台，反之亦然

`public ResultSet search(String columnName, String condition, boolean isOutput) throws SQLException`

> 使用`select`命令搜索表，可指定搜索条件，如要搜索整张表，则令condition为`"true"`(1.1.0版本以前为`null`)即可

- 参数<br>
  columnName - 选中的列名，在1.0.0版本中为fieldName<br>
  condition - 指定的条件，如id=1<br>
  isOutput - true则会将结果输出在控制台，反之亦然

## class FieldList

> 该类用于规范化创建Table对象时传入的字段列表，该类添加于1.1.0版本

### 方法摘要

`public void addPrimaryField(String fieldName, String fieldType, String fieldLength)`

> 向FieldList对象中添加指定fieldName, fieldType和fieldLength的主键字段

- 参数<br>
  fieldName - 要添加的字段的名称，不允许重复，否则会抛出SQLException<br>
  fieldType - 要添加的字段的类型<br>
  fieldLength - 要添加的字段的长度

`public void addField(String fieldName, String fieldType, String fieldLength)`

> 向FieldList对象中添加指定fieldName, fieldType和fieldLength的普通字段，默认值为null，不具有任何约束

- 参数<br>
  fieldName - 要添加的字段的名称，不允许重复，否则会抛出SQLException<br>
  fieldType - 要添加的字段的类型<br>
  fieldLength - 要添加的字段的长度

`public void addField(String fieldName, String fieldType, String fieldLength, Object defaultValue, boolean isNotNull, boolean isUnique)`

> 向FieldList对象中添加指定fieldName, fieldType和fieldLength的字段，可设置默认值、是否具有非空约束和唯一约束

- 参数<br>
  fieldName - 要添加的字段的名称，不允许重复，否则会抛出SQLException<br>
  fieldType - 要添加的字段的类型<br>
  fieldLength - 要添加的字段的长度<br>
  defaultValue - 该字段的默认值<br>
  isNotNull - 用于设置该字段是否具有非空约束<br>
  isUnique - 用于设置该字段是否具有唯一约束

`public int size()`

> 获取该FieldList对象中具有字段的数量

## interface TablePrintStream

> 该接口用于将指定的ResultSet对象使用表格输出，目前若使用中文，则会出现表格无法对齐的问题，该接口在1.0.0版本中为类

### 方法摘要

`private static void printLine(int[] maxLengths)`

> 使用指定的每一列的最大长度输出分割线

- 参数<br>
  maxLengths - 每一列的最大长度

`private static void printRows(ResultSet resultSet, int[] maxLengths) throws SQLException`

> 使用每一列的最大长度以表格形式输出指定的ResultSet对象中的每一行数据

- 参数<br>
  resultSet - 要输出的内容<br>
  maxLengths - 每一列的最大长度

`public static void printTable(ResultSet resultSet, String... titles) throws SQLException`

> 使用指定的标题以表格形式输出ResultSet对象中的所有数据

- 参数<br>
  resultSet - 要输出的内容<br>
  titles - 要输出的表格每一列的标题
