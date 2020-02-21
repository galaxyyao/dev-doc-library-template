# SQL语句 
### 1. 【强制】不要使用count(列名)或count(常量)来替代count(*)
**说明**  
count(*)会统计值为NULL的行，而count(列名)不会统计此列为NULL值的行。 

### 2. 【强制】因此使用sum()时需注意NPE问题
**说明**  
当某一列的值全是NULL时，count(col)的返回结果为0，但sum(col)的返回结果为NULL。
可以使用如下方式来避免sum的NPE问题：  
```sql
SELECT IF(ISNULL(SUM(g)),0,SUM(g)) FROM table;
```
### 3. 【强制】禁止在开发代码中使用TRUNCATE
TRUNCATE无事务且不触发trigger，有可能造成事故

### 4. 【推荐】尽量避免使用存储过程
存储过程难以调试和扩展，更没有移植性。  

### 5. 【推荐】需要仔细评估in后边的集合元素数量，控制在1000个之内

### 6. 统计字数使用CHARACTER_LENGTH而非LENGTH
**说明**  
```sql
-- 返回为12
SELECT LENGTH("轻松工作");
-- 返回为4
SELECT CHARACTER_LENGTH("轻松工作");
```


