**Lab name: File Inclusiony** <br>
*Link to Lab:* https://academy.hackthebox.com/app/module/23
<br><br><br>
<h3>Intro to File inclusion</h3>
In many modern back-end languages such as PHP, Javascript or Java which use HTTP paramaters, if the functionalities are not securely coded, an attacker can display any local file on the hosting server, also known as a Local File Inclusion Vulnrability.
<h3>Local File Inclusion (LFI)</h3>
LFI vulnrabilities are most frequently found in templating engines. These are software tools that combine static template files with dynamic data to produce web pages. This includes common parts such as the header, navigation bar or footer.<br>
These vunrabilities can lead to source code disclosure, sensitive data exposure or remote code execution.
<h3>Examples of vulnrable code</h3>
In PHP the ```include()``` function is used to load local or remote files. If the ```include()``` function is taken from a user-controlled paramater such as ```GET``` and if the code does not filter and sanitize the user input, the code is vulrable to remote file inclusion.For example:
```
if (isset($_GET['language'])) {
    include($_GET['language']);
}
```
Within this the language paramater from the GET function is directly linked to the include() function without any sanitization. This means that any path that we pass through the language paramater will be loaded onto the page including local files.
