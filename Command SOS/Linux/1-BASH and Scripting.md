---
id: Sans
created_date: 25/10/2022
updated_date: 25/10/2022
type: note
---

#  Sans
- **🏷️Tags** :  #10-2022 #bash #scripting #CheatSheet #linux 



### Shebang

The shebang line is always at the top of each script and always starts with "`#!`". This line contains the path to the specified interpreter (`/bin/bash`) with which the script is executed. We can also use Shebang to define other interpreters like Python, Perl, and others.

Code: python

```python
#!/usr/bin/env python
```

Code: perl

```perl
#!/usr/bin/env perl
```

### Conditional Execution 
#### Script.sh

```bash
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

<SNIP>
```

-   `#!/bin/bash` - Shebang.
-   `if-else-fi` - Conditional execution.
-   `echo` - Prints specific output.
-   `$#` / `$0` / `$1` - Special variables.
-   `domain` - Variables.

#### If-Only.sh

Code: bash

```bash
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
        echo "Given argument is greater than 10."
fi
```

##### If-Only.sh - Execution

  If-Only.sh - Execution

```shell-session
GabrielQK@htb[/htb]$ bash if-only.sh 5
```

  If-Only.sh - Execution

```shell-session
GabrielQK@htb[/htb]$ bash if-only.sh 12

Given argument is greater than 10.
```

#### If-Elif-Else.sh

Code: bash

```bash
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
	echo "Given argument is greater than 10."
elif [ $value -lt "10" ]
then
	echo "Given argument is less than 10."
else
	echo "Given argument is not a number."
fi
```

##### If-Elif-Else.sh - Execution

 
```shell-session
GabrielQK@htb[/htb]$ bash if-elif-else.sh 5

Given argument is less than 10.
```



```shell-session
GabrielQK@htb[/htb]$ bash if-elif-else.sh 12

Given argument is greater than 10.
```



```shell-session
GabrielQK@htb[/htb]$ bash if-elif-else.sh HTB

if-elif-else.sh: line 5: [: HTB: integer expression expected
if-elif-else.sh: line 8: [: HTB: integer expression expected
Given argument is not a number.
```

#### Several Conditions - Script.sh

Code: bash

```bash
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
elif [ $# -eq 1 ]
then
	domain=$1
else
	echo -e "Too many arguments given."
	exit 1
fi

<SNIP>
```

## Exercise Script

Code: bash

```bash
#!/bin/bash
# Count number of characters in a variable:
#     echo $variable | wc -c

# Variable to encode
var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..40}
do
        var=$(echo $var | base64)
done
```

##### Answer 

``` bash
#!/bin/bash
# Count number of characters in a variable:
# echo $variable | wc -c

# Variable to encode

var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..40}
do
	var=$(echo $var | base64)
	if [ $counter -eq 35 ]
	then
		echo $var | wc -c
	fi
done

```

```shell-session
GabrielQK@htb[/htb]$ ./TP1.sh
1197735
```
## Questions/Thoughts


## 🔗 Links
- [CHEATSHEET](https://devhints.io/bash)
- [HELP](https://linuxconfig.org/bash-scripting-cheat-sheet) 