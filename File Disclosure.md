### Basic LFI
In the exercise below, there is an example web app which allows users to switch their language. If you change the language by pressing on Language and then Spanish, you can see that the URL changes to ```http://<SERVER_IP>:<PORT>//index.php?language=es.php```.<br>
If the application is pulliong a file that is being included in the page, we may be able to change what file it is accessing. Two common readable files are ```/etc/passwd ``` on linux and  ```C:\Windows\boot.ini``` on Windows. Therefore to access the file containing the passwords it is possible to replace ```es``` with ```/etc/psswd```. However, this only works if the whole input is used in the ```include()``` function without any additions, simmilarly to the vulnerable code seen in the Intro to File Inclusion File. <br>
However, if a string is prepended the payload must change. For example, the developer may add a directory like in the example below:
```
include("./languages/" . $_GET['language']);
```
Therefore, we need to traverse directories by using realtive paths. This means that we need to add ```../``` before the filename to go back one directory. Trial and error is required to know how many paths back you have to go.<br>
Additionally, if the string is prepended the paylaod will also change. For example in this code segment:
```
include("lang_" . $_GET['language']);
```
To bypass this, place a ```/``` before the payload, allowing us to bypass the filename.<br>
### Second-Order Attacks
Second-Order vulnrabilities are found when a web application's functionality is insecurely pulling files from the bcak-end server based on user-controlled paramaters. For example, if the web application allows us to download a avatar through a URL such as ```/profile/$username/avatar.png```, it may be possible to change the file which is being pulled. For example, if the username is changed to ```../../../etc/passwd)```
### Practical exercise
Once you spawn your target, place the IP into your browser. After this you should be be on a website similar to this:
<img width="911" height="712" alt="image" src="https://github.com/user-attachments/assets/4c4e0f3f-23c0-4915-802a-8eceee57b284" />
After this, I decided to investigate how changing the language affects the URL. I could see that the URL after changing the language to spanish was ```http://<SERVER_IP>:<PORT>//index.php?language=es.php```.<br>
From the information given before, I knew that by replacing the ```es.php``` in the URL, I could trigger a File Inclusion Vulnrability. Therefore I tried replacing it with ```etc/psswd``` , but nothing popped up.<br> <br>
Therefore, I kept adding ```../``` before the payload to go back one directory. Eventually, when I inputted ```../../../../etc/passwd``` a list of passwords and users appeared. Since I knew that we were searching for a user whose name started with a "B", I found the answer to the first question.<br>
Q1.Using the file inclusion find the name of a user on the system that starts with "b".<br>
A1.barry<br><br>
After this I decided to combine the file path (```/usr/share/flags```) and file name (```flag.txt file```) together to get the next payload ```/usr/share/flags/flag.txt```. After inputting that however, no results popped up. Therefore, I added ```../``` before the payload until the flag appeared.<br>
Q2.Submit the contents of the flag.txt file located in the /usr/share/flags directory.<br>
A2.HTB{n3v3r_tru$t_u$3r_!nput}
