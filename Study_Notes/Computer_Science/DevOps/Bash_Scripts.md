# Script File Structure
> [!important]
> The first line of the script should be `#!` followed by the absolute path of the interpreter.
> - If you want your script to be executed by python, `#!<path_to_python.exe>` 
> - If you want your script to be executed by bash, `#!/bin/bash`



# Quotes
## Double Qoutes
> [!def]
> `"$VAR \$"`, 在`double quotes`中的所有`$VAR`都会被自动替换成变量值。
> 
> 如果我们要打印`$`字符而不是想让他自动转义，则需要`\$`
```bash
>>> SKILL=DevOps
>>> echo "I have $SKILL skill"
>>> I have DevOps skill
>>> echo "I have $SKILL skill, which pays me \$90000 a year"
>>> I have DevOps skill, which pays me $90000 a year
```

## Single Qoutes
> [!def]
> 在`single quotes`中不会发生转义现象，所见即所得。
```bash
>>> SKILL=DevOps
>>> echo 'I have $SKILL skill'
>>> I have $SKILL skill
```


## Backtick Quotes - Command Substitution
> [!def]
> 在`backtick quotes`中可以编写指令，或自动获取指令执行的结果。有两种替换方式:
> - VarName=\`Command\`
> - VarName=\$(Command)
```bash
>>> SKILL=`uptime`
>>> echo $SKILL
>>> execution result of uptime
```


## Example Scripts
### Fetch free memory info
> [!code]
```bash
FREERAM=`free -h | grep Mem | awk '{print $4}'`
```



# Exporting Variables
> [!important]
> The lifetime of the variable defined in the shell by default only last the session of this bash. If you swith to another bash or child bash, the variable is gone.
> 
> If you want to make the variable permanent, there are three ways:
> - If you want the variable to be permanent and global to all users(including root), `sudo -i` then append `export VarName=VarValue` to the `/etc/profile` file.
> - If you want the variable to be permanent and exclusive to a sepcific user, append `export VarName=VarValue` to the `/.bashrc` file and source it if you want it to take effect immediately, otherwise everytime you open a new bash it will automatically be sourced.



# User Input
> [!def]
> - `read -p "Username:" VAR`, `p` means prompt message.
> - `read -sp "Password: " PASS` , `s` means suppressed. Even ifuser input something, it won't be shown on the screen.


# Branch-Decision Making
## Syntax
> [!code]
> `indentation` is optional here
```bash
#!/bin/bash
if [ $NUM -gt 100]
then 
	echo "We have entered an IF block."
	sleep 3
	echo "Your number is greater than 100."
	echo
	date
else
	echo "You have entereed number less than 100."
fi

echo "Script execution completed successfully"
```


## Example Scripts
> [!code]
> - `grep` searches for lines that contains the keyword(argument of `grep`)
> - `grep -v LOOPBACK` inverts the match(`-v` removes lines that contain "LOOPBACK")
> - `-c` tells grep to count the number of matching lines, instead of showing them
```bash
#!/bin/bash

value=$(ip addr show | grep -v LOOPBACK | grep -ic mtu)$

if [$value -eq 1] 
then
	echo "1 active network driver found."
elif [$value -gt 1] 
then
	echo "More than 1 active network driver found."
else 
	echo "No active multiple active interface found."
```



# Scripts for Monitor
> [!code]
> - `>` redirects stdout to a file, overwriting it
> - `>>` appends stdout to a file
> - `&>` redirects both stdout and stderr to a file
> 
> ![](Bash_Scripts.assets/4f4fc6b8f0be635f5fea8a0f2c062a37_MD5.jpeg)
```bash
#!/bin/bash

ls /var/run/httpd/httpd.pid &> /dev/null

# $? will be non 0 if the previous command failed to execute successfully
if [$? -eq 0]
then
	echo "Httpd process is running."
else
	echo "Httpd process is NOT Running."
	echo "Starting the process"
	systemctl start httpd
	if [$? -eq 0]
	then
		echo "Process started successfully."
	else 
		echo "Process starting failed, contact the admin."
	fi
fi
```



# Loops
## For Loop Examples
> [!code] Code Example 1
```bash
#!/bin/bash

for VAR1 in java .net python ruby php
do
	echo "Looping..."
	echo "#############################"
	echo "Value of VAR1 is $VAR1"
	echo "#############################"
	date
	echo
done
```

> [!code] Code Example 2
```bash
#!/bin/bash

# This is actually valid syntax
echo "Bash Version ${BASH_VERSION}$"
# $BASH_VERSION is also valid

MYUSERS="alpha beta gamma"

for usr in $MYUSERS
do
	echo "Adding user $usr."
	useradd $usr
	id $usr
	echo "##############################"
done
```

> [!code] Code Example 3
```bash
#!/bin/bash

for (( c=1; c<=5; c++ ))
do
	echo "Welcome $c times"
done
```



## While Loop Examples
> [!code] Code Example 4
```bash
#!/bin/bash

counter=0

# Be careful there should be whitespace before and after the loop condition.
while [ $counter -lt 5 ]
do 
	echo "Looping"
	echo "Value o counter is $counter."
	counter=$(($counter + 1))
done
```



# Remote Command Execution




# SSH Key Exchange









