<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>SQL-10</title>
</head><body>Sql-10 10 ---<br/>
https://sql-mayham.openctf.com/ziopxuoiwquyerhnszpasdyvzlkxcjlwerqwer/sql-10/ <br/>
<br/>
I will save you a bunch of time. This one does not require you to &quot;escape&quot; the query to inject. This code puts the user supplied input directly into the query.<br/>
<img src="screenshot.png"/><br/>
Note: Anytime you inject SQL the statement must be balanced. The -- at the end of the query ends the query and discards anything after it. Not all SQL languages use --, so don't give up if that doesn't work in the future.<br/>
<br/>
With this in mind, lets try an easy one.<br/>
<img src="screenshot 2.png"/><br/>
<br/>
The first thing we need to do is determine the number of columns will return data. Based on the output, we can assume at least 4 and start testing there.<br/>
Note: There are lots of great references for commands if you need one.  <br/>
http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet<br/>
https://www.owasp.org/index.php/Testing_for_SQL_Injection_(OTG-INPVAL-005)<br/>
<img src="screenshot 3.png"/><br/>
The first thing interesting you sould notice is that we only got back <br/>
(1,2,3,4) <br/>
and not <br/>
(1 'bob', 'simmons', 'none')<br/>
(1, 2, 3, 4)<br/>
This is important, because we are only getting 1 row of data back and only 4 columns worth. Next lets try 5.<br/>
<img src="screenshot 4.png"/><br/>
This tells us there is an error because of the number of columns don't match. You usually wont get this, but instead will probably not get back any results. Tip: After getting the first error on number of columns, change from 1 (which will get interpreted as a string or in) and instead use null. Null can be any type and won't error if the appliction expects a specific type (i.e. String).<br/>
<br/>
What version of sql is running? If you remember the error statement, it tells you (sqlite). So now lets get back data. First remember we only get back one row. We need to put our data back in those 4 spots of the union to be able to read it. We will need to start by figuring out the table name (we will skip the typical stuff like user running it etc.).<br/>
1 union select 1, 2, 3, name from sqlite_master; --<br/>
<img src="screenshot 5.png"/><br/>
<br/>
Now that we have the table name. Lets find the column names.<br/>
1 union select 1,2,3, sql FROM sqlite_master; --<br/>
<img src="screenshot 6.png"/><br/>
<br/>
This says that the id is the primary key and it autoincrements. For kicks and giggles, lets find out what the last one is.<br/>
1 union select 1,2,3,max(id) FROM person;--<br/>
<img src="screenshot 7.png"/><br/>
now lets query this one<br/>
<img src="screenshot 8.png"/><br/>
We have the FLAG!<br/>
</body></html>