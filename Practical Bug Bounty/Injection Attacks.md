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
- 