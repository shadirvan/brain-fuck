### Brute force Login
#### Burpsuit
- Intercept the post request for login
- add it to intruder
- add a position
- load a payload configuration (word list)
- Start the Attack. Check The length of responses. The odd one might be the right word or password.
#### FFUF
- Copy the request to file by right clicking and selecting the option.
- edit the request file and replace the password to `FUZZ` and save it.
- use `ffuf -request req.txt -request-proto http -w <path to wordlist> -fs 1814` 
	- the `-fs 1814` filters all the request that are of size 1814. this value is found by running the command without the filter and then filter out the size 1814 which is the size of invalid password response.
### Attacking MFA
- When attacking Multi-Factor Authentication:
	- check whether the token expires.
	- Does the token apply to multiple users
	- Is the token weak and brute force able.
	- Can you use it multiple times.
### Attacking Auth with Account lockouts
- In order to attack a user account with like 5 attempts before account lockout we use cluster bomb attack.
- In **burp suite** intercept the traffic and intrude it. 
	- use the cluster bomb attack.
	- add two markers for username and password
	- use a username word list and only use the most common passwords which is less than account lock out threshold.
	- perform the attack.
- To do with **ffuf** : 
	- copy the request to a file from burp.
	- replace the username and password with something like FUZZUSER and FUZZPASS
	- use the command `ffuf -request req.txt -request-proto http -mode clusterbomb -w <username wordlist>:FUZZUSER -w <password wordlist>:FUZZPASS`
- We can visit `https://appsecexplained.gitbook.io` to read about different attack likes Attacking MFA. there is also checklist available for this attacks.
### Insecure Direct Object Reference (IDOR)
- This attack allows unauthorized users to access data.
- for example in page where user details are show the link might be `https://example.com/profile.php?id=10` if it is IDOR vulnerable we can change the id value and still obtain information that we are not authorized to see.
- we can use burp suite intruder brute force this vulnerability.
- To do with ffuf : `ffuf -u 'https://example.com/profile.php?id=FUZZ' -w num.txt -mr 'admin'` : This fuzz and find all the response that contain the regex 'admin'].
### Broken Access Control
- `jwt.io` decodes a encoded JWT token.
- the token has three section each is base64 encoded.
- Broken access control : if there is an API to login to accounts, another API to update account information, every time a person login he get a JWT token and  if a person can use his JWT token and modify other user account it is **broken function level authorization**.
- burp suite has **autorise** extension which allows checking a request against BFLA by using the mentioned cookie in every request