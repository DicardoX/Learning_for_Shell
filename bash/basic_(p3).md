# Bash基础知识(3)

------

[整理自：Bash Examples](https://linuxhint.com/30_bash_script_examples/)

## 函数创建和使用

### 1. 简单的函数定义：

  ```
    function F1()                     # 'function' can also be omitted
    {
      echo "I like bash programming"
    }
    
    F1                                # Call the function
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh 
    I like bash programming
  ```

### 2. 创建带参数的函数：

  ```
    Rectangle_Area(){
      area=$(($1 * $2))
      echo "Area is : $area"
    }
    
    Rectangle_Area 10 20                   # Call the function with parameters
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Area is : 200
  ```
  
### 3. 创建带返回值的函数：

  - Case 1: 使用全局变量：
  
  ```
    function F1()
    {
      retval='I like programming'
    }
    retval='I hate programming'
    echo $retval                          # Print 'hate'
    F1
    echo $retval                          # Print 'like'
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    I hate programming
    I like programming
  ```
  
  - Case 2: 使用函数指令：

&emsp; 可以接收一个bash函数的返回值并在调用该函数时存储在一个变量中。

  ```
    function F2()
    {
      local retval='Using BASH Function'
      echo "$retval"                    # 'echo' command in a function will not print anything but return the variable!
    }
    
    getval=$(F2)                        # Call & Store
    echo $getval
  ```

&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Using BASH Function
  ```
  
  - Case 3: 使用变量：
  
  ```
    function F3()
    {
      local arg1=$1                                       # If don't add 'local', treat arg1 as global variable in default
      if [[ $arg1 != "" ]];
      then
        retval="BASH function with variable"              # If the argument is not empty
      else
        echo "No Argument"                                # If the argument is empty
      fi
    }
    
    getval1="Bash Function"
    F3 $getval1                                           # Argument exists
    echo $retval
    ##### Error condition #####
    getval2=$(F3 10)                                      
    echo $getval2
    ##### Erroe condition ends here #####
    getval3=$(F3)                                         # Argument not exists
    echo $getval3
  ```

&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    BASH function with variable
                                                          # Error condition
    No Argument
  ```
  
  - Case 4: 使用返回语句：
  
  ```
    function F4()
    {
      echo "Bash Return Statement"                        # Will print the string
      return 35                                           # Usage of return statement
    }
    
    F4
    echo "Return value of the function is $?"             # Use $? to store the return value of the function called 
  ```
  
&emsp; 注意，`$?`的使用必须紧接着函数调用的下一行，否则值为0。

&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Bash Return Statement
    Return value of the function is 35
  ```
  
----------------

## 创建目录

  
  
