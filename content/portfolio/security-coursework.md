+++
categories = ["coursework"]
coders = []
date = 2019-12-06T00:00:00Z
description = "Performing a Pentest and CTF on a Virtual Machine"
github = ["https://github.com/samrobbins85/NS-Security-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1598985945/undraw_safe_bnk7_dimo8p.svg"
site = ""
title = "Security Coursework"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599475099/Kali_Linux_2.0_wordmark_wsz9aw.svg"
name = "Kali Linux"
url = "https://www.kali.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599475328/nmap-logo-64px_sdhhyu.svg"
name = "nmap"
url = "https://nmap.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599475230/logo_john_the_ripper_newolr.png"
name = "John the Ripper"
url = "https://www.openwall.com/john/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1599475460/Grub_logo_large_s4qmeb.png"
name = "GRUB"
url = "https://www.gnu.org/software/grub/"

+++
For this coursework we were to find vulnerabilities in a system and explain how they could be mitigated, along with solving a murder mystery in the system, which required finding and decoding a range of files.

# Vulnerabilities

## Database file can be opened by any user

There was a file in the database folder named `Database.db`, this could be opened using `sqlite` and with the command `SELECT * FROM Users`, you could find personal information on the users, such as passwords.

This could simply be mitigated by not providing the file to users. Further mitigation though would be to hash passwords and redact credit card information.

## Program vulnerable to buffer overflow

There was a program that could be used to get details about a Bitcoin wallet. However the password input for this was vulnerable to buffer overflow by inserting a password of 64 characters, followed by `\0x01`, this overwrites a the variable to decide if the password is correct from 0 to 1, allowing you to see the private key.

This could be mitigated using `fgets` rather than `gets` as `fgets` allows you to limit the number of characters you take in, for example to 64.

## The compiled executable contains both the password and private key

For the program described above, simply reading it in terminal exposes both the password and private key. The password should be stored as a hash, and the inputted password then hashed and compared to it. The private key should also be encrypted, using the password as the key to decrypt it.

## The standard user can access any user's directory

By simply moving up the filesystem with `cd`, a user can then move into any of the other accounts. This could be mitigated with file permissions by creating a group for each user, and setting that user group to only own the files within their directory. This could be done using `chmod`

## The system passwords for other users can be found

Running `cat /etc/passwd > passwords.txt` allows you to save the `passwd` file for cracking. This can then be transferred to another computer with forensic tools and John the Ripper can be used to get the passwords of all the users. This could be mitigated with `pwconv` to use a shadow file instead of `/etc/passwd`. Also using more secure passwords and hashing algorithms would make it more difficult to reverse the hashes.

## Port 8888 has a root shell

By running `nmap`, it is revealed that port 8888 is open. Getting access to this using `netcat` gives you a shell which it is revealed is a root shell.

This is mitigated by removing a script to open up this shell, which is located at `/etc/init.d/jess.sh`. Using a firewall to ensure no unspecified ports are open would also prevent this happening in the future.

## You can access all files on the system from the website

Using the string `%2e%2e%2f` at the end of the URL you can go up a level in the system, this can be used repeated to move around the filesystem, allowing for use of other exploits detailed here, such as one on `/etc/passwd`

This can be mitigated by using regular expressions to prevent the typing of this or similar strings. The webserver could also be set up inside a chroot jail so that the website views its own directory as the root directory of the computer and can't move outside that.

## You can log in as any user on the website

On the login page providing the username `' OR 1==1 --` and clicking login allows you to log in as root. Prepared statements should be used here to insert the login information so the username and password can't be run as code.

## You can get a root shell from GRUB 

By editing the boot command to run `init=/bin/sh`, you will get a root shell. A password should be added to GRUB to mitigate this.

## The database program can be used to run commands as root

The database program runs the input command you give it, so by running the command `./Backup "; $SHELL # "` it will replace the current command with a command to open the shell as root.

Using the file operations in C would be much better suited here rather than running a system command