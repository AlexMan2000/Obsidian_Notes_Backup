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

## Backtick Quotes
> [!def]
> 在`backtick quotes`中可以编写指令，或自动获取指令执行的结果。
```bash
>>> SKILL=`uptime`
>>> echo $SKILL
>>> execution result of uptime
```


