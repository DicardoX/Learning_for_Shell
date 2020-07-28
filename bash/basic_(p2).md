# Bash基础知识(2)

------

[整理自：Bash Examples](https://linuxhint.com/30_bash_script_examples/)

## 获取用户输入

### 1.简单的用户读入指令 —— read指令

  ```
    echo -n "What is your favorite food: "
    read answer
    echo "Oh! you like $answer!"
  ```
&emsp; Output (if the input command is: What is your favorite food: `pizza`):

  ```
    Oh! you like pizza!
  ```
  
### 2. 带选择的用户读入指令 —— read -p & read -sp

  ```
    read -p 'Username: ' user           # -p is used to display some useful message
    read -sp 'Password: ' pass          # -sp will also hide the input
    
    if (( $user == "admin" && $pass == "12345" ))
    then 
      echo -e "\nSuccessful login"
    else
      echo -e "\nUnsuccessful login"
    fi
  ```
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Username: admin
    Password: 
    Successful login
    dicardo@MacBook-Pro desktop % bash Try.sh
    Username: admin
    Password: 
    Unsuccessful login
  ```

### 3. 多项用户输入

  ```
    echo "Type four names of your favorite programming languages"
    read lan1 lan2 lan3 lan4                # Multiple input
    echo "$lan1 is your first choice"
    echo "$lan2 is your second choice"
    echo "$lan3 is your third choice"
    echo "$lan4 is your fourth choice"
  ```

&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Type four names of your favorite programming languages
    C++ python java JS
    C++ is your first choice
    python is your second choice
    java is your third choice
    JS is your fourth choice
  ```
### 4. 带时间限制的用户输入指令 —— read -t [time]
  ```
    read -t 5 -p "Type your favorite color in 5 secs: " color           # If exceeded 5 secs, the program will exit
  ```
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Type your favorite color in 5 secs: red
    dicardo@MacBook-Pro desktop % bash Try.sh
    Type your favorite color in 5 secs: %    
  ```
-----------

## Case语句的使用

  ```
    echo "Enter your lucky number"
    read n
    case $n in                            # Start with this
    101)                                  # Case 1: n = 101
    echo "You got 1st prize";;
    510)                                  # Case 2: n = 510
    echo "You got 2nd prize";;
    999)                                  # Case 3: n = 999
    echo "You got 3rd prize";;
    *)                                    # Case 4: n = other value
    echo "Sorry, try next time...";;
    esac                                  # End with this
  ```
  
&emsp; Output:

  ```
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter your lucky number
    777
    Sorry, try next time...
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter your lucky number
    101
    You got 1st prize
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter your lucky number
    510
    You got 2nd prize
    dicardo@MacBook-Pro desktop % bash Try.sh
    Enter your lucky number
    999
    You got 3rd prize
  ```



