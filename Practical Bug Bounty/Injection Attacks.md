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