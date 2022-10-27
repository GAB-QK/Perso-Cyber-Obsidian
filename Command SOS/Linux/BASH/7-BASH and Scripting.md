---
id: 5-BASH
created_date: 26/10/2022
updated_date: 26/10/2022
type: note
---

#  5-BASH
- **🏷️Tags** :  #10-2022  #command #basics #linux #scripting #bash

# Functions

---
`Functions` are an essential part of scripts and programs, as they are used to execute recurring commands for different values and phases of the script or program. Therefore, we do not have to repeat the whole section of code repeatedly but can create a single function that executes the specific commands. The definition of such functions makes the code easier to read and helps to keep the code as short as possible. It is important to note that functions must always be defined logically `before` the first call since a script is also processed from top to bottom. Therefore the definition of a function is always `at the beginning` of the script. There are two methods to define the functions:

#### Method 1 - Functions

Code: bash

```bash
function name {
	<commands>
}
```

#### Method 2 - Functions

Code: bash

```bash
name() {
	<commands>
}
```

We can choose the method to define a function that is most comfortable for us. In our `CIDR.sh` script, we used the first method because it is easier to read with the keyword "`function`."

## Parameter Passing

Such functions should be designed so that they can be used with a fixed structure of the values or at least only with a fixed format. Like we have already seen in our `CIDR.sh` script, we used the format of an IP address for the function "`network_range`". The parameters are optional, and therefore we can call the function without parameters. In principle, the same applies to the passed parameters as to parameters passed to a shell script. These are `$1` - `$9` (`${n}`), or `$variable` as we have already seen. Each function has its own set of parameters. So they do not collide with those of other functions or the parameters of the shell script.

An important difference between bash scripts and other programming languages is that all defined variables are always processed `globally` unless otherwise declared by "[local](https://www.tldp.org/LDP/abs/html/localvar.html)." This means that the first time we have defined a variable in a function, we will call it in our main script (outside the function). Passing the parameters to the functions is done the same way as we passed the arguments to our script and looks like this:

#### PrintPars.sh

Code: bash

```bash
#!/bin/bash

function print_pars {
	echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"
```

  PrintPars.sh

```shell-session
GabrielQK@htb[/htb]$ ./PrintPars.sh

First parameter Second parameter Third parameter
```

## Return Values

When we start a new process, each `child process` (for example, a `function` in the executed script) returns a `return code` to the `parent process` (`bash shell` through which we executed the script) at its termination, informing it of the status of the execution. This information is used to determine whether the process ran successfully or whether specific errors occurred. Based on this information, the `parent process` can decide on further program flow.

| **Return Code** | **Description**                |
| --------------- | ------------------------------ |
| `1`             | General errors                 |
| `2`             | Misuse of shell builtins       |
| `126`           | Command invoked cannot execute |
| `127`           | Command not found              |
| `128`           | Invalid argument to exit       |
| `128+n`         | Fatal error signal "`n`"       |
| `130`           | Script terminated by Control-C |
| `255\*`         | Exit status out of range       |

#### Return.sh

Code: bash

```bash
#!/bin/bash

function given_args {

        if [ $# -lt 1 ]
        then
                echo -e "Number of arguments: $#"
                return 1
        else
                echo -e "Number of arguments: $#"
                return 0
        fi
}

# No arguments given
given_args
echo -e "Function status code: $?\n"

# One argument given
given_args "argument"
echo -e "Function status code: $?\n"

# Pass the results of the funtion into a variable
content=$(given_args "argument")

echo -e "Content of the variable: \n\t$content"
```

**Output**


```shell-session
GabrielQK@htb[/htb]$ ./Return.sh

Number of arguments: 0
Function status code: 1

Number of arguments: 1
Function status code: 0

Content of the variable:
    Number of arguments: 1
```

### Exercice

Create a "For" loop that encodes the variable "var" 28 times in "base64". The number of characters in the 28th hash is the value that must be assigned to the "salt" variable.

Code: bash

```bash
#!/bin/bash

# Decrypt function
function decrypt {
	MzSaas7k=$(echo $hash | sed 's/988sn1/83unasa/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/4d298d/9999/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/3i8dqos82/873h4d/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/4n9Ls/20X/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/912oijs01/i7gg/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/k32jx0aa/n391s/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/nI72n/YzF1/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/82ns71n/2d49/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/JGcms1a/zIm12/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/MS9/4SIs/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/Ymxj00Ims/Uso18/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/sSi8Lm/Mit/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/9su2n/43n92ka/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/ggf3iunds/dn3i8/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/uBz/TT0K/g')

	flag=$(echo $MzSaas7k | base64 -d | openssl enc -aes-128-cbc -a -d -salt -pass pass:$salt)
}

# Variables
var="9M"
salt=""
hash="VTJGc2RHVmtYMTl2ZnYyNTdUeERVRnBtQWVGNmFWWVUySG1wTXNmRi9rQT0K"

# Base64 Encoding Example:
#        $ echo "Some Text" | base64

# <- For-Loop here

# Check if $salt is empty
if [[ ! -z "$salt" ]]
then
	decrypt
	echo $flag
else
	exit 1
fi
```

### solution 
```bash
#!/bin/bash

  

# Decrypt function

function decrypt {
MzSaas7k=$(echo $hash | sed 's/988sn1/83unasa/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/4d298d/9999/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/3i8dqos82/873h4d/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/4n9Ls/20X/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/912oijs01/i7gg/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/k32jx0aa/n391s/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/nI72n/YzF1/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/82ns71n/2d49/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/JGcms1a/zIm12/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/MS9/4SIs/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/Ymxj00Ims/Uso18/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/sSi8Lm/Mit/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/9su2n/43n92ka/g')
Mzns7293sk=$(echo $MzSaas7k | sed 's/ggf3iunds/dn3i8/g')
MzSaas7k=$(echo $Mzns7293sk | sed 's/uBz/TT0K/g')
  
flag=$(echo $MzSaas7k | base64 -d | openssl enc -aes-128-cbc -a -d -salt -pass pass:$salt)

}

# Variables
var="9M"
salt=""
hash="VTJGc2RHVmtYMTl2ZnYyNTdUeERVRnBtQWVGNmFWWVUySG1wTXNmRi9rQT0K"

for counter in {1..28}
do
	var=$(echo $var | base64)
done

lenght=$(echo $var | wc -c)
salt=$lenght

# Check if $salt is empty
if [[ ! -z "$salt" ]]
then
	decrypt
	echo $flag
else
exit 1
fi
```
## Questions/Thoughts


## 🔗 Links