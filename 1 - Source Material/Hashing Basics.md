---
sr-due: 2025-05-13
sr-interval: 16
sr-ease: 169
---
2025-08-08 17:55
Status:
Source: [[../3 - Indexes/THM|THM]]
Tags: [[../2 - Tags/Cryptography|Cryptography]]

#review 



A hash value is a fixed-size string or characters that is computed by a hash function. A hash function takes an input of an arbitrary size and returns an output of a fixed length

## Hash Functions

Hash functions have no key, and it is meant to be impossible to go from the output back to the input. A hash function takes some input data of any size and creates a summary or **digest** of the data. Output has a fixed size

The output of a hash function is typically raw bytes, which are then encoded. Common encodings are base64 or hexadecimal. <span style="color:rgb(255, 192, 0)">md5sum</span>, <span style="color:rgb(255, 192, 0)">sha1sum</span>, <span style="color:rgb(255, 192, 0)">sha256sum</span>, and <span style="color:rgb(255, 192, 0)">sha512sum</span> produce their outputs in hexadecimal format.

A server does not store your password, it records the hash value of your password. When you log in, it will calculate the hash value of the password you submitted with the recorded hash value

**Hash collision** occurs when two different inputs produce the same output.  The total number of possible hash values is 2^number_of_bits.

## Insecure Password Storage for Authentication

Insecure practices when it comes to passwords:

- Storing passwords in plaintext
- Storing passwords using a deprecated encryption
- Storing passwords using an insecure hashing algorithm

## Using Hashing for Secure Password Storage

A rainbow table is a lookup table of hashes and plaintext so you can quickly find out what password a user had just from the hash. They sacrifice hard disk space for time

 [CrackStation](https://crackstation.net/) and [Hashes.com](https://hashes.com/en/decrypt/hash) internally use massive rainbow tables to provide fast password cracking for **hashes without salts**. <span style="color:rgb(255, 0, 0)">Do not rely on just tools, use context and research as well</span>

To protect against rainbow table, we use salts. A salt is a randomly generated value stored in the database and should be unique to each user. It is added to either the start or end of the password before its hashed, meaning similar passwords will still have different hashes. 

The following example is good security practices when storing user passwords:

1.  Select a secure hashing function, such as Argon2, Scrypt, Bcrypt, or PBKDF2.
2. We add a unique salt to the password, such as **Y4UV*^(=go_!**
3. Concatenate the password with the unique salt. For example, if the password is **AL4RMc10k**, the result string would be **AL4RMc10kY4UV*^(=go_!**
4. Calculate the hash value of the combined password and salt. In this example, using the chosen algorithm, you need to calculate the hash value of **AL4RMc10kY4UV*^(=go_!.**
5. Store the hash value and the unique salt used (**Y4UV*^(=go_!**).

## Recognizing Password Hashes

 If you find the hash in a web application database, it’s more likely to be MD5 than NTLM 

#### Linux Passwords

On Linux, password hashes are stored in<span style="color:rgb(0, 176, 80)"> /etc/shadow</span>, which is normally only readable by root. They used to be stored in <span style="color:rgb(0, 176, 80)">/etc/passwd</span>, which was readable by everyone. 

The shadow file contains the password information. Each line contains nine fields separated by colon. The first two fields are the login name and the encrypted password. The encrypted password field contains the hashed passphrase with four components: prefix (algorithm id), options (parameters), salt, and hash. It is saved in the format <span style="color:rgb(255, 192, 0)">$prefix$options$salt$hash</span> 

#### MS Windows Passwords

MS Windows passwords are hashed using NTLM; visually identical to MD4 and MD5 hashes, use context 

On MS Windows, password hashes are stored in the SAM (Security Accounts Manager). <span style="color:rgb(0, 176, 240)">Mimikatz</span>  circumvents MS Windows security

#### Password Cracking

You cannot decrypt a password hash, as they are not encrypted. You have to crack the hash by hashing many different inputs.(such as rockyou.txt as it covers many possible passwords), potentially adding the salt if there is one and comparing it to the target hash. Once it matches, you know what the password was. <span style="color:rgb(0, 176, 240)">Hashcat</span> and <span style="color:rgb(0, 176, 240)">John the Ripper</span> are commonly used for these purposes

## Hashing for Integrity Checking

If you put the same data in, you always get the same data out. This means you can use it to check that files haven’t been modified or to ensure that the file you downloaded is identical to the file on the web server.

HMAC is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data

## Conclusion

**Hashing** is a process that takes input data and produces a hash value, a fixed-size string of characters, also referred to as digest.

**Encoding** converts data from one form to another to make it compatible with a specific system.

**Encryption** protects data confidentiality using a cryptographic cipher and a key