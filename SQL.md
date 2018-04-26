- 查找入职员工时间排名倒数第三的员工所有信息
```
SELECT * FROM employees ORDER BY hire_date DESC LIMIT 2,1;

// LIMIT m,n : 表示从第m+1条开始，取n条数据；
// LIMIT n ： 表示从第0条开始，取n条数据，是limit(0,n)的缩写。
```

