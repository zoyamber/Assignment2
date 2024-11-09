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

**1. #!/bin/bash**
- called a "shebang" and indicates the script interpreter.
- /bin/bash specifies that the script should be run in the Bash shell


**2. #comments**
- Lines starting with # are comments. 
- not executed and are used to explain what different parts of the code do.


**3. list-packages() { ... }**
- list-packages is the name of a function
- () after list-packages concludes that it’s a function.
- { ... } contains the code for the function. 


**4. packages=("kakoune" "tmux")**
- packages is an array variable that holds a list of package names.
- =("kakoune" "tmux") assigns the values "kakoune" and "tmux" to the packages array.


**5. echo "Creating list-packages.txt with these packages:"**
- echo is a command that prints text to the terminal.
- "Creating list-packages.txt with these packages:" is the string that echo will print, letting the user know the file is being created.


**6. > list-packages.txt**
- > is a redirection operator. It writes the output to the specified file.
- list-packages.txt is the filename where the output is directed.
- This command clears any existing content in list-packages.txt or creates the file if it doesn’t exist.


**7. for package in "${packages[@]}"; do ... done**
- for ... in ...; do ... done is a loop structure in Bash.
- package is a variable that will hold each element in the array during the loop.
- "${packages[@]}" expands to all elements in the packages array.
- do marks the start of the loop’s actions for each package.
- done marks the end of the loop.


**8. echo "$package" >> list-packages.txt**
- "$package" is the current element from the packages array, representing each package name.
- >> is an append redirection operator, which adds output to the end of a file without overwriting existing content.
- list-packages.txt is the file where each package name is appended.


**9. echo "- $package"**
- echo prints text to the terminal.
- "- $package" prints a hyphen followed by the current package name, formatted for readability.


**10. echo "Package list successfully saved to list-packages.txt"**
- Prints a confirmation message to the terminal, indicating that the packages have been saved to the file.


**11. list-packages**
- This line calls the list-packages function, executing all the code within the function.


## Script 2: install-packages

This Bash script is designed to check if it’s being run as root, ensure a package list file exists, and install each package listed in that file, printing any errors if a package fails to install

**1. check-root() {**
- check-root is the name of a function that checks if the script is run as root.


**2. if [[ $EUID -ne 0 ]]; then**
- if begins a conditional statement.
- [[ $EUID -ne 0 ]] checks if the effective user ID ($EUID) is not equal (-ne) to 0.
- 0 is the user ID of the root user, so this checks if the script is not run as root.

  
**3. echo "this script can only be run as root"**
- echo prints text to the terminal.


**4. exit 1**
- exit stops the script.
- 1 is an exit status code that signals an error.


**5. check-package-exists() {**
- Defines a function called check-package-exists that checks for the existence of a
- package list file.


**6. if [[ ! -f list-packages ]]; then**
- if begins a conditional statement.
- [[ ! -f list-packages ]] checks if the file list-packages does not (!) exist (-f).
- list-packages is the expected name of the package list file.


**7. install-package() {**
- Defines a function called install-package that installs packages listed in list-packages.txt.


**8. while read -r package; do**
- while initiates a loop that will run for each line in the package file.
- read -r package reads each line from list-packages.txt into a variable called package.
- do indicates the start of the loop’s body.


**9. if [[ -n "$package" ]]; then**
- Begins an if statement.
- [[ -n "$package" ]] checks if package is non-empty, meaning it skips any blank lines.


**10. pacman -S --noconfirm "$package" || echo "Failed to install $package"**
- pacman is the package manager command for Arch Linux.
- -S installs a package.
- --noconfirm skips confirmation prompts during installation.
- "Failed to install $package" is printed if the installation fails, due to the || operator, which only executes the second command if the first fails.


**11. done < list-packages.txt**
- done ends the while loop.
< list-packages.txt provides list-packages.txt as the input source for the while loop.


**12. check-root**
- Calls the check-root function to ensure the script is run as root.


**13. check-package-exists**
- Calls the check-package-exists function to ensure the list-packages file exists.


**14. install-package**
- Calls the install-package function to install each package listed in list-packages.txt


## Script 3: app-config-files


This script sets up symbolic links for configuration files, allowing users to easily configure their environment by linking files from a central directory to standard locations in the home directory. This simplifies setup and management of dotfiles across systems


**1. config_dir=$(pwd)**
- config_dir is a variable assigned the output of the pwd command.
- $(pwd) captures the current directory path where the script is being run.


**2. dest_link=$1**
- dest_link is assigned the value of the first argument passed to the script.
- $1 is a positional parameter representing the first command-line argument.

**Function to Create a Symbolic Link:**


**3. create_sym_link()**
- create_sym_link is the function name for creating symbolic links.

  
**4. if [[ -e "$config_dir" ]]; then**
- Checks if the path specified in config_dir exists (-e stands for "exists").


**5. if ln -sf "$config_dir" "$dest_link"; then**
- Creates a symbolic link from config_dir to dest_link using ln -sf.
- -s makes a symbolic link, and -f forces it, replacing any existing file at dest_link.


**6. ln -sf "$config_dir/bin/sayhi" ~/bin/sayhi**
- Links the sayhi script from config_dir/bin to ~/bin/.


**7. ln -sf "$config_dir/bin/install-fonts" ~/bin/install-fonts**
- Links install-fonts from config_dir/bin to ~/bin/.


**8. mkdir -p ~/.config**
- Creates the ~/.config directory if it doesn’t already exist.
- -p ensures no error if the directory already exists.


**9. ln -sf "$config_dir/config/kak" ~/.config/kak**
- Links the kak configuration from config_dir/config to ~/.config.


**10. ln -sf "$config_dir/config/tmux" ~/.config/tmux**
- Links the tmux configuration from config_dir/config to ~/.config.


**11. ln -sf "$config_dir/home/bashrc" ~/.bashrc**
- Links bashrc from config_dir/home to the user’s home directory as ~/.bashrc.


**12. echo "symbolic links were created successfully!"**
- Prints a success message after all symbolic links have been created.


## script4: call-scripts






