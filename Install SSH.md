ls -al ~/.ssh  ✔  at 16:05:47  ▓▒░
ls: /Users/fauzannurrachman/.ssh: No such file or directory
ls -la ~/.ssh  1 ✘  at 16:06:16  ▓▒░
ls: /Users/fauzannurrachman/.ssh: No such file or directory
mkdir -p ~/.ssh

░▒▓    ~  chmod 700 ~/.ssh  ✔  at 16:08:47  ▓▒░
░▒▓    ~  ssh-keygen -t ed25519 -C "fauzan1812@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/fauzannurrachman/.ssh/id*ed25519): Enter passphrase for "/Users/fauzannurrachman/.ssh/id_ed25519" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/fauzannurrachman/.ssh/id_ed25519
Your public key has been saved in /Users/fauzannurrachman/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:/YJjQA+Mdonry1oJtYSTqZzgkGSrK3MCiq7cZ820r4w fauzan1812@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
| o |
|o..+ + . |
|+.= \* * |
|\_..= = o . |
|++. o . S . |
|+. o . o . . |
|B . + + = . . |
|++.o +o= . . |
|oo.o=E oo. |
+----[SHA256]-----+
░▒▓    ~  eval "$(ssh-agent -s)"  ✔  took 1m 1s   at 16:10:52  ▓▒░
Agent pid 10469
░▒▓    ~  ssh-add ~/.ssh/id_ed25519  ✔  at 16:11:45  ▓▒░
Enter passphrase for /Users/fauzannurrachman/.ssh/id_ed25519:
Identity added: /Users/fauzannurrachman/.ssh/id_ed25519 (fauzan1812@gmail.com)
░▒▓    ~  pbcopy < ~/.ssh/id_ed25519.pub
░▒▓    ~  ssh -T git@github.com  ✔  at 16:13:06  ▓▒░
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi fauzhanFARTF! You've successfully authenticated, but GitHub does not provide shell access.
