<h3>Basic LFI</h3>
In the exercise below, there is an example web app which allows users to switch their language. If you change the language by pressing on Language and then Spanish, you can see that the URL changes to http://<SERVER_IP>:<PORT>//index.php?language=es.php.<br>
If the application is pulliong a file that is being included in the page, we may be able to change what file it is accessing. Two common readable files are ```/etc/passwd ``` on linux and  ```C:\Windows\boot.ini``` on Windows. Therefore to access the file containing the passwords it is possible to replace ```es``` with ```/etc/psswd```. However, this only works if the whole input is used in the ```include()``` function without any additions, simmilarly to the vulnerable code seen in the Intro to File Inclusion File. <br>
However, if a string is appende or prepended the payload must change. For,example he developer may add a directory like in the example below:
```
include("./languages/" . $_GET['language']);
```

















FIrst i tried etc/pswd to figure out how many indentations present.
then ../etc/psswd, all the way to ../../../../etc/passwd
"barry:x:1000:1000::/home/barry:/bin/sH" was outputted at teh bottom of the user list. So name of ser starting with b i barry
did same thing with ../usr/share/flags/flag.txt
