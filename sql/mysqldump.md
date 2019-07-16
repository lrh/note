
# mysqldump 常用方法

1. 获取一个完整备份
    ```bash
    # 不锁库备份
    mysqldump -uusername -p --triggers --routines --events -A -B --single-transaction --master-data=2 > backup.$(date +%F).sql
    ```

2. 导出指定库
    ```bash
    mysqldump -uusername -p -B dbname > backup.$(date +%F).sql
    # 如果是导出单库也可以不使用-B 参数，无非就是没有创建库的语句。
    # 如果是多个库可以使用如下命令，但是必须使用-B参数
    mysqldump -uusername -p -B DB1 DB2 DB3 > backup.$(date +%F).sql
    ```

3. 导出指定表的数据和结构
    ```bash
    mysqldump -uusername -p DBNAME table1 table2 > tablename.sql
    # 或者使用 –tables 参数
    mysqldump -uusername -p --tables DBNAME table1 table2 > backup.$(date +%F).sql  
    # 或者
    mysqldump  -uusername -p DBNAME  --tables table1 table2 table3 > tablename.sql
    ```

4. 导出指定表的结构
    ```bash
    # 不包含数据
    mysqldump -ubackup -p --no-data  DBNAME table1 table2 > backup.$(date +%F).sql
    # 或者使用–tables参数
    mysqldump -ubackup -p --no-data DBNAME  --tables table1 table2 > backup.$(date +%F).sql
    # 或者
    mysqldump -ubackup -p --no-data  --tables DBNAME table1 table2 > backup.$(date +%F).sql
    ```

5. 导出指定表的数据
    ```bash
    # 不包含表结构
    mysqldump  -uusername -p --no-create-info DBNAME  table1 table2 table3 > backup.$(date +%F).sql
    # 或者使用–tables 参数
    mysqldump  -uusername -p --no-create-info DBNAME --tables table1 table2 table3 > backup.$(date +%F).sql
    # 或者
    mysqldump  -uusername -p --no-create-info  --tables DBNAME table1 table2 table3 > backup.$(date +%F).sql
    ```

6. 导出整个数据库结构 (包括表结构,不包含数据)
    ```bash
    mysqldump -uusername -p --no-data DBNAME > backup.$(date +%F).sql
    ```

7. 导出数据库表结构和数据时排除某些表
    ```bash
    # 使用 –ignore-table 参数
    mysqldump -uusername -p  --single-transaction --master-data=2 --add-drop-database  -B DBNAME --ignore-table=DBNAME.table1 --ignore-table=DBNAME.table2 > backup.$(date +%F).sql
    ```

8. 导出数据直接压缩
    ```bash
    # 导出压缩
    mysqldump -uusername -p -B DBNAME | gzip > backup.sql.gz
    # 解压命令：
    gunzip backup.sql.gz
    ```
