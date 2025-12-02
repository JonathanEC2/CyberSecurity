

## Types of Linux Shells

<span style="color:rgb(0, 176, 80)">/etc/shells</span> contains all installed shells on a Linux system; to switch between shells, type in the shell name you wish to use

<span style="color:rgb(255, 192, 0)">chsh -s SHELL_PATH </span>to permanently change default shell

| Feature             | Bash                                                         | Fish                                                                           | Zsh                                                                                  |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| Full Name           | The full form of Bash is Bourne Again Shell.                 | The full form of Fish is Friendly Interactive Shell.                           | The full form of Zsh is Z Shell.                                                     |
| Scripting           | compatible scripting with extensive documentation available. | It has limited scripting features as compared to the other two shells.         | Iexcellent level of scripting,  capabilities of Bash shell with some extra features. |
| Tab completion      | It has a basic tab completion feature.                       | advanced tab completion by giving suggestions based on your previous commands. | Its tab completion capability can be extended heavily by using plugins.              |
| Customization       | Basic level of customization.                                | offers some good customization through interactive tools.                      | Advanced customization through oh-my-zsh framework.                                  |
| User friendliness   | It is less user-friendly, widely used shell,                 | most user-friendly shell.                                                      | I user-friendly with proper customization.                                           |
| Syntax highlighting | Not available                                                | Built-in                                                                       | can be used with this shell by introducing some plugins.                             |

## Shell Scripting and Components

Shell script is nothing but a set of commands 

Every script should start from shebang. Shebang is a combination of some characters that are added at the beginning of a script, starting with <span style="color:rgb(255, 0, 0)">#!</span> followed by the name of the interpreter to use while executing the script. EX: <span style="color:rgb(255, 0, 0)">#!/bin/bash</span> 

### Variables
<span style="color:rgb(255, 192, 0)">echo</span> displays a string on screen
<span style="color:rgb(255, 192, 0)">read</span> is used to take input from the user
<span style="color:rgb(255, 192, 0)">$</span> displays variable value

<span style="color:rgb(255, 192, 0)">chmod +x SCRIPT_FILE</span> gives script executing permissions

### Loops

```shell
for i in {1..10}; //iterates from 1-10
do                //indicates start of loop code
echo $i
done              //indicates end
```

### Conditional Statements
```shell
# Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi       //ends loop
```

### Comments

use <span style="color:rgb(255, 192, 0)">#</span> 