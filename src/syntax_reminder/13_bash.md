<!-- markdownlint-disable MD001 -->

# Bash

- [Shebang](#shebang)
- [Print](#print)
- [Input](#input)
- [Variables](#variables)
- [Commands](#commands)
- [Functions](#functions)
- [Control flow](#control-flow)
- [Error handling](#error-handling)

### Shebang

```bash
#!/bin/bash

# alternative:
#!/usr/bin/env bash
```

### Print

```bash
$name="world"
echo "hello $name"

printf "hello %s \n" world
```

### Input

```bash
echo -e "Please enter your name: "
read name
echo "Nice to meet you $name"
```

### Variables

```bash
# Use letters, numbers and underscores for variable names

my_variable=my_value
my_variable='hello world' # single quotes are not interpreted
my_variable="hello $name" # double quotes allow substitution
my_dir=/home/dev
variable=$( my_command ) # save output of command into a variable
timestamp=$(date +"%Y-%m-%d_%H:%M:%S")

$my_dir 
${my_dir} # variable expansion
${#my_string} # string length
${my_var=default_value}
${my_var1?my_var2} # use my_var2 if my_var1 is null

a{d,c,b}e # brace expansion: "ade ace abe"

# environment variable (export to all child processes created from that shell)
export my_var1="${my_var2}" 

# positional parameters
$0 # name of the script
$1 - $9 # first 9 arguments of the script
$# # number of arguments passed to the script
$? # the exit status of the most recently run process
$$ # the process ID of the current script
$USER # the username of the user running the script
$HOSTNAME # the hostname of the machine the script is running on
$SECONDS # the number of seconds since the script was started
$RANDOM # return a random number
$LINENO # returns the current line number in the script
```

### Commands

```bash
# commands separated by ";" are executed sequentially
command1; command2; command3

# commands separated by "&" are executed in parallel (and in background)
command2 & command2 & command3

# command2 is executed iff command1 returns an exit status of zero
command1 && command2

# command2 is executed iff command1 returns a non-zero exit status
command1 || command2

# execute in subshell
( cd directory && command1 )

# If the value of the expression is non-zero, the return status is 0; otherwise the return status is 1
(( expression ))

# Return a status of 0 or 1 depending on the evaluation of the conditional expression
# Word splitting and pathname expansion are not performed
[[ expression ]]
```

### Functions

```bash
function my_function {
    # commands

    # optional return status
    return my_return_status
}

# alternative syntax
my_function () {
    # commands
}

# call function
my_function my_arg1 my_arg2
```

### Control flow

```bash
# arithmetic operators inside [[ ]]: 
-eq, -ne, -lt, -gt, -le, -ge

# arithmetic operators inside (( )):
==, !=, <, >, <=, >=

# if-else
if (( $a < $b )); then
    # statement
elif (( $a == $b )); then
    # statement
else 
    # statement
fi

# for loop
for i in {1..3}
do
    # statement
done

# directory exists
if [[ -d $directory ]]; then
    # statement
fi

# file exists
if [[ -f $directory ]]; then
    # statement
fi

# case
read -p "Continue (yes or no)?" choice
case "$choice" in 
  yes ) 
    # statements
    ;;
  no )
    # statements
    ;;
  * ) 
    # statements
    ;;
esac
```

### Error handling

```bash
exit N
# N = 0: executed successfully
# N != 0: error occured
```
