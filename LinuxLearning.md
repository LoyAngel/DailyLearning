# Linux 
## 基本用法
### 管道   
        管道是一个特殊的文件，它将前一个命令的输出作为后一个命令的输入，多个命令可以通过管道连接起来，形成一个管道线。
        例如：ls -l | grep test ，将ls -l的输出作为grep test的输入，即查找包含test的行。

### 多命令执行
        多命令执行是指多个命令通过特殊字符连接起来，按顺序执行。
        1. 分号; —— 顺序执行，即使前一个命令执行失败，也会执行后面的命令。 
        例如：cd /root; ls -l，先切换到/root目录，然后执行ls -l命令。
        2. 与符号&& —— 逻辑与，只有前一个命令执行成功，才会执行后面的命令。
        例如：cd /root && ls -l ，先切换到/root目录，然后执行ls -l命令，如果cd /root命令执行失败，则不会执行ls -l命令。

### 命令替换
        命令替换是指将命令的输出作为另一个命令的参数。
        1. 反引号` ` —— 将反引号里面的命令的输出作为另一个命令的参数。
        2. $() —— 将$()里面的命令的输出作为另一个命令的参数。
        例如，ls -l $(which python) 或者 ls -l `which python`，先查找python命令的路径，然后执行ls -l命令。

### 任务调度
        任务调度是指在指定的时间执行命令。
        1. & 符号 —— 在后台执行命令。
        注意：& 仅仅是将命令放到后台执行，但是如果终端关闭，命令也会停止。如果想要在后台执行命令，即使终端关闭命令也不会停止，需要使用nohup命令，或者Ctrl+Z挂起后，使用bg命令，切换到后台执行。
        2. Ctrl+Z —— 挂起命令。
        注意：Ctrl+Z 仅仅是将命令挂起，但是如果终端关闭，命令也会停止。
        Ctrl+Z 可以在vim中使用，比如在vim中输入Ctrl+Z，然后输入jobs，可以看到vim已经被挂起，然后输入bg，可以将vim切换到后台执行。
        3. jobs —— 查看挂起的命令。
        注意：jobs 命令只能查看当前终端的挂起命令，如果想要查看所有终端的挂起命令，需要使用jobs -l命令。
        4. bg/fg —— 将挂起的命令切换到后台/前台执行。
        注意：bg/fg 命令只能切换当前终端的挂起命令，如果想要切换所有终端的挂起命令，需要使用bg/fg %jobnumber命令。

### 链接文件
        链接文件是指将一个文件链接到另一个文件，这样就可以通过两个文件名访问同一个文件。
        1. inode
        inode是文件的索引节点，每个文件都有唯一的inode号，通过inode号可以找到文件的存储位置。
        2. 硬链接与软链接
        硬链接是指将一个文件链接到另一个文件，并且两个文件的inode号相同，即指向同一个文件。当对硬链接文件进行修改时，被链接的文件也会被修改。当删除被链接的文件时，硬链接文件不会被删除。硬链接只能链接文件，不能链接目录。
        软链接是指将一个文件链接到另一个文件,并且inode号也可以不同，即指向不同的文件。与硬链接不同，软链接只是一个指向文件的快捷方式，因此当对软连接文件进行修改时，被链接的文件不会被修改。当删除被链接的文件时，软链接文件将失效。软连接可以链接文件，也可以链接目录。
        3. ln 命令
        ln 命令用于创建链接文件。创建的链接文件默认是硬链接文件。
        ln -s 命令用于创建软链接文件。
        常见用法：
        ln test.txt test2.txt ：创建test2.txt文件，指向test.txt文件
        ln -s test.txt test2.txt ：创建test2.txt文件，指向test.txt文件
        注意:
        ln -s不可以链接相对路径，不然会提示符号链接层数过多。

### 重定向至文件
        >, >> , <
        1. > 重定向
        > 重定向用于将命令的输出重定向到文件，如果文件不存在，则创建文件，如果文件存在，则覆盖文件。
        如：ls -l > test.txt，将ls -l的输出重定向到test.txt文件。
        2. >> 追加重定向
        >> 追加重定向用于将命令的输出重定向到文件，如果文件不存在，则创建文件，如果文件存在，则追加到文件末尾。
        如：ls -l >> test.txt，将ls -l的输出追加重定向到test.txt文件。
        3. < 输入重定向
        < 输入重定向用于将文件作为命令的输入。
        如：wc -l < test.txt，将test.txt文件作为wc -l命令的输入。

