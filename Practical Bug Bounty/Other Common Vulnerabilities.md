### Cross Site Request Forgery
- Vulnerability that allows an attacker to induce users to perform actions that they do not intend to perform.
- If a user is logged in a system. then if there is not csrf token to validate each user requests. this vulnerability allows actions such as changing the password, email, etc.
- A malicious link or site is sent to the user and when user open it in their browser, their authenticated session will be used to perform the malicious activity.
- There might be csrf token send as a hidden field in a form.
- Sometimes in a poorly secured security mechanism there might not be proper validation of csrf token - simply the existence of the csrf token will be enough.
### Server Side Request Forgery
 - A type of vulnerability that allows us to induce the server to make requests on our behalf.
 -  In a Scenario where there is a website that fetches price of a product. In it's body it contains a URL like `http://localhost/labs/api/price.php`. Now by fuzzing the `http://localhost/labs/api/FUZZ` we got a admin page. but when we try to access it denies the access to website. 
 - If the site is vulnerable to SSRF we can simply put the admin URL `http://localhost/labs/api/admin.php` in the body of the request and get the contents of the page.
 - We can also do the fuzzing for internal IPs like **10.10.10.4** and giving it in our current scenario request which may give us some data which may not be accessible from the outside web.
### Open Redirect
- Simple vulnerabilities that allows modification of return URL that in turn could allow the attacker to forward user to malicious links.
- for example in a link : `https://example.com/posts.php?id=2&return_url=https://example.com/home.php` when the user interact with the browser and click return button or something the user is redirected to the website given in the URL. attacker could change the URL to lead user into some malicious websites.