# Git

## Create an empty branch

```
git checkout --orphan <branch>
git reset --hard
```

## Clear the working directory

``git rm --cached -rf .``

# Configure for Windows

On Windows machine, open up Git Bash

```bash
$ ssh-keygen -t rsa -C "David Moore <david@digitalgenus.com>"
Generating public/private rsa key pair.
Enter file in which to save the key (/d/Users/David/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /d/Users/David/.ssh/id_rsa.
Your public key has been saved in /d/Users/David/.ssh/id_rsa.pub.
The key fingerprint is:
xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx David Moore <david@digitalgenus.com>

David@WHUP ~/.ssh
```

Copy the contents of  `~/.ssh/id_rsa.pub,` paste into `<dev>/home/git/.ssh/authorized_keys`

On host, `tail -f /var/log/secure` to watch for errors.

If you see "`Authentication refused: bad ownership or modes for file /home/git/.ssh/authorized_keys`" (or for the `.ssh` dir) then you need to change the flags for `/home/git/.ssh`:

```bash
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
xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx David.Moore@maily.digitalgenus.com

[David.Moore@maily ~]$ cat ~/.ssh/id_rsa.pub
ssh-rsa *snip*== David.Moore@maily.digitalgenus.com
```

## Add Git user
```bash
Useradd git
Su - git
Mkdir ~/.ssh
exit
```

## Disable shell for Git user
```bash
    vim /etc/passwd
```

Update the shell:

```bash
    git:x:520:520::/home/git:/usr/bin/git-shell
```

Verify:

```bash
    $ ssh git@dev.net.gen.nz
    The authenticity of host 'dev.net.gen.nz (60.234.73.20)' can't be established.
    RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'dev.net.gen.nz,x.x.x.x' (RSA) to the list of kn
    own hosts.
    git@dev.net.gen.nz's password:
    fatal: What do you think I am? A shell?
    Connection to dev.net.gen.nz closed.
```

Add ssh keys to git:

```bash
    cat /home/David.Moore/.ssh/id_rsa.pub >> /home/git/.ssh/authorized_keys
```