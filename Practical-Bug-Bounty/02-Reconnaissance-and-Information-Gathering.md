### Fingerprinting Web Technologies
- use `https://builtwith.com` to find out what websites are built with.
- `Wappalyzer`  extension on browser allows to check the technologies the website is built.
- `curl -I https://example.com`  to use curl command to get the website information like headers. `-L` argument follows the redirect.
- `securityheaders.com` allows you to see the headers used and what headers are missing.
- we can also get some information of website using nmap. `nmap -p443 -A example.com`
### Directory Enumeration and Brute Forcing
- `fuff`: Directory brute force tool.
	- usage : `fuff -w /path/to/wordlist:FUZZ -u http://<ip>/FUZZ`
	- `-recursion` argument can be used to enable the recursion
	- `-recursion-depth` : for maximum recursion depth
- `dirb` : directory buster, has default configuration
	- basic syntax : `dirb http://example.com` : it uses default word list and configuration. 
- `OWASP DirBuster` : GUI based directory enumeration tool
### Subdomain Enumeration
- in order to find the subdomain with google dorking use : `site:example.com -www` as search query. the `-www` remove the sites starts with that.
- We can find subdomains using certificate search. go to `crt.sh` and search `%.example.com`
- `subfinder -d example.com` : tool used to find the subdomains.
- `assetfinder example.com` : This finds assets related to the given domain. even assets related to sister companies.
- `amass enum -d example.com` : this tool has lot of other capabilities also.
- output this to a single file.
- `httprobe` : check whether the subdomain is alive.
- `cat example-subdomains.txt | grep example.com | sort -u | httprobe -prefer-https | grep https > example-alive.txt` : This piped command gives the the https domains that are alive.
- `gowitness scan file -f alive.txt --no-http`: this command takes a screenshot of the pages. Also remember to remove the `https://` part from the live domains text file. find and replace in mousepad can be used for this.
### Burp Suite
- The history of requests can be seen in the `Target` tab next to dashboard tab.
- The Scope section under it can be used to set the in scope and out scope domains.
- There is also advanced scope control that support a host or IP range and different options.
- In extension tab, Inside the BApp Store we can add different extensions