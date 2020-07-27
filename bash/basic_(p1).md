# Bash基础知识(1)

------

[整理自：Bash Examples](https://linuxhint.com/30_bash_script_examples/)

## Bash程序的创建和执行

### 1.创建

&emsp; 创建方式有两种：

- 直接通过文本编辑器进行编辑，然后将文件保存为`xxx.sh`的格式

- 通过命令行指令`nano xxx.sh`来在终端内进行编辑，进而保存到当前打开的位置

### 2.执行

&emsp; 执行方式也有两种：

- 使用`bash`指令：

  ```
    bash xxx.sh
  ```

- 使用`chmod a+x`指令修改文件权限：
  
  ```
    chmod a+x xxx.sh
    ./xxx..sh
  ```
&emsp; 补充：**chmod指令的使用**

&emsp; 模式选择：

  - `chmod a+x filename`等价于`chmod +x 文件名`：给所有人该文件的可执行权限
  
  - `chmod u+x filename`：给所有用户该文件的可执行权限
  
  - `chmod g+x filename`：给用户组该文件的可执行权限
  
  - `chmod o+x filename`：给其他人该文件的可执行权限
  
  - `chmod xxx filename/listname`：将该文件/目录的权限分别设置文件所有者（最高位）、群组用户（中间位）、其他用户（最低位）的权限值，权限值分为以下三种：
  
     权限 | 权限值 | 具体作用 |
    | ---- | ---- |   ----   |
    |   r  |  4   |  读取。当前用户可以读取文件内容，浏览目录 |
    |   w  |  2   |  写入。当前用户可以新增或修改文件内容，删除、移动目录或目录内文件 |
    |   x  |  1   |  执行。当前用户可以执行文件，进入目录   

&emsp; 若想同时设置为多模式，则将相应的权限值累加。例如，`chmod 777 filename`：将该文件权限修改为777（**可读可写可执行**）。

  
--------------

## Echo指令的使用
&emsp; [Echo指令详解](http://www.zsythink.net/archives/96/)

--------------

## 注释与多行注释
  - 单行注释：
  ```
    # This is a comment
  ```
  
  - 多行注释：
  ```
    : '
    This is a comment.
    This is a comment.
    '
  ```
 
 ------------
 
 ## 循环

### 1. While循环
&emsp; 基本格式为：
  ```
    while[ condition ]
    do
      commands
    done
  ```
&emsp; 特别需要注意的是，在bash中对变量进行赋值时，不能在等号左右加空格，否则会报语法错误，即必须为`var=1`而不能是`var = 1`。

  - Case 1:
  ```
    count=1
    while [ $count -lt 5 ]   # When count < 5
    do
      echo $count             # Use $ to access the value of count
      (( count++ ))           # The format for updating the counter
    done
  ```
  &emsp; Output:
  ```
    1
    2
    3
    4
  ```
  
  - Case 2:
  ```
    count=1
    while [ $count -le 10 ]
    do
      if [ $count == 6 ]      # Can also use: $count -eq 6
      then
        echo "Terminated..."
        break
      fi
      echo "Position: $count"     # Can use $ to print value of a variable in echo "xxxx"
      (( count++ ))
    done
  ```
  &emsp; Output:
  ```
    Position: 1
    Position: 2
    Position: 3
    Position: 4
    Position: 5
    Terminated...
  ```
  
  - Case 3:
  ```
    n=1
    while :             # Inifite loop
    do
      printf "The current value of n is: $n\n"      # The usage of printf in bash
      if [ $n == 3 ]
      then
        echo "Good!"
      elif [ $n == 5 ]
      then
        echo "Shit!"
      elif [ $n == 7 ]
      then
        exit 0              # The usage of exit 0 in bash
      fi
      (( n++ ))
    done
  ```
  &emsp; Output:
  ```
  The current value of n is: 1
  The current value of n is: 2
  The current value of n is: 3
  Good!
  The current value of n is: 4
  The current value of n is: 5
  Shit!
  The current value of n is: 6
  The current value of n is: 7
  ```
  
### 2. For循环
&emsp; 基本格式为：
  ```
    for variableName in lists
    do
      commands
    done
  ```
  - Case 1:
  ```
    for color in Blue Green Pink White Red
    do
      echo "Color = $color"
    done
  ```
  &emsp; Output:
  ```
    Color = Blue
  Color = Green
  Color = Pink
  Color = White
  Color = Red
  ```
  
  - Case 2:
  ```
    ColorList=("Blue Green Pink White Red")           # Create the array and initialize it
    for color in $ColorList                             # Access the array
    do
      if [ $color == 'Pink' ]
      then
        echo "My favorite color is $color"
      fi
    done
  ```
  &emsp; Output:
  ```
    My favorite color is Pink
  ```
  
  - Case 3: Read Command-line Arguments
  ```
    for myval in $*                         # read command-line arguments
    do
      echo "Argument: $myval"
    done
  ```
  &emsp; Output: (Assume that the command is: `bash Try.sh I love U`)
  ```
    Argument: I
    Argument: love
    Argument: U
  ```
  
  - Case 4: Three expressions in for loop
  ```
    for (( n=1; n<=5; n++ ))
    do
      if (( $n % 2 == 0 ))
      then
        echo "$n is even"
      else
        echo "$n is odd"
      fi
    done
  ```
  &emsp; Output:
  ```
    1 is odd
    2 is even
    3 is odd
    4 is even
    5 is odd
  ```

  - Case 1: File Reading
  ```
    i=1
    for day in `cat weekday.txt`            # File Operations
    do
      echo "Weekday: $i: $day"
      (( i++ ))
    done
  ```
  &emsp; Output:
  ```
    Weekday 1: Monday
    Weekday 2: Tuesday
    Weekday 3: Wednesday
    Weekday 4: Thursday
    Weekday 5: Friday
    Weekday 6: Saturday
    Weekday 7: Sunday
  ```
  
  
  
  
