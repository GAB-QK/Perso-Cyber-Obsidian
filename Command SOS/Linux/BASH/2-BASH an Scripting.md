---
id: BASH
created_date: 26/10/2022
updated_date: 26/10/2022
type: note
---

#  BASH
- **🏷️Tags** :  #10-2022 #command #basics #linux #scripting #bash 

### Arguments

The advantage of bash scripts is that we can always pass up to 9 arguments (`$0`-`$9`) to the script without assigning them to variables or setting the corresponding requirements for these. `9 arguments` because the first argument `$0` is reserved for the script. As we can see here, we need the dollar sign (`$`) before the name of the variable to use it at the specified position. The assignment would look like this in comparison:

```shell-session
GabrielQK@htb[/htb]$ ./script.sh ARG1 ARG2 ARG3 ... ARG9
       ASSIGNMENTS:       $0      $1   $2   $3 ...   $9
```

This means that we have automatically assigned the corresponding arguments to the predefined variables in this place. These variables are called special variables. These special variables serve as placeholders. If we now look at the code section again, we will see where and which arguments have been used.

#### CIDR.sh

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
else
	domain=$1
fi

<SNIP>
```

There are several ways how we can execute our script. However, we must first set the script's execution privileges before executing it with the interpreter defined in it.

## Special Variables

Special variables use the [Internal Field Separator](https://bash.cyberciti.biz/guide/$IFS) (`IFS`) to identify when an argument ends and the next begins. Bash provides various special variables that assist while scripting. Some of these variables are:

| **IFS** | **Description**                                                                                                               |
| ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `$#`    | This variable holds the number of arguments passed to the script.                                                             |
| `$@`    | This variable can be used to retrieve the list of command-line arguments.                                                     |
| `$n`    | Each command-line argument can be selectively retrieved using its position. For example, the first argument is found at `$1`. |
| `$$`    | The process ID of the currently executing process.                                                                            |
|   `$?`      |             The exit status of the script. This variable is useful to determine a command's success. The value 0 represents successful execution, while 1 is a result of a failure.                                                                                                                  |


Of the ones shown above, we have 3 such special variables in our `if-else`
condition.

| **IFS** | **Description**                                                                                                                                                                                                                                       |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$#`    | In this case, we need just one variable that needs to be assigned to the `domain` variable. This variable is used to specify the target we want to work with. If we provide just an FQDN as the argument, the `$#` variable will have a value of `1`. |
| `$0`    | This special variable is assigned the name of the executed script, which is then shown in the "`Usage:`" example.                                                                                                                                     |
|    `$1`     |      Separated by a space, the first argument is assigned to that special variable.                                                                                                                                                                                                                                                 |


#### Declaring a Variable - Error

  Declaring a Variable - Error

```shell-session
GabrielQK@htb[/htb]$ variable = "this will result with an error."

command not found: variable
```

#### Declaring a Variable - Without an Error

  Declaring a Variable - Without an Error

```shell-session
GabrielQK@htb[/htb]$ variable="Declared without an error."
GabrielQK@htb[/htb]$ echo $variable

Declared without an error.
```


#### Arrays.sh

Code: bash

```bash
#!/bin/bash

domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)

echo ${domains[0]}
```

We can also retrieve them individually using the index using the variable with the corresponding index in curly brackets. Curly brackets are used for variable expansion.

  Arrays.sh

```shell-session
GabrielQK@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com
```

#### Quote Simple/double
It is important to note that single quotes (`'` ... `'`) and double quotes (`"` ... `"`) prevent the separation by a space of the individual values in the array. This means that all spaces between the single and double quotes are ignored and handled as a single value assigned to the array.
#### Arrays.sh

Code: bash

```bash
#!/bin/bash

domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}
```

  Arrays.sh

```shell-session
GabrielQK@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com
```

## Questions/Thoughts


## 🔗 Links
- 