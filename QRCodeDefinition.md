# 概述 #
  * 使用CSV来表示类似数据库的结构化数据

# 规则 #
  * 文件编码：UTF-8
  * 文件格式：用一个被方括号包含的字符串表示表名，后面紧接着定义数据列的名称。接下来每一行表示一条数据记录：
```
[TableName1]ColumnName1,ColumnName2,...\n   
ColumnData1,ColumnData2,...\n 
...
[TableName2]ColumnName1,ColumnName2,...\n   
ColumnData1,ColumnData2,...\n 
...
```
  * 转义：按下列规则对每个字段中的数据进行转义

| 转义字符 | 实际字符 |
|:-------------|:-------------|
| `\\` | `\` |
| `\,` | `,` |
| `\[` | `[` |
| `\]` | `]` |

  * 注意：
    1. 逗号后面不要有空格
    1. 行末不要有多余的逗号
    1. 不支持用“`#`”表示注释

# 样例 #
```
[Group]Name
清华常用
[Members]Name,PhoneNumber,Extra
张三,13911111111,这是一列为未来留的数据（没用）
李四\[班长\],13900000000,这是一列为未来留的数据（没用）
王\,五,13999999999,这人偏要在名字里加逗号
```

# 接口建议 #
  * 一个最General的接口可以考虑设计成这样（仅供参考）
```
interface DataRow
{
    String getField(String columnName);
    void setField(String columnName, String value);
}
interface DataTable
{
    String getName();
    void setName(String name);
    DataRow getDataRow(int index);
    void insertDataRow(int index);
    void removeDataRow(int index);
    Iterable<DataRow> getAllRows();
}
interface DataSet
{
    DataTable getDataTable(String dataTableName);
    void insertDataTable(DataTable table);
    void removeDataTable(DataTable table);
}
```