# Linux 高级用法 ：
## 管道   
        管道是一个特殊的文件，它将前一个命令的输出作为后一个命令的输入，多个命令可以通过管道连接起来，形成一个管道线。
        例如：ls -l | grep test ，将ls -l的输出作为grep test的输入，即查找包含test的行。
  
## 常用文档命令
  
1.  ps 命令 
      - 解读：ps 命令用于显示当前进程的状态。
      - 常见参数：
        - ps -ef : 显示所有进程, 包括其他用户的进程, 各列分别代表: 用户名, 进程ID, 父进程ID, CPU占用率, 内存占用率, 运行时间, 命令
        - ps -aux : 显示所有进程, 包括其他用户的进程, 但不包括进程的详细信息, 各列分别代表: 用户名, 进程ID, CPU占用率, 内存占用率, 运行时间, 命令
    
2. grep 命令
      - 解读：grep 命令用于查找文件里符合条件的字符串。
      - 常见用法：
        - grep test : 查找包含test的行
        - grep -E 'test1|test2' : 查找包含test1或test2的行
      - 常见参数：
        - grep -i : 忽略大小写
        - grep -v : 反向查找(即查找不包含指定字符串的行)
        - grep -E : 支持正则表达式
        - grep -e : 指定多个匹配条件, 例如grep -e test1 -e test2
        - grep --color : 匹配到的字符串高亮显示
    
3. awk 命令
      - 解读：awk 命令是一种处理文本文件的语言，是一个强大的文本分析工具。
      - 常见用法：
        - awk '{print $1}' : 打印第一列
        - awk '$1 > 10 {print $1}' : 打印第一列大于10的行
        - awk -F : '{print $1}' : 以:为分隔符，打印第一列
        - awk -v var=10 '{print $1}' : 定义变量var=10，打印第一列大于10的行
        - awk 'function abs(x){return ((x < 0.0) ? -x : x)} {print abs($1)}' : 计算第一列的绝对值
      - 常见参数：
        - awk -F : 指定分隔符，比如awk -F: '{print $1}'，表示以:为分隔符，打印第一列
        - awk -v : 定义变量，比如awk -v var=10 '{print $1}'，表示定义变量var=10，打印第一列大于10的行
  
4. kill 命令
      - 解读：kill 命令用于终止进程。
      - 常见参数：
        - (数字)
        - kill -1 : 重新读取配置文件
        - kill -9 : 强制终止进程
        - (字母)
        - kill -l : 列出所有信号名称
        - kill -s : 向进程发送信号，比如kill -s SIGKILL 1234，表示向进程1234发送SIGKILL信号
  
5. xargs 命令
      - 解读：xargs 命令用于将标准输入转换成命令行参数，常用于将管道的输出作为命令的参数。
      - 常见用法：
        - ps -ef | grep test | xargs kill -9 : 查找包含test的进程，然后终止进程
        - find . -name "*.txt" | xargs rm -rf : 查找所有txt文件，然后删除
      - 常见参数：
        - xargs -n : 指定每次传递给命令的参数个数，比如xargs -n 1，表示每次传递一个参数
        - xargs -I : 指定替换字符串，比如xargs -I {}，表示用{}替换命令中的参数
  
6. sed 命令
      - 解读：sed 命令是一种流编辑器，用来对文本进行过滤和替换。
      - 常见用法：
        - sed 's/test1/test2/g' : 将test1替换成test2
        - sed '1,3d' : 删除第1行到第3行
        - sed '1,3p' : 打印第1行到第3行
      - 常见参数：
        - sed -i : 直接修改文件内容
        - sed -e : 多点编辑，比如sed -e 's/test1/test2/g' -e 's/test3/test4/g'
        - sed -r : 支持正则表达式
  
7. find 命令
      - 解读：find 命令用于查找文件。
      - 常见用法：
        - find . -name "*.txt" : 查找当前目录下所有txt文件
        - find . -name "*.txt" -exec rm -rf {} \; : 查找当前目录下所有txt文件，然后删除
      - 常见参数：
        - find -name : 按照文件名查找
        - find -type : 按照文件类型查找，比如find . -type f，表示查找文件。类型有：f(文件), d(目录), l(链接)等。
        - find -size : 按照文件大小查找，比如find . -size +10M，表示查找大于10M的文件
        - find -perm : 按照文件权限查找，比如find . -perm 777，表示查找权限为777的文件
  
8. nohup 命令
      - 解读：nohup 命令用于在后台运行命令，即使终端关闭，命令也不会停止。
      - 常见用法：
        - nohup python test.py > test.log 2>&1 & : 后台运行test.py文件，输出日志到test.log
      - 常见参数：
        - nohup -u : 不缓冲输出，即不将输出缓冲到缓冲区，直接输出到文件
        - nohup -p : 指定进程号，比如nohup -p 1234，表示将进程号为1234的进程放到后台运行
        - 
  
## 常见用法解读
    1.  查找进程名为FILENAME的进程

    ps -aux | grep FILENAME  

    2. kill 所有python相关进程（除了管道本身查询命令外）
   
    ps -ef | grep python | grep -v grep | awk '{print $2}' | xargs kill -9

    kill -s 9 ps aux | grep python | awk '$11=="java" {print $2}'   

    区别：前者是先查找所有python进程，然后过滤掉grep命令，最后取出进程ID，然后kill；后者是先查找所有python进程，然后过滤掉grep命令，最后kill。

    两者特点: 前者更加通用，后者更加简洁。    

    3. 后台运行FILENAME.py文件，输出日志到LOGNAME.log，-u表示不缓冲输出，2>&1表示将标准错误输出重定向到标准输出，&表示后台运行。
   
    nohup python -u FILENAME.py > LOGNAME.log 2>&1 & 

    nohup java -jar universal_spider_java-0414.jar > /root/universal_spider/nohup.out 2>&1 &

    解释：nohup命令用于在后台运行命令，即使终端关闭，命令也不会停止。-u表示不缓冲输出，2>&1表示将标准错误输出重定向到标准输出，&表示后台运行。
