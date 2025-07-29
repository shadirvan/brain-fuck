- In HTTP version 1 there are two ways to specify how long the content is 
- The parameters used are `Content-Length` or  `Transfer-Encoding`
- Content-Length value takes no of byte (which can be seen on the right side of burp as selection when selected). Transfer-Encoding takes the no of chunks.
- In a web app there might be a front end server and a back end server.
- The front-end might use content-length to identify the length of the request while back-end might use Transfer-Encoding.
-  What happens in smuggling is that the front only process the request based on content-length and the rest is left.
- when the request reaches the back-end according to the transfer-encoding the request might not be complete and result in a timeout.
- Smuggling take advantage of this vulnerability.
- The Left Part is then used with the next request resulting in the smuggling of the left part.
Note : non-printable characters are also taken as part of content length. turn on the option show non printable character button(the \n button)

First Request:
```
POST / HTTP/1.1
Host: 0a470001049308108199432d0002004f.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

0

G

```

Second Request

```
POST / HTTP/2
Host: 0a470001049308108199432d0002004f.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 7
Foo=bar
```

- The content length of the first request includes the non-printable characters also.
- The G is not consider or is left in the first request
- Then It is send as part of the second request resulting in a  method GPOST.