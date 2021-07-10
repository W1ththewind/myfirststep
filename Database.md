# Database  

## 创建数据库
```sql
Create database database_name
on primary
(
    name = file_name,  
    filename = 'address\filename.mdf',  
    size = X,  
    maxsize = Y,  
    filegrowth = 10%
),
(
    name = subfile_name,
    ...    
)，
filegroup group_name
(    
    ...
),
(    
    ...
),
Log on  
(
    name = logfile_name,
    filename = 'address\logfilename.ldf',
    size = X,
    maxsize = unlimited,
    filegrowth = 1MB
)
```  
> primary文件与次文件之间用' **,** '隔开  
> 若创建快照，只需按照创建数据库文件的方式，不填写具体size信息，并在括号后添加
```sql
 as snapshot of database_name  
 go  
```

---  

## 创建表  
```sql
Create table table_name
(
    column_0 type primary key identity
    column_1 type unique
)
```
> identity：使column自增长
## 修改表  
### 增删改column
```sql
alter table table_name
add column_name type
drop column column_name
alter column column_name type
```
### 主键约束
```sql
Alter table table_name
add constraint constraint_name 
primary key(column_name)
```
### 外键约束
```sql
Alter table table_name
add constraint constraint_name 
foreign key(column_name)
reference table_name(column_name)
on delete cascade/set null/set default/no action
on update cascade/set null/set default/no action
```
### 唯一性约束
```sql
alter table table_name
add constraint constraint_name  
unique(conlumn_name)
```
### 检查约束
```sql
alter table table_name
add constraint constraint_name 
check(column_limits)
```  
> 通常可用于控制属性的数值范围  
---
## 选择
```sql
select (约束) select_list as '列名' from table_0，table_1 
join table_2 on condition
where condition and/or condition
group by group_list
having condition
order by order_list asc/desc
```
> - Select 可加的约束：distinct/top n  
> - Select 后接聚合函数如 sum();avg();max();min();count()等，需注意 **where** 后不能接聚合函数  
> - Like 模式匹配： %不限字符，_一个字符，[1-5]限制范围为1-5，[^123]排除123
> - Group by 后需接的list为 未包含在聚合函数内的列名
> - Having 通常与 Group by 联用，用于进一步筛选结果  
> - Order by ASC升序排列，DESC为降序
> - 针对字符的操作：
> - - ascii()：左非空第一字节转为ascii码
> - - ltrim/rtrim()：消除左/右空格
> - - lower/upper()：小/大写显示
> - - revenue()：逆序
> - - left(表达式,n)：取左边第n个开始的字符
> - - substring（表达式，start，length）：取从start处开始，length长度个字符
---
## 视图
```sql
create view view_name
as
select ...
```
---
## 函数
```sql
create function fun_name returns return_type
as
begin
    ...
return
end
```
> 注意定义表值函数（即返回表的函数）使用时应视为表，至少要给予一个列名
---
## 存储过程
```sql
create procedure proc_name @parameter_1 datatype,@parameter_2 datatype output
as
begin
    ...
end
go

execute proc_name

```
> 
---
## 触发器
```sql
create trigger tigger_name on table
for/after/instead of     insert/update/delete
as
{
    ...
}
```
---
## 游标
```sql
declare cursor_name cursor for select_statement
open cursor
fetch cursor_name into variable_name
close cursor
```
> 
---
## 备份
```sql
exec sp_addumpdevice 'DISK','BP1','文件地址'
backup database database_name to 设备名
restore database database_name from 备份设备 
```
> sp_addumpdevice存储过程用于创建备份设备，'BP1'即为设备名
---
## 用户和权限
```sql
create login [pc名/用户]
for Windows
with default_database = database_name
-----
create login user_name
with password = '123456'
with default_database = database_name
-----
create user user_name
login login_name
with default_schema = dbo
-----
grant/deny 权限 on table to user1
revoke 权限 on table from user1 
```
> Windows、server、database用户注意区分