<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
</head>
<body>Nightmare-50<br/>
Automated home work scoring my ass. https://shades-of-nightmare.openctf.com/nzpoixyucvkjwnerntasdfascdvasdfqwerqwe/nightmare-50/<br/>
<br/>
Lets load the page and see what it does.<br/>
<img src="screenshot.png"/><br/>
It looks like it runs python, lets try something.<br/>
<img src="screenshot 2.png"/><br/>
it runs then closses the connection.... Notice that I used print(). This is python 3. If you try print &quot;&quot; it will error because that is python2 syntax.<br/>
<br/>
To figure out the current directory and file names we will need to import os.<br/>
<img src="screenshot 3.png"/><br/>
<br/>
Well, that doesn't work. Can we at least run two lines of code?<br/>
<img src="screenshot 4.png"/><br/>
<br/>
Lets look at the built in functions and see if any can help us.<br/>
https://docs.python.org/3/library/functions.html<br/>
<br/>
I think exec might be helpful. Notice it says &quot;This function supports dynamic execution of Python code. <i>object</i>must be either a string or a code object.&quot;. Lets try testing by using python code as a string.<br/>
<img src="screenshot 5.png"/><br/>
<br/>
Awesome! Now lets see what the current directory is and the files in it.<br/>
REF: https://docs.python.org/3/library/os.html<br/>
<img src="screenshot 6.png"/><br/>
<br/>
Sweet! Now lets just read the flag.txt<br/>
<img src="screenshot 7.png"/><br/>
<br/>
</body></html>