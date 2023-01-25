# tpch-data

```bash
$ pip install pyarrow duckdb
$ python3
>>> import duckdb
>>> import pyarrow.parquet as pq
>>> con = duckdb.connect(database=':memory:')
>>> con.execute("INSTALL tpch; LOAD tpch")
>>> con.execute("CALL dbgen(sf=10)")
>>> print(con.execute("show tables").fetchall())
[('customer',), ('lineitem',), ('nation',), ('orders',), ('part',), ('partsupp',), ('region',), ('supplier',)]
>>> tables = ["customer", "lineitem", "nation", "orders", "part", "partsupp", "region", "supplier"]
>>> for t in tables:
...     res = con.query("SELECT * FROM " + t)
...     pq.write_table(res.to_arrow_table(), t + ".parquet")
...
```
