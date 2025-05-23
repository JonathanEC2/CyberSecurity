#linux

# Linux Fundamentals 3

## Terminal Text Editors

<span style="color:rgb(0, 176, 240)">nano</span>
<span style="color:rgb(0, 176, 240)">VIM</span>  is a much more advanced text editor. [Cheat Sheet](https://vim.rtorr.com/)
## General/Useful Utilities

Wget ;; allows you to download files from the web via HTTP
scp ;; command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.

| Variable                                                    | Value           |
| ----------------------------------------------------------- | --------------- |
| The IP address of the remote system                         | 192.168.1.30    |
| User on the remote system                                   | ubuntu          |
| Name of the file on the local system                        | important.txt   |
| Name that we wish to store the file as on the remote system | transferred.txt |
Copy an example file from our machine to a remote machine:
<span style="color:rgb(255, 192, 0)">scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt</span>

Reverse this and layout the syntax for using scp to copy a file from a remote computer that we're not logged into:
<span style="color:rgb(255, 192, 0)">scp ubuntu@192.168.1.30:/home/ubuntu/transferred.txt important.txt </span>

##### Serving Files from Your Host

python3 http.server turns your computer into a quick and easy web server that you can use to serve your own files,  where they can then be downloaded by another computing using commands such as <span style="color:rgb(0, 176, 240)">curl</span> and <span style="color:rgb(0, 176, 240)">wget</span>

- Host server;; <span style="color:rgb(255, 192, 0)">python3 -m  http.server</span>
- DL files: <span style="color:rgb(255, 192, 0)">wget http://[IP address]:8000/[file name]</span>

<u>You must know the exact name and location of the file that you wish to use.</u>

## Processes 101

<span style="color:rgb(255, 192, 0)">ps</span> ;; provides a list of the running processes
<span style="color:rgb(255, 192, 0)">top</span> ;; gives you real-time statistics about the processes running on your system
<span style="color:rgb(255, 192, 0)">ps</span> aux ;; to see the processes run by other users and those that don't run from a session 

<span style="color:rgb(255, 192, 0)">kill</span> command and the associated PID that we wish to kill
- SIGTERM - Kill the process, but allow it to do some cleanup tasks beforehand
- SIGKILL - Kill the process - doesn't do any cleanup after the fact
- SIGSTOP - Stop/suspend a process

##### How do Processes Start?
?
The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. Think of it as splitting your computer up into slices -- similar to a cake. Processes within that slice will have access to a certain amount of computing power, however, it will be a small portion of what is actually available to every process overall.

<span style="color:rgb(255, 192, 0)">Systemctl</span> ;; allows us to interact with the systemd process/daemon  <span style="color:rgb(255, 192, 0)">systemctl</span> <span style="color:rgb(0, 176, 240)">option</span>:

- Start
- Stop
- Enable
- Disable

Rather than relying on the & operator to background a process, we can use <span style="color:rgb(255, 192, 0)">Ctrl + Z </span>on our keyboard

<span style="color:rgb(255, 192, 0)">fg</span> ;; command is being used to bring the background process back into use on the terminal

## Maintaining Your System: Automation

A crontab is simply a special file with formatting that is recognized by the cron process to execute each line step-by-step. Crontabs require 6 specific values:

|   |   |
|---|---|
|Value|Description|
|MIN|What minute to execute at|
|HOUR|What hour to execute at|
|DOM|What day of the month to execute at|
|MON|What month of the year to execute at|
|DOW|What day of the week to execute at|
|CMD|The actual command that will be executed.|

Let's use the example of backing up files. You may wish to backup "cmnatic"'s  "Documents" every 12 hours. We would use the following formatting: 

<span style="color:rgb(255, 192, 0)">0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/</span>

[Crontab Generator](https://crontab-generator.org/) 

## Maintaining Your System: Package Management

Additional repositories can be added by using the <span style="color:rgb(0, 176, 240)">add-apt-repository</span>. Normally we use the apt command to install software onto our Ubuntu system

A good practice is to have a separate file for every different community/3rd party repository that we add. After we have added this entry, we need to update apt to recognize this new entry -- this is done using the apt update command

Removing packages is as easy as reversing. This process is done by using the add-apt-repository --remove ppa:PPA_Name/ppa command or by manually deleting the file that we previously added to. Once removed, we can just use apt remove [software-name-here] i.e. apt remove sublime-text
 
## Maintaining Your System: Logs

Services and logs are a great way to monitor and protect the health of your system. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:

- access log
- error log
