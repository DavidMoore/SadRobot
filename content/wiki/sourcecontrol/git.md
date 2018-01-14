Git
===

Configure for Windows
---------------------

On Windows machine, open up Git Bash

$ ssh-keygen -t rsa -C "David Moore <david@digitalgenus.com>"
Generating public/private rsa key pair.
Enter file in which to save the key (/d/Users/David/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /d/Users/David/.ssh/id_rsa.
Your public key has been saved in /d/Users/David/.ssh/id_rsa.pub.
The key fingerprint is:
8a:ef:52:86:76:53:b3:ed:d6:54:02:c3:75:9d:94:22 David Moore <david@digitalgenus.com>

David@WHUP ~/.ssh

Copy the contents of  ~/.ssh/id_rsa.pub, paste into <dev>/home/git/.ssh/authorized_keys


On host, tail -f /var/log/secure to watch for errors.
If you see "Authentication refused: bad ownership or modes for file /home/git/.ssh/authorized_keys" (or for the .ssh dir) then you need to change the flags for /home/git/.ssh:

    chmod -R 750 /home/git/.ssh



 ::

    git --bare init
    Initialized empty Git repository in /projects/git/Commons.git/

[David.Moore@maily ~]$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/David.Moore/.ssh/id_rsa):
Created directory '/home/David.Moore/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/David.Moore/.ssh/id_rsa.
Your public key has been saved in /home/David.Moore/.ssh/id_rsa.pub.
The key fingerprint is:
7d:a8:71:23:25:94:b2:8c:7b:1e:29:b7:62:63:fc:a9 David.Moore@maily.digitalgenus.com

[David.Moore@maily ~]$ cat ~/.ssh/id_rsa.pub
ssh-rsa *snip*== David.Moore@maily.digitalgenus.com


Add Git user
------------

Useradd git
Su - git
Mkdir ~/.ssh
exit

Disable shell for Git user
--------------------------

    vim /etc/passwd

Update the shell::

    git:x:520:520::/home/git:/usr/bin/git-shell

Verify:

    $ ssh git@dev.net.gen.nz
    The authenticity of host 'dev.net.gen.nz (60.234.73.20)' can't be established.
    RSA key fingerprint is 0b:78:18:ab:f0:9a:17:ec:6d:6d:7b:d3:1f:ae:04:4f.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'dev.net.gen.nz,60.234.73.20' (RSA) to the list of kn
    own hosts.
    git@dev.net.gen.nz's password:
    fatal: What do you think I am? A shell?
    Connection to dev.net.gen.nz closed.

Add ssh keys to git:

    cat /home/David.Moore/.ssh/id_rsa.pub >> /home/git/.ssh/authorized_keys
