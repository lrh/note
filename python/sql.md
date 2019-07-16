
# sql

```python
# 访问mysql
import MySQLdb

def run_sql(host,user,passwd,db_name,port,sql_str):
	conn=MySQLdb.connect(host=host,user=user,passwd=passwd,db=db_name,port=port)
	cur=conn.cursor()
	cur.execute(sql_str)
	cur.close()
	conn.commit()
	conn.close()
	pass
```
