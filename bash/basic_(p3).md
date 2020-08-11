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
    echo $retval
    F1
    echo $retval
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh              
    I hate programming
    I like programming
  ```

  - Case 2: 使用函数指令：
  
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

### 1. 简单的目录创建：

  ```
    echo "Enter directory name"
    read newdir
    `mkdir $newdir`                                         # Create the new directory
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter directory name
    xxx
    dicardo@MacBook-Pro desktop % ls
    Try.sh		weekday.txt	xxx
  ```
  
### 2. 基于检查目录是否存在的目录创建：

  ```
    echo "Enter directory name"
    read newdir
    if [ -d "$newdir" ]
    then
      echo "Directory exist"
    else
      `mkdir $newdir`
      echo "Directory created"
    fi
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter directory name
    xxx
    Directory created
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter directory name
    xxx
    Directory exist
  ```

### 3. 多目录创建：

  ```
    dicardo@MacBook-Pro desktop % mkdir tmp1 tmp2 tmp3
    dicardo@MacBook-Pro desktop % ls
    Try.sh		tmp1		tmp2		tmp3		weekday.txt
  ```
  
### 4. 使用`mkdir -p path`指令在不存在的路径中创建目录：

&emsp; Error condition：
  ```
    dicardo@MacBook-Pro desktop % mkdir picture/newdir/test
    mkdir: picture/newdir: No such file or directory
  ```
  
&emsp; 使用`mkdir -p path`指令:
  ```
    dicardo@MacBook-Pro desktop % mkdir -p picture/newdir/test
    dicardo@MacBook-Pro desktop % cd picture
    dicardo@MacBook-Pro picture % ls -R
    newdir

    ./newdir:
    test

    ./newdir/test:
  ```

### 5. 创建带权限的目录：

&emsp; 使用`stat`指令查看目录权限：
  ```
    dicardo@ubuntu:~/桌面$ mkdir newdir
    dicardo@ubuntu:~/桌面$ stat newdir/
    文件：newdir/
    大小：4096      	块：8          IO 块：4096   目录
    设备：805h/2053d	Inode：396209      硬链接：2
    权限：(0775/drwxrwxr-x)  Uid：( 1000/ dicardo)   Gid：( 1000/ dicardo)
    最近访问：2020-08-11 16:43:43.371211359 +0800
    最近更改：2020-08-11 16:43:43.371211359 +0800
    最近改动：2020-08-11 16:43:43.371211359 +0800
    创建时间：-

  ```
  
&emsp; 使用`mkdir -m`来设置目录权限：
  ```
    dicardo@ubuntu:~/桌面$ mkdir -m 777 newdir
    dicardo@ubuntu:~/桌面$ stat newdir
    文件：newdir
    大小：4096      	块：8          IO 块：4096   目录
    设备：805h/2053d	Inode：393274      硬链接：2
    权限：(0777/drwxrwxrwx)  Uid：( 1000/ dicardo)   Gid：( 1000/ dicardo)
    最近访问：2020-08-11 16:46:09.174257613 +0800
    最近更改：2020-08-11 16:46:09.170255037 +0800
    最近改动：2020-08-11 16:46:09.170255037 +0800
    创建时间：-
  ```







