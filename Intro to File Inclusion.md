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
<br>
Similarly to PHP, Node JS also loads content based off HTTP paramaters. FOr example:
```
if(req.query.language) {
    fs.readFile(path.join(__dirname, req.query.language), function (err, data) {
        res.write(data);
    });
}
```
In this code snippet, whatever paramater is passed in the URL is transfered to the ```readfile``` function, which then displays the file content as a HTTP response. <br>
Alternatively, the ```render()``` function within the Express.js framework can alsolead to a vulnrability as seen in the code snippet below:
```
app.get("/about/:language", function(req, res) {
    res.render(`/${req.params.language}/about.html`);
});
```
In this example, the ```render```function takes an input directly from the URL, meaning that we can change the URL to show a different file.<br>
The same concept applied to Java where the ```include``` function can be used to access local files.
For example,
```
<c:if test="${not empty param.language}">
    <jsp:include file="<%= request.getParameter('language') %>" />
</c:if>
```
Here, the iclude function takes an input directly from the URL and then renders the object into a front-end temlate. This means that it can be used to access certain local files.<br>
Alternatively, the ```import``` function can be used to render a local file, and if the input comes straight from the URL, it can be easily exploited.<br>
File Inclusion vulnrabilities may also occur in .NET web applications due to the ```Response.WriteFile``` function which takes a file path as an input and then writes the files contents as a response.
This can be seen in the example below:
```
@if (!string.IsNullOrEmpty(HttpContext.Request.Query['language'])) {
    <% Response.WriteFile("<% HttpContext.Request.Query['language'] %>"); %> 
}
```
Additionally, the ```@HTML.Partial()``` or the ```include``` function can also be used to render local files if they can be manipulated by the user
<h3>Read vs Execute</h3>
File Inclusion vulnrabilities may occur in any webserver and any developmental framework since all of them can load dynamic content. However, only some of the functions listed above can be used to execute files whilst others only give enough permissions to read the file. A list of all the functions and their respective capabilities are listed in the lab.
