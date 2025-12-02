---
sr-due: 2025-05-18
sr-interval: 3
sr-ease: 130
---
#offensive_security
#review 

[[../2 - Tags/Cryptography|Cryptography]]


## Basic Terms
#### What are Hashes?

 A hash is a way of taking a piece of data of any length and representing it in another form that is a fixed length. This masks the original value of the data. Hashing functions are designed as one-way functions. In other words, it is easy to calculate the hash value of a given input; however, it is a difficult problem to find the original input given the hash value. By "difficult", we mean that it is computationally infeasible.

#### Where John Comes in

Even though the algorithm itself is not feasibly reversible. That doesn't mean that cracking the hashes is impossible. If you have the hashed version of a password, for example- and you know the hashing algorithm- you can use that hashing algorithm to hash a large number of words, called a dictionary. You can then compare these hashes to the one you're trying to crack, to see if any of them match. If they do, you now know what word corresponds to that hash- you've cracked it!

## Cracking Basic Hashes

#### John Basic Syntax
?
<span style="color:rgb(255, 192, 0)">john</span> : invokes john the RIpper program
{<span style="color:rgb(0, 176, 240)">OPTIONS</span>}: specifies the options you want to use
{<span style="color:rgb(0, 176, 80)">FILE_PATH</span>}: file containing the hash you’re trying to crack

#### Automatic Cracking

<span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--wordlist</span>={<span style="color:rgb(0, 176, 80)"> path to word list</span>} {<span style="color:rgb(0, 176, 80)">path to file</span>}

**Example Usage:**
	<span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--wordlist</span>=<span style="color:rgb(0, 176, 80)">/usr/share/wordlists/rockyou.txt</span> hash_to_crack.txt

#### Identifying Hashes

[Hash identifier website](https://hashes.com/en/tools/hash_identifier)

<span style="color:rgb(217, 145, 204)">hash-identifier</span>, a Python tool that is super easy to use and will tell you what different types of hashes the one you enter is likely to be, giving you more options if the first one fails. To use hash-identifier, you can use <span style="color:rgb(255, 192, 0)">wget</span> or <span style="color:rgb(255, 192, 0)">curl</span> to download the Python file hash-id.py from its GitLab page. Then, launch it with <span style="color:rgb(255, 192, 0)">python3 hash-id.py</span> and enter the hash you’re trying to identify.

Once you have identified the hash that you're dealing with, you can tell john to use it while cracking the provided hash using the following syntax:

#### Format-Specific Cracking

Once you have identified the hash that you’re dealing with, you can tell John to use it while cracking the provided hash using:

<span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--format</span>={format} <span style="color:rgb(0, 176, 240)">--wordlist</span>={<span style="color:rgb(0, 176, 80)">path to wordlist</span>}

When you are telling john to use formats, if you're dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with raw- to tell john you're just dealing with a standard hash type, though this doesn't always apply. To check if you need to add the prefix or not, you can list all of John's formats using <span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--list</span>=formats and either check manually, or grep for your hash type using something like <span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--list</span>=formats | <span style="color:rgb(255, 192, 0)">grep</span> <span style="color:rgb(0, 176, 240)">-iF</span> "md5".


## Cracking Windows Authentication Hashes

Authentication hashes are the hashed versions of passwords that are stored by operating systems; it is sometimes possible to crack them using brute-force methods. To get your hands on these hashes, <span style="color:rgb(255, 0, 0)">you must often already be a privileged user</span>

You can acquire NTHash/NTLM hashes by dumping the **SAM** database on a Windows machine, by using a tool like Mimikatz or from the Active Directory database: NTDS.dit. You may not have to crack the hash to continue privilege escalation- as you can often conduct a "pass the hash" attack instead, but sometimes hash cracking is a viable option if there is a weak password policy.

  
## Cracking /etc/shadow Hashes

The <span style="color:rgb(0, 176, 80)">/etc/shadow</span> file is the file on Linux machines where password hashes are stored. It also stores other information, such as the date of last password change and password expiration information. <span style="color:rgb(255, 0, 0)">This file is usually only accessible by the root user</span>- so in order to get your hands on the hashes you must have sufficient privileges

John can be very particular about the formats it needs data in to be able to work with it, for this reason- <span style="color:rgb(255, 0, 0)">in order to crack /etc/shadow passwords, you must combine it with the /etc/passwd file in order for John to understand the data it's being given</span>. To do this, we use a tool built into the John suite of tools called unshadow. The basic syntax of unshadow is as follows:

<span style="color:rgb(255, 192, 0)">unshadow</span> {<span style="color:rgb(0, 176, 80)">path to passwd</span>} {<span style="color:rgb(0, 176, 80)">path to shadow</span>}

Example Usage:
<span style="color:rgb(255, 192, 0)">unshadow</span> local_passwd local_shadow > unshadowed.txt

## Single Crack

Single Crack mode ;; In this mode, John uses only the information provided in the username, to try and work out possible passwords heuristically, by slightly changing the letters and numbers contained within the username.
#### Word Mangling

Consider the username “Markus”.

Some possible passwords could be:

Markus1, Markus2, Markus3 (etc.)
MArkus, MARkus, MARKus (etc.)
Markus!, Markus$, Markus* (etc.)

#### GECOS

 <span style="color:rgb(0, 176, 80)">/etc/shadow</span> and <span style="color:rgb(0, 176, 80)">/etc/passwd</span> has fields separated by a colon ":". The fifth field in the user account record is the **GECOS** field.  John can take information stored in those records, such as full name and home directory name to add in to the wordlist it generates when cracking<span style="color:rgb(0, 176, 80)"> /etc/shadow </span>hashes with single crack mode

#### Using Single Crack Mode

<span style="color:rgb(255, 192, 0)">john</span> <span style="color:rgb(0, 176, 240)">--</span><span style="color:rgb(0, 176, 240)">single</span> <span style="color:rgb(0, 176, 240)">--format</span>={format} {path to file}

If you’re cracking hashes in single crack mode, you need to change the file format that you’re feeding John for it to understand what data to create a wordlist from.<span style="color:rgb(255, 0, 0)"> You do this by prepending the hash with the username that the hash belongs to</span>
## Cracking a Password Protected Zip File

Similarly to the unshadow tool that we used previously, we're going to be using the zip2john tool to convert the zip file into a hash format that John is able to understand, and hopefully crack. The basic usage is like this:

<span style="color:rgb(255, 192, 0)">zip2john</span> {<span style="color:rgb(0, 176, 240)">options</span>} {zip file} > {output file}

**Example Usage**
	<span style="color:rgb(255, 192, 0)">zip2john</span> zipfile.zip > zip_hash.txt

<span style="color:rgb(255, 192, 0)">rar2john</span> {<span style="color:rgb(0, 176, 240)">options</span>} {rar file} > {output file}


  
## Cracking SSH Key Passwords

Unless configured otherwise, you authenticate your SSH login using a password. However, you can configure key-based authentication, which lets you use your private key, id_rsa, as an authentication key to login to a remote machine over SSH.

#### SSH2John

converts the id_rsa private key into a hash format that John can work with

if you don’t have ssh2john installed, you can use <span style="color:rgb(217, 145, 204)">ssh2john.py</span>, located in the <span style="color:rgb(0, 176, 80)">/opt/john/ssh2john.py</span>

- <span style="color:rgb(255, 192, 0)">ssh2john</span> {id_rsa private key file{} > {output file}
- Feed the output of this file into regular john

