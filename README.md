# ACIT 2420 Assignment 2

# TABLE OF CONTENTS
- Introduction
- Project 1
    - list-packages
    - install-packages
    - config-app-files
    - call-scripts
- Project 2
    - Create-user
- Conclusion

# INTRODUCTION

In this assignment, I was tasked to write two essential shell scripts to automate common system administration tasks:

## Project 1: System Setup Scripts: 
In this script, I created 4 simple scripts to automate software installation and set up symbolic links to configuration files. 
My four scripts include:
List-packages
Install-packages
Config-app-files
call-scripts
This will simplify system configuration and ensure a consistent setup.

## Project 2: User Creation Script: 
In this script, there is automation to adding new users, setting passwords, assigning groups, creating home directories, and configuring shells.
This will help streamline user management and access control.

This assignment can strengthen my shell scripting skills, focusing on command-line options, error handling, and best practices in coding.

# Project 1: 
## Script 1: List-packages

The purpose of this script is to create a file called list-packages.txt that contains a list of specified packages, which are printed to the terminal while being added to their file.

1. #!/bin/bash
- called a "shebang" and indicates the script interpreter.
- /bin/bash specifies that the script should be run in the Bash shell

2. # (comments)
- Lines starting with # are comments. 
- not executed and are used to explain what different parts of the code do.

3. list-packages() { ... }
- list-packages is the name of a function
- () after list-packages concludes that it’s a function.
- { ... } contains the code for the function. 

4. packages=("kakoune" "tmux")
- packages is an array variable that holds a list of package names.
- =("kakoune" "tmux") assigns the values "kakoune" and "tmux" to the packages array.

5. echo "Creating list-packages.txt with these packages:"
- echo is a command that prints text to the terminal.
- "Creating list-packages.txt with these packages:" is the string that echo will print, letting the user know the file is being created.

6. > list-packages.txt
- > is a redirection operator. It writes the output to the specified file.
- list-packages.txt is the filename where the output is directed.
- This command clears any existing content in list-packages.txt or creates the file if it doesn’t exist.

7. for package in "${packages[@]}"; do ... done
- for ... in ...; do ... done is a loop structure in Bash.
- package is a variable that will hold each element in the array during the loop.
- "${packages[@]}" expands to all elements in the packages array.
- do marks the start of the loop’s actions for each package.
- done marks the end of the loop.

8. echo "$package" >> list-packages.txt
- "$package" is the current element from the packages array, representing each package name.
- >> is an append redirection operator, which adds output to the end of a file without overwriting existing content.
- list-packages.txt is the file where each package name is appended.

9. echo "- $package"
- echo prints text to the terminal.
- "- $package" prints a hyphen followed by the current package name, formatted for readability.

10. echo "Package list successfully saved to list-packages.txt"
- Prints a confirmation message to the terminal, indicating that the packages have been saved to the file.

11. list-packages
- This line calls the list-packages function, executing all the code within the function.


