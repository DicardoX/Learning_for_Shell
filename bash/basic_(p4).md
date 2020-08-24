# Bash基础知识(4)

------

[整理自：Bash Examples](https://linuxhint.com/30_bash_script_examples/)

## 文件操作

### 1. 文件读取：

  - Case 1: 从命令行读取文件内容：
  
  ```
    while read line; do echo $line; done < weekday.txt  
  ```
  
注意，文件每行内容存储在`$line`变量中。
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % while read line; do echo $line; done < weekday.txt
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
    Sunday
  ```
  
  - Case 2: 使用`script`读取文件内容：
  
  ```
    filename='weekday.txt'
    n=1
    while read line; do
	    echo "Line No. $n : $line"
	    n=$((n+1))
    done < $filename
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Line No. 1 : Monday
    Line No. 2 : Tuesday
    Line No. 3 : Wednesday
    Line No. 4 : Thursday
    Line No. 5 : Friday
    Line No. 6 : Saturday
    Line No. 7 : Sunday

  ```
  
  - Case 3: 通过命令行传递文件名，读取文件：
  
  ```
    filename=$1
    while read line; do
	    echo $line
    done < $filename
    
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh weekday.txt
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
    Sunday

  ```
  
  - Case 4: 读取文件，忽略反斜杠`\`转义（直接打印`\`）：
  
  ```
    while read -r line; do
      echo $line
    done < weekday.txt
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh weekday.txt
    Monday \\
    Tuesday \\
    Wednesday \\
    Thursday \\
    Friday \\
    Saturday \\
    Sunday \\

  ```
  
---------

### 2. 文件删除：

  ```
    echo "Enter filename to remove"
    read filename
    rm -i $filename                           # -i option is used to get permission from the user
  ```
 
### 3. 文件内容增补：

  ```
    echo "Before appending the file"
    cat weekday.txt
    
    echo "Learning Bash" >> weekday.txt
    echo "After appending the file"
    cat weekday.txt
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Before appending the file
    Monday 
    Tuesday 
    Wednesday 
    Thursday 
    Friday 
    Saturday 
    Sunday 
    After appending the file
    Monday 
    Tuesday 
    Wednesday 
    Thursday 
    Friday 
    Saturday 
    Sunday 
    Learning Bash                         # Create a new line
    
  ```
  
### 4. 测试文件是否存在：

  ```
    filename=$1
    if [ -f "$filename" ]; then
      echo "File exists"
    else
      echo "File does not exist"
    fi
    
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh weekday.txt
    File exists
    dicardo@MacBook-Pro desktop % bash Try.sh weekend.txt
    File does not exist
  ```
  
----------

## 发送邮件

  ```
    # Way 1
    Recipient="1106828059@qq.com"
    Subject="Greeting"
    Message="Welcome to our site"
    `mail -s $Subject $Recipient <<< $Message`

    # Way 2
    echo "hello world" | mail -s test 1106828059@qq.com
  
  ```

----------

## 获取、解析当前时间

  ```
    Year=`date +%Y`
    Month=`date +%m`
    Day=`date +%d`
    Hour=`date +%H`
    Minute=`date +%M`
    Second=`date +%S`
    echo `date`
    echo "Current Date is: $Day-$Month-$Year"
    echo "Current Time is: $Hour:$Minute:$Second"
    
  ```
  
  &emsp; Output:
  
  ```
    dicardo@MacBook-Pro desktop % bash Try.sh 
    2020年 8月24日 星期一 18时01分54秒 CST
    Current Date is: 24-08-2020
    Current Time is: 18:01:54
    
  ```
  
-----------

## Wait指令

  ```
    echo "Wait command" &
    process_id=$!
    echo "Current process ID is $process_id"
    wait $process_id                            # Wait until Process $process_id is completed
    echo "Exited with status $?"
    
  ```
  
  &emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Current process ID is 1149
    Wait command
    Exited with status 0
    
  ```
  
## Sleep指令

  - Case 1: 以秒为单位sleep：

  ```
    echo "Sleep for 5 seconds"
    sleep 5
    echo "Completed"
    
  ```
  
  &emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Sleep for 5 seconds
    Completed
    dicardo@MacBook-Pro desktop % time bash Try.sh
    Sleep for 5 seconds
    Completed
    bash Try.sh  0.00s user 0.00s system 0% cpu 5.011 total
    
  ```
  
  - Case 2: 以分钟为单位sleep：
  
  ```
    echo "Sleep for 0.05 minites"
    sleep 0.05m
    echo "Task Completed"
    
  ```
  
  - Case 3: 以小时为单位sleep：
  
  ```
    echo "Sleep for 0.003 hours"
    sleep 0.003h
    echo "Task Completed"
  ```
  
  - Case 4: 和其他指令结合sleep：
  
  ```
    dicardo@MacBook-Pro desktop % ls && sleep 2 && pwd
    Try.sh		weekday.txt
    /Users/dicardo/desktop
  ```
  
  - Case 5: 用指令提示实现sleep：
  
  ```
    dicardo@MacBook-Pro desktop % time (echo "Start"; sleep 5; echo "End") 
    Start
    End
    ( echo "Start"; sleep 5; echo "End"; )  0.00s user 0.00s system 0% cpu 5.005 total
    
  ```

  
  
  
  
  
  
  
  
  
