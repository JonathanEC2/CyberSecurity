[[../2 - Tags/Networking|Networking]]
**DNS** operates at Layer 7, uses port UDP 53 by default and TCP 53 as a backup

**A record** maps a hostname to one or more IPv4 addresses
**AAAA record** same as A record but for IPv6
**CNAME record** maps a domain name to another domain name
**MX record** mail exchange server

<span style="color:rgb(255, 192, 0)">nslookup</span>  to get these records

## WHOIS

<span style="color:rgb(255, 192, 0)">whois</span> record provides information about the entity that registered a domain name, including name, phone number, email, and address. 

Some whois records are protected by privacy protection

## HTTP(S): Accessing the Web
Defines how your web browser communicates with the web servers.

- **GET** retrieves data from a server
- **POST** submits new data to a server
- **PUT** creates a new resource on the server and updates and overwrites existing information
- **DELETE** deletes a resource

Ports 80,443,8080,8443

<span style="color:rgb(255, 192, 0)">telnet</span> MACHINE_IP 80
<mark style="background: #FFF3A3A6;">GET / HTTP/1.1</mark> and <mark style="background: #FFF3A3A6;">Host: anything </mark>to get the page we wanted

## FTP: Transferring Files

- **USER** input user name
- **PASS** enter password
- **RETR** used to download a file from the FTP server to client
- **STOR** upload a file from client to FTP server

FTP server listens on port 21, transferred on 22

<span style="color:rgb(255, 192, 0)">ftp</span> MACHINE_IP

## SMTP: Sending Email

- **HELO** or **EHLO** established connection 
- **MAIL FROM** specifies the senders email address
- **RCPT TO** specifies recipients email address
- **DATA** indicates that the client will begin sending the content of the email message
- **.** is sent on a line by itself to indicate the end 

<span style="color:rgb(255, 192, 0)">telnet</span> MACHINE_IP 25
## POP3: Receiving Email

- **USER**  **(username)** identifies the user
- **PASS** **(password)** provides the user’s password
- **STAT** requests the number of messages and total size
- **LIST** lists all messages and their sizes
- **RETR** **(message_number)** the specified message
- **DELE**  **(message_number)** marks a message for deletion
- **QUIT** ends the POP3 session applying changes, such as deletions

<span style="color:rgb(255, 192, 0)">telnet</span> MACHINE_IP 110

## IMAP: Synchronizing Email

- **LOGIN  (username) (password)** authenticates the user
- **SELECT (mailbox)** selects the mailbox folder to work with
- **FETCH (mail_number) (data_item_name)** Example **fetch 3 body[]** to fetch message number 3, header and body.
- **MOVE** (sequence_set) (mailbox) moves the specified messages to another mailbox
- **COPY (sequence_set) (data_item_name)** copies the specified messages to another mailbox
- **LOGOUT** logs out


