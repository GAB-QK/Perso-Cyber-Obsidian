---
id: 5-BASH
created_date: 26/10/2022
updated_date: 26/10/2022
type: note
---

#  5-BASH
- **🏷️Tags** :  #10-2022  #command #basics #linux #scripting #bash
 
 
 # Flow Control - Loops

---

The control of the flow of our scripts is essential. We have already learned about the `if-else` conditions, which are also part of flow control. After all, we want our script to work quickly and efficiently, and for this, we can use other components to increase efficiency and allow error-free processing. Each control structure is either a `branch` or a `loop`. Logical expressions of boolean values usually control the execution of a control structure. These control structures include:

-   Branches:
    -   `If-Else` Conditions
    -   `Case` Statements
-   Loops:
    -   `For` Loops
    -   `While` Loops
    -   `Until` Loops

#### Syntaxe - Exemples

Code : bash

```bash
for $variable in 1 2 3 4
do
	echo $variable
done
```

Code : bash

```bash
for $variable in file1 file2 file3
do
	echo $variable
done
```

Code : bash

```bash
for ip in "10.10.10.170 10.10.10.174 10.10.10.175"
do
	ping -c 1 $ip
done
```

## While Loops

The `while` loop is conceptually simple and follows the following principle:

-   A statement is executed as long as a condition is fulfilled (`true`).

Code: bash

```bash
<SNIP>
		stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
<SNIP>
```

#### WhileBreaker.sh

Code: bash

```bash
#!/bin/bash

counter=0

while [ $counter -lt 10 ]
do
  # Increase $counter by 1
  ((counter++))
  echo "Counter: $counter"

  if [ $counter == 2 ]
  then
    continue
  elif [ $counter == 4 ]
  then
    break
  fi
done
```

##### Output

```shell-session
GabrielQK@htb[/htb]$ ./WhileBreaker.sh

Counter: 1
Counter: 2
Counter: 3
Counter: 4
```

# Flow Control - Branches

---

As we have already seen, the branches in flow control include `if-else` and the `case` statements. We have already discussed the `if-else` statements in detail and know how this works. Now we will take a closer look at the case statements.

---

## Case Statements

`Case` statements are also known as `switch-case` statements in other languages, such as C/C++ and C#. The main difference between `if-else` and `switch-case` is that `if-else` constructs allow us to check any boolean expression, while `switch-case` always compares only the variable with the exact value. Therefore, the same conditions as for `if-else`, such as "greater-than," are not allowed for `switch-case`. The syntax for the switch-case statements looks like this:

#### Syntax - Switch-Case

Code: bash

```bash
case <expression> in
	pattern_1 ) statements ;;
	pattern_2 ) statements ;;
	pattern_3 ) statements ;;
esac
```

The definition of switch-case starts with `case`, followed by the variable or value as an expression, which is then compared in the pattern. If the variable or value matches the expression, then the statements are executed after the parenthesis and ended with a double semicolon (`;;`).

In our `CIDR.sh` script, we have used such a `case` statement. Here we defined four different options that we assigned to our script, how it should proceed after our decision.

#### CIDR.sh

Code: bash

```bash
<SNIP>
# Available options
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
<SNIP>
```


## Questions/Thoughts


## 🔗 Links