### 系统服务管理
        1. service 命令
        service 命令用于管理系统服务。
        常见用法：
        service test start ：启动test服务
        service test stop ：停止test服务
        service test restart ：重启test服务
        service test reload ：重新加载配置文件
        service test status ：查看test服务状态
        
        2. chkconfig 命令
        chkconfig 命令用于管理开机自启动服务。
        常见用法：
        chkconfig --list ：列出所有服务
        chkconfig --add test ：添加test服务
        chkconfig --del test ：删除test服务
        chkconfig test on ：设置test服务开机自启动
        chkconfig test off ：取消test服务开机自启动

        3. systemctl 命令
        systemctl 命令用于管理系统服务。systemctl是融合了service和chkconfig的新命令，既可以管理系统服务，也可以管理开机自启动服务。
        常见用法：
        systemctl start test ：启动test服务
        systemctl stop test ：停止test服务
        systemctl restart test ：重启test服务
        systemctl reload test ：重新加载配置文件
        systemctl status test ：查看test服务状态
        systemctl enable test ：设置test服务开机自启动
        systemctl disable test ：取消test服务开机自启动
        systemctl is-enabled test ：查看test服务是否开机自启动
        systemctl list-unit-files ：列出所有服务
        systemctl list-units ：列出所有运行的服务

     
## 常用文档命令
### 进程管理命令
 - ps 命令 
      - 解读：ps 命令用于显示当前进程的状态。
      - 常见参数：
        - ps -ef : 显示所有进程, 包括其他用户的进程, 各列分别代表: 用户名, 进程ID, 父进程ID, CPU占用率, 内存占用率, 运行时间, 命令
        - ps -aux : 显示所有进程, 包括其他用户的进程, 但不包括进程的详细信息, 各列分别代表: 用户名, 进程ID, CPU占用率, 内存占用率, 运行时间, 命令
  
 - kill 命令
      - 解读：kill 命令用于终止进程。
      - 常见参数：
        - (数字)
        - kill -1 : 重新读取配置文件
        - kill -9 : 强制终止进程
        - kill -15 : 终止进程(默认)
        - (字母)
        - kill -l : 列出所有信号名称
        - kill -s : 向进程发送信号，比如kill -s SIGKILL 1234，表示向进程1234发送SIGKILL信号

  - nohup 命令
      - 解读：nohup 命令用于在后台运行命令，即使终端关闭，命令也不会停止。
      - 常见用法：
        - nohup python test.py > test.log 2>&1 & : 后台运行test.py文件，输出日志到test.log
      - 常见参数：
        - nohup -u : 不缓冲输出，即不将输出缓冲到缓冲区，直接输出到文件
        - nohup -p : 指定进程号，比如nohup -p 1234，表示将进程号为1234的进程放到后台运行
  
  - top 命令
      - 解读：top 命令用于实时显示进程的动态。
      - 常见用法：
        - top : 显示所有进程的动态
        - top -u root，表示显示root用户的进程动态
        - top -p 1234，表示显示进程号为1234的进程动态
      - 常见参数： 
        - top -u : 显示指定用户的进程动态
        - top -p : 显示指定进程号的进程动态
        - top -d : 指定刷新时间，比如top -d 1，表示每隔1秒刷新一次
        - top -n : 指定刷新次数，比如top -n 10，表示刷新10次后退出
        - top -b : 以批处理模式运行，即不显示交互界面，直接将结果输出到文件
      - 其他：
        进入top命令后，可以使用以下快捷键： 
        - h : 显示帮助
        - q : 退出
        - k : 终止进程
        - u : 显示指定用户的进程动态
        - p : 显示指定进程号的进程动态
        - d : 指定刷新时间，比如d 1，表示每隔1秒刷新一次
        - n : 指定刷新次数，比如n 10，表示刷新10次后退出
        - b : 以批处理模式运行，即不显示交互界面，直接将结果输出到文件
        - c : 切换显示模式，比如显示完整命令，显示路径等
        - M : 按内存使用大小排序
        - P : 按CPU使用大小排序
        - T : 按运行时间排序
 ### 命令行编辑命令 
 - xargs 命令
      - 解读：xargs 命令用于将标准输入转换成命令行参数，常用于将管道的输出作为命令的参数。
      - 常见用法：
        - ps -ef | grep test | xargs kill -9 : 查找包含test的进程，然后终止进程
        - find . -name "*.txt" | xargs rm -rf : 查找所有txt文件，然后删除
      - 常见参数：
        - xargs -n : 指定每次传递给命令的参数个数，比如xargs -n 1，表示每次传递一个参数
        - xargs -I : 指定替换字符串，比如xargs -I {}，表示用{}替换命令中的参数

