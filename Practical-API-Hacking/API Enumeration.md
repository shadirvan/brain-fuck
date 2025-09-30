- The first step that is performed when we get a API endpoint.
- Bookstore in tryhackme is a beginner level API fuzzing or enumeration room.
- check whether there is a v1, v2, v3  or v0 of the api by using the repeater in burp.
- check whether there is change in content or anything.
- Send the api request to intruder and fuzz for for different endpoints using a wordlist.
- `wfuzz` can also be used for fuzzing the web request. The syntax is : 
`wfuzz -c -z file,/usr/share/wordlists/dirb/common.txt --sc 200 'http://example.com/api/v1/books?show=FUZZ'`
-  The `--sc 200` shows only the 200 responses.