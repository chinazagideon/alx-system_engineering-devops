## SHELL COMMANDS

### Create a script that creates an alias.
#### Script file: 0-alias
#### alias - keyword
#### <code>variable_name</code> - new command alias
#### <code>command</code> - assign commands


### Create a script that prints hello user, where user is the current Linux user
#### Script file: 1-hello_you
#### echo - keyword to print any parameter assigned 
#### $USER - reserved shell keyword for current user

### Add /action to the PATH. /action should be the last directory the shell looks into when looking for a program.
#### Script file: 2-path
#### $PATH - shell variable with recognised command paths

### Count Directories in PATH
#### Script file: 3-paths
#### echo '$PATH' - list directories as string
#### <code>tr ':' '\n'</code> will translate every colon in the PATH into a newline character. This effectively puts each directory on a new line.
#### <code> wc -l </code> then counts the number of lines, which gives you the total number of directories.


#### List ENV Variables
#### Script file: 4-global_variables
#### printenv - shell keyword