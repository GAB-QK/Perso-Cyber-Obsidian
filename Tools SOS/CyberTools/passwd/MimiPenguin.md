---
id: MimiPenguin
created_date: 10/10/2022
updated_date: 10/10/2022
type: note
---

#  MimiPenguin
- **🏷️Tags** :  #10-2022 #password #credentials #tools #browser

## 📝 Notes
- Many applications and processes work with credentials needed for authentication and store them either in memory or in files so that they can be reused. For example, it may be the system-required credentials for the logged-in users. Another example is the credentials stored in the browsers, which can also be read. In order to retrieve this type of information from Linux distributions, there is a tool called [mimipenguin](https://github.com/huntergregal/mimipenguin) that makes the whole process easier. However, this tool requires administrator/root permissions.

- Takes advantage of cleartext credentials in memory by dumping the process and extracting lines that have a high probability of containing cleartext passwords. Will attempt to calculate each word's probability by checking hashes in /etc/shadow, hashes in memory, and regex searches. 2.0 introduces a clean C port that aims to increase the speed of execution and portability


## Questions/Thoughts


## 🔗 Links
- https://github.com/huntergregal/mimipenguin
![[Pasted image 20221010193014.png]]