### 文本处理命令
 - sed 命令
      - 解读：sed 命令是一种流编辑器，用来对文本进行过滤和替换。
      - 常见用法：
        - sed 's/test1/test2/g' : 将test1替换成test2
        - sed '1,3d' : 删除第1行到第3行
        - sed '1,3p' : 打印第1行到第3行
      - 常见参数：
        - sed -i : 直接修改文件内容
        - sed -e : 多点编辑，比如sed -e 's/test1/test2/g' -e 's/test3/test4/g'
        - sed -r : 支持正则表达式
    
 - awk 命令
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
  
### 文件查找命令
 - find 命令
      - 解读：find 命令用于查找文件。
      - 常见用法：
        - find . -name "*.txt" : 查找当前目录下所有txt文件
        - find . -name "*.txt" -exec rm -rf {} \; : 查找当前目录下所有txt文件，然后删除
      - 常见参数：
        - find -name : 按照文件名查找
        - find -type : 按照文件类型查找，比如find . -type f，表示查找文件。类型有：f(文件), d(目录), l(链接)等。
        - find -size : 按照文件大小查找，比如find . -size +10M，表示查找大于10M的文件
        - find -perm : 按照文件权限查找，比如find . -perm 777，表示查找权限为777的文件   
        
 - grep 命令
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

 - locate 命令
      - 解读：locate 命令用于查找文件，比find命令快，但是不够准确，因为它不是实时查找，而是根据系统建立的索引进行查找。
      - 常见用法：
        - locate test : 查找包含test的文件
        - locate -i test : 忽略大小写，查找包含test的文件
        - locate -r test$ : 支持正则表达式，查找以test结尾的文件
      - 常见参数：
        - locate -i : 忽略大小写
        - locate -r : 支持正则表达式
        - locate -c : 只输出匹配到的文件数量
        - locate -l : 输出匹配到的文件数量，以及匹配到的文件列表
      - 其他：
        - updatedb : 更新索引，一般每天自动更新，不需要手动更新

### 压缩与归档
10. gzip 命令
      - 解读：gzip 命令用于压缩文件，压缩后的文件名为原文件名后面加上.gz后缀。
      - 常见用法：
        - gzip test.txt : 压缩test.txt文件，压缩后的文件名为test.txt.gz
      - 常见参数：
        - gzip -d : 解压缩文件，比如gzip -d test.txt.gz，表示解压缩test.txt.gz文件
        - gzip -c : 将压缩后的文件输出到标准输出，比如gzip -c test.txt > test.txt.gz，表示将test.txt压缩后输出到test.txt.gz文件
        - gzip -r : 递归压缩目录下的所有文件，比如gzip -r test，表示压缩test目录下的所有文件

11. tar 命令
        - 解读：tar 命令用于归档文件，归档后的文件名为原文件名后面加上.tar后缀。归档文件，即将多个文件或目录合并到一个文件中。
        - 常见用法：
          - tar -cvf test.tar test.txt test2.txt : 归档test.txt和test2.txt文件到test.tar文件
          - tar -zxvf test.tar.gz : 解压缩test.tar.gz文件
        - 常见参数：
          - tar -c : 归档文件
          - tar -x : 解压缩文件
          - tar -z : 支持gzip压缩
          - tar -v : 显示详细信息
          - tar -f : 指定归档文件名
          - tar -r : 向归档文件中追加文件
          - tar -t : 显示归档文件中的文件列表

### 作业调度
12. at 命令
        - 解读： at 命令用于在指定的时间执行命令。
        - 常见用法：
          - at now + 1 minute : 在1分钟后执行命令
          - at 10:00 : 在10点执行命令
          - at -f test.sh now + 1 minute : 在1分钟后执行test.sh脚本
        - 常见参数：
          - at -f : 指定脚本文件
          - at -l : 列出所有任务
          - at -d : 删除任务，如at -d 1，表示删除第1个任务
          - at -c : 显示任务内容
        - 其他：
          TIME时间格式有如下几种： HH:MM, HH:MM:SS, HH:MM MMDDYY, MM/DD/YY, MM.DD.YY, MM-DD-YY, HH:MM MM/DD/YY, HH:MM MM.DD.YY, HH:MM MM-DD-YY

