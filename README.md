# EX-11-Oracle-Database-Connection-with-Python

## DATE : 26/10/23
# AIM :
To connect Oracle database with Python using cx_Oracle module.

# PROCEDURE :
1.Install cx-Oracle : With the command pip install cx-Oracle
2.To Connect connect(): Now Establish a connection between the Python program and Oracle database by using connect() function.

```
con = cx_Oracle.connect('username/password@localhost')
cursor(): To execute a SQL query and to provide results some special object is
 required that is nothing but cursor() object.
cursor = con.cursor()
```
3.To Execute execute/executemany method:

```
cursor.execute(sqlquery) - - - -> to execute a single query. 
cursor.executemany(sqlqueries) - - - -> to execute a single query
 with multiple bind variables/place holders.
```
4.To Commit commit(): For DML(Data Manipulation Language) queries that comprise operations like update, insert, delete. We need to commit() then only the result reflects in the database.
5.To Fetch rows: fetchone(), fetchmany(int), fetchall(): fetchone() : This method is used to fetch one single row from the top of the result set. fetchmany(int): This method is used to fetch a limited number of rows based on the argument passed in it. fetchall() : This method is used to fetch all rows from the result set.
6.To Close db connectivity close(): After all done it is mandatory to close all operations.
```
cursor.close()
con.close()
```
# PROGRAM :
```
# importing module
import cx_Oracle

# Create a table in Oracle database
try:
	con = cx_Oracle.connect('tiger/scott@localhost:1521/xe')
	print(con.version)
	# Now execute the sqlquery
	cursor = con.cursor()
	# Creating a table employee
	cursor.execute(
		"create table employee(empid integer primary key,
name varchar2(30), salary number(10, 2))")
	print("Table Created successfully")
except cx_Oracle.DatabaseError as e:
	print("There is a problem with Oracle", e)
# by writing finally if any error occurs
# then also we can close the all database operation
finally:
	if cursor:
		cursor.close()
	if con:
		con.close()
```
OUTPUT :

![image](https://github.com/Kamali22004796/EX-11-Oracle-Database-Connection-with-Python/assets/120567837/d739f334-a8eb-4e21-a5b6-e3be97b02d86)


# PROGRAM :
```
import cx_Oracle
# Load data from a csv file into Oracle table using executemany
try:
	con = cx_Oracle.connect('tiger/scott@localhost:1521/xe')
except cx_Oracle.DatabaseError as er:
	print('There is an error in Oracle database:', er)
else:
	try:
		cur = con.cursor()
		data = [[10007, 'Vikram', 48000.0], [10008, 'Sunil', 65000.1],
[10009, 'Sameer', 75000.0]]
		cur = con.cursor()
		# Inserting multiple records into employee table
		# (:1,:2,:3) are place holders. They pick data from
a list supplied as argument
		cur.executemany('insert into employee values(:1,:2,:3)', data)
	except cx_Oracle.DatabaseError as er:
		print('There is an error in Oracle database:', er)
	except Exception as er:
		print(er)
	else:
		# To commit the transaction manually
		con.commit()
		print('Multiple records are inserted successfully')
finally:
	if cur:
		cur.close()
	if con:
		con.close()
```

# OUTPUT :

![image](https://github.com/Kamali22004796/EX-11-Oracle-Database-Connection-with-Python/assets/120567837/546f92d0-7903-4130-852b-389759a86f95)


# PROGRAM :
```
import cx_Oracle
try:
	con = cx_Oracle.connect('tiger/scott@localhost:1521/xe')
except cx_Oracle.DatabaseError as er:
	print('There is error in the Oracle database:', er)
else:
	try:
		cur = con.cursor()
		cur.execute('select * from employee where salary > :sal',
{'sal': 50000})
		rows = cur.fetchall()
		print(rows)
	except cx_Oracle.DatabaseError as er:
		print('There is error in the Oracle database:', er)
	except Exception as er:
		print('Error:', er)
	finally:
		if cur:
			cur.close()
finally:
	if con:
		con.close()
```
# OUTPUT :

![image](https://github.com/Kamali22004796/EX-11-Oracle-Database-Connection-with-Python/assets/120567837/42cc54bf-6cce-4cc5-b102-abf2f302d8b5)


# RESULT :
Thus the program for dababase connectivity with python has been executed successfully.
