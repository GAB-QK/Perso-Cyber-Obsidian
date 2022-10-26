---
id: 3-BASH
created_date: 26/10/2022
updated_date: 26/10/2022
type: note
---

#  3-BASH
- **🏷️Tags** :  #10-2022 #command #basics #linux #scripting #bash

# Comparison Operators

---

To compare specific values with each other, we need elements that are called [comparison operators](https://www.tldp.org/LDP/abs/html/comparison-ops.html). The `comparison operators` are used to determine how the defined values will be compared. For these operators, we differentiate between:

-   `string` operators
-   `integer` operators
-   `file` operators
-   `boolean` operators

---

## String Operators

If we compare strings, then we know what we would like to have in the corresponding value.

| **Operator** | **Description**                     |
| ------------ | ----------------------------------- |
| `==`         | is equal to                         |
| `!=`         | is not equal to                     |
| `<`          | is less than ASCII alphabetic order |
| `>`          | is greater than in ASCII order      |
| `-z`         | if the string is empty (null)       |
| `-n`            | if the string is not null                                    |

String comparison operators "`<` / `>`" works only within the double square brackets `[[ <condition> ]]`. We can find the ASCII table on the Internet or by using the following command in the terminal. We take a look at an example later.

### Attention 
It is important to note here that we put the variable for the given argument (`$1`) in double-quotes (`"$1"`). This tells Bash that the content of the variable should be handled as a string. Otherwise, we would get an error.

## Integer Operators

Comparing integer numbers can be very useful for us if we know what values we want to compare. Accordingly, we define the next steps and commands how the script should handle the corresponding value.

| **Operator** | **Description**          |
| ------------ | ------------------------ |
| `-eq`        | is equal to              |
| `-ne`        | is not equal to          |
| `-lt`        | is less than             |
| `-le`        | is less than or equal to |
| `-gt`        | is greater than          |
| `-ge`        | is greater or equal to                         |


## File Operators

The file operators are useful if we want to find out specific permissions or if they exist.

| **Operator** | **Description** |
| ------------ | --------------- |
|`-e`|if the file exist|
|`-f`|tests if it is a file|
|`-d`|tests if it is a directory|
|`-L`|tests if it is if a symbolic link
|`-N`|checks if the file was modified after it was last read|
|`-O`|if the current user owns the file|
|`-G`|if the file’s group id matches the current user’s|
|`-s`|tests if the file has a size greater than 0|
|`-r` |tests if the file has read permission|
|`-w`|tests if the file has write permission|
|`-x`|tests if the file has execute permission|

Code: bash

```bash
#!/bin/bash

# Check the boolean value
if [[ -z $1 ]]
then
	echo -e "Boolean value: True (is null)"
	exit 1

elif [[ $# > 1 ]]
then
	echo -e "Boolean value: True (is greater than)"
	exit 1

else
	domain=$1
	echo -e "Boolean value: False (is equal to)"
fi
```

## Logical Operators

With logical operators, we can define several conditions within one. This means that all the conditions we define must match before the corresponding code can be executed.

| **Operator** | **Description** |
| ------------ | --------------- |
|`!`|logical negotation NOT|
|`&&`|logical AND|
|double pipe|logical OR|

Code: bash

```bash
#!/bin/bash

# Check if the specified file exists and if we have read permissions
if [[ -e "$1" && -r "$1" ]]
then
	echo -e "We can read the file that has been specified."
	exit 0

elif [[ ! -e "$1" ]]
then
	echo -e "The specified file does not exist."
	exit 2

elif [[ -e "$1" && ! -r "$1" ]]
then
	echo -e "We don't have read permission for this file."
	exit 1

else
	echo -e "Error occured."
	exit 5
fi
```

## Questions/Thoughts


## 🔗 Links
- 