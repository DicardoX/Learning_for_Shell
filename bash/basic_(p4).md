# Bash基础知识(4)

------

[整理自：Bash Examples](https://linuxhint.com/30_bash_script_examples/)

## 文件操作

### 1. 文件读取：

  - Case 2: 从命令行读取文件内容：
  
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
  
  
