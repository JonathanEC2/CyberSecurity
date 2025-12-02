#linux


## SSH
SSH is;; a protocol between devices in an encrypted form. It is the common means of connecting and interacting with the CLI of a remote Linux device

The command to log in to a remote machine is ssh and then the username of the account, @ the IP address of the machine.<span style="color:rgb(255, 192, 0)"> ssh tryhackme@10.10.38.244</span> 

-i identity_file A file from which the identity key (private key) for public key authentication is read ;;<span style="color:rgb(255, 192, 0)">ssh</span> <span style="color:rgb(0, 176, 240)">-i</span> <span style="color:rgb(0, 176, 80)">/path/to/keyfile</span> username@server
## Filesystem Interaction Continued


| Command | Full Name      | Purpose                      |
| ------- | -------------- | ---------------------------- |
| touch   | touch          | Create file                  |
| mkdir   | make directory | Create a folder              |
| cp      | copy           | Copy a file or folder        |
| mv      | move           | Move a file or folder        |
| rm      | remove         | Remove a file or folder      |
| file    | file           | Determine the type of a file |
| nano    | nano           | Create or edit a file        |

## Permissions 101 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdnHaFWoYM2eBj-I5Q2PMfcdAfwJfRmtLLGLQEusH0wg1czENlpo7xk8a-geypFu-qk09Ic27Rr1pLHBdQbNhttVMF7O4C997X98A_at5GJSCRF28UsmXI-fSiQzbGqPZFmk9-vGujwN50qxmbwa7cTAMAc?key=TfE_5MxENIjRvhHpOZCQ2w)

  
## Common Directories
<span style="color:rgb(0, 176, 80)"> /etc</span>;; a commonplace location to store system files that are used by your operating system. 
<span style="color:rgb(0, 176, 80)">/var</span>;; stores data that is frequently accessed or written by services or applications running on the system.
<span style="color:rgb(0, 176, 80)">/root</span>;; Unlike the /home directory, the /root folder is the home for the "root" system user.
<span style="color:rgb(0, 176, 80)">/tmp </span>;; is volatile and is used to store data that only needs to be accessed once or twice.

<u> Go through this room again once or twice to gain some familiarity with the concepts. After all, practice makes perfect! </u>