13. crontab 命令
        - 解读： crontab 命令用于在指定的时间执行命令，与at命令不同的是，crontab命令是周期性执行。
        - 常见用法：
          - crontab -e，然后输入* * * * * echo "hello"，表示每分钟执行一次echo "hello"命令
        - 常见参数：
          - crontab -e : 编辑任务
          - crontab -l : 列出所有任务
          - crontab -r : 删除所有任务
        - 其他：
          crontab格式： * * * * * command，分别表示
                       分钟(0-59) 小时(0-23) 日期(1-31) 月份(1-12) 星期(0-6,0表示周日) command

### shell环境命令
14. export 命令
        - 解读： export 命令用于设置环境变量。
        - 常见用法：
          - export PATH=$PATH:/usr/local/python3/bin : 将/usr/local/python3/bin目录添加到PATH环境变量中
        - 常见参数：
          - export -n : 删除指定的环境变量，比如export -n PATH，表示删除PATH环境变量
          - export -p : 列出所有环境变量

15. source 命令
        - 解读： source 命令用于在当前shell环境下读取并执行指定文件中的命令。
        - 常见用法：
          - source test.sh : 在当前shell环境下读取并执行test.sh文件中的命令
        - 常见参数：
          - source -n : 不执行命令，仅仅读取文件中的命令
          - source -v : 显示所有读取的命令

16. env 命令
        - 解读： env 命令用于显示当前系统的环境变量。
        - 常见用法：
          - env : 显示所有环境变量
          - env PATH : 显示PATH环境变量
        - 常见参数：
          - env -i : 清除所有环境变量
          - env -u : 清除指定的环境变量，比如env -u PATH，表示清除PATH环境变量

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

    nohup java -jar universal_spider_java-0414.jar > nohup.out 2>&1 &

    nohup python -u app.py --debug > app.log 2>&1 &

    解释：nohup命令用于在后台运行命令，即使终端关闭，命令也不会停止。-u表示不缓冲输出，2>&1表示将标准错误输出重定向到标准输出，&表示后台运行。

## service文件
        service文件是systemd管理的服务的配置文件，一般位于/etc/systemd/system目录下，以.service结尾，比如sshd.service。service文件是一个文本文件，可以使用vim编辑。
### 常见格式
```bash
# 系统自带的服务，可以放在After,Before,Wants,Requires，常见的有network.target( 网络服务 ),syslog.target( 系统日志服务 ),local-fs.target( 本地文件系统服务 ),remote-fs.target( 远程文件系统服务 ),time-sync.target( 时间同步服务 ),timers.target( 定时任务服务 ),sockets.target( 套接字服务 ),swap.target( 交换分区服务 ),basic.target( 基本服务 ),multi-user.target( 多用户服务 ),graphical.target( 图形界面服务 ),rescue.target( 救援服务 ),emergency.target( 紧急服务 )
[Unit]
Description=描述
After=依赖的服务,表示某些服务启动后再启动该服务
Before=依赖的服务,表示某些服务启动前启动该服务
Wants=依赖的服务,弱依赖，表示依赖的服务启动后再启动该服务, 但是依赖的服务启动失败、停止后，该服务仍然会启动
Requires=依赖的服务,强依赖，表示依赖的服务启动后再启动该服务, 但是依赖的服务启动失败、停止后，该服务不会启动

[Service]
Type=服务类型，常见的有simple( 默认值，表示该服务是一个简单的命令 ),forking( 表示该服务是一个守护进程, 类似nohup启动),oneshot( 表示该服务只运行一次 ),dbus( 表示该服务是一个dbus服务 )
ExecStart=启动命令
Restart=重启策略，常见的有no( 默认值，表示不重启 ),on-success( 表示只有在成功退出时才重启 ),on-failure( 表示只有在失败退出时才重启 ),on-abnormal( 表示只有在异常退出时才重启 ),on-abort( 表示只有在异常退出时才重启 ),on-watchdog( 表示只有在看门狗退出时才重启 )

[Install]
WantedBy=表示服务所在的target，一般用multi-user.target(多用户服务),因为这个target是默认启动的
```

## shell 脚本
### 经典解读
```bash
#!/bin/bash 表示使用bash解释器执行脚本

# 定义变量
case "$1" in
start) # 表示如果第一个参数是start，则执行下面的命令
    do something...
    echo "start"
    ;;
stop) # 表示如果第一个参数是stop，则执行下面的命令
    do something...
    echo "stop"
    ;;
...
*) # 表示如果第一个参数不是start或stop，则执行下面的命令
    echo "Usage: $0 {start|stop}"
    exit 1
    ;;
esac # 表示case语句结束

exit 0 # 表示脚本正常退出
```
