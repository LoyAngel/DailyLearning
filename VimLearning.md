# VIM 

## 快速移动
### 普通跳转
        hjkl 上下左右
        g + hjkl （就算被文本分割也能）上下左右
        
### word跳转
        w e b ge 下个word首，下个word尾，上个word首，上个word尾
        W E B gE 下个WORD首，下个WORD尾，上个WORD首，上个WORD尾
        
### 本行跳转
        0 $ ^ g_ 切换到行首/行尾/非空行首/非空行尾
        % 跳转到本行光标后的括号/匹配的括号
        
### 本行查找
        f F{character} 快速跳到下个word/上个word 字符
        t T{character} 快速跳到下个word/上个word 前面一个字符
        , ; 在跳转查询后，切换上个/下个查询
        
### 垂直跳转
        { } 切换到上个/下个 段落
        ctrl+ d/u 向下/上 翻页
        % 跳转到{([ 等括号
        
### 垂直查找
        / ? 向后/前 搜索
        n N 在搜索项目中 向后/前 跳转
        
### 数字的奥义
        数字前缀 + 命令  有不同神奇作用 
        
### 全局跳转
        zz 当前行置于中央
        zt 当前行置于首行
        zb 当前行置于尾行
        gg 跳转文首
        G 跳转文尾
        {line}gg 指定跳转{line}行
        
        

## 编辑操作
### 动词
#### 操作准则
        {operators}{count}{motion}   
        {操作}{计数}{范围}
        例如：
            d2w 删除2 word
            d2j 向下删除2行
            df` 删除本行所有的`
            d/helloworld 删除本文件所有的helloworld
            ggdG 删除全文
            c/hello 直到遇到第一个hello之前，删除所有文本
            <ii 将本层级的所有行都缩进
#### 常用命令
        c change 覆盖 
        d delete 删除
        y yank 复制
        p paste 粘贴
        < > 向左/右缩进
        = format 格式化
        g~ toggle 翻转大小写
        gu gU 切换到小/大写
### 介词(范围)
#### 常用命令
        i inner 内部
        a around 包裹
        ii/ai 选择本层级内/包括本层级在内的所有内容(常用于Python)
        
        . 当前
        {num} 第几行
        $ 最后一行
        % 全部行
        , 范围区间
        .,+5/-5 当前到后/前5行
        :/^example/+1,$ 当前行以下，从字符 "example" 开头的那一行的下一行至结尾
        :/a//b//c/ 设置多个查找条件
### 名词
#### 常用命令
        w word 单词
        s sentence 句子
        p paragraph 段落
        b ( block 小括号
        B { Block 大括号
        i innter 本层级
        t html标签
        " ' 引用
### 其他操作
#### . 的妙用
        1. . 可以重复上一次命令
        2. 在搜索后一系列操作，在n后按.重复系列操作
        3. 在i进入模式，进行文本输入，ctrl+c退出，按.会重复输入
#### 删除操作
        x del 向后删除
        X backspace 向前删除
#### 撤销与恢复
        u 撤销
        ctrl + r 恢复



## 插入操作
#### 进入模式
        i insert 插入（光标前）
        a append 添加（光标后）
        o O open a line below/above 向下/上插入一行
        gi insert the place you last changed 插入在上次编辑位置
#### 插入模式快捷键
        ctrl+h 删除上一个输入的字符
        ctrl+w 删除上一个输入的word
        ctrl+u 删除上一个输入行
        
        ctrl+o 离开其他模式并且返回原先normal mode时所在位置 
        ctrl+i 进入insert mode并且返回原先insert mode时所在位置 

## 选择操作
#### 进入模式
        v 选择字符
        V 选择行
        ctrl+v 选择方块
        ctrl+a 取消选择模式进入普通模式（可以快速进入多光标）
#### 操作准则
        {trigger visual mode}{motion}{operator}

## 查找操作
#### 常规操作
        f 本行查找
        / 向后查找
        ? 向前查找
        * # 向后/前查找当前文本
#### 进阶操作
        gn 可以视为{motion} 
        比如:原先删除需要n+.的配合，但现在dgn就是删除下一个匹配，再用.即可完成一键删除。

## 复制操作
#### 常规操作
        y 复制
        yy Y 复制一行
        p P 向后/前粘贴
#### 进阶操作
        ddp 交换上下行
        xp 交换字符
#### 寄存器
#### 寄存器种类
        未命名寄存器
            " 默认寄存器
        命名寄存器
            0 最后寄存器
#### 保存之前复制与剪贴内容
#### 可使用寄存器
        未命名寄存器
            " 默认寄存器
        命名寄存器
            0 最后寄存器
            1-9 保存之前复制与剪贴内容
            a-z 可使用寄存器
            + * 剪贴板寄存器
            _ 黑洞寄存器，放里面不会复制
            / 查找寄存器，寄存查找内容

        非只读寄存器可以更改：
            :let @{name of reg} = '{text}'
#### 寄存器使用
        "{name of register} y d c {motion}   
#### 寄存器的查看
        :reg
        :reg {name of register} 
#### 插入模式的使用
        ctrl+R {name of register} 粘贴

## 命令模式
### 文件操作
        e edit {path}  打开文档
        w write 不解释 
        q quit 不解释
        ! force 强制 ，如w! 强制写，q! 不保存退出（强制退出）
        all 全部，跟在q,w 后面，表示全部文件都执行
### 编辑操作
        常见格式：
            :[range]command [options]
        例子：
            :10,12d a 将10-12行剪切到a寄存器
        
        range：
            同上
            '<,'> Visual mode后进入Ex mode中会自动补齐范围
            
        替换操作：
            :[range]s/{pattern}/{substitute}/{flags}
            
            flags:
                g 所有选中行
                i 忽略大小写
                c 确认每个替换
### 重复操作
          @: 重复上一次操作
          @@ 重复之前重复的操作

## 书签操作

### 标记操作
        命令格式：
                :[range]mark {a-zA-Z0-9}
        标记解释：
                a-z 只作用于当前文件
                A-Z 作用于所有文件
                0-9 作用于所有文件，但是只在退出vim后才会保存。mark会保存到viminfo文件中。该标记比较特殊，例如：0 会跳转到上次退出vim时的位置；1 会跳转到上上次退出vim时的位置等等。
        常用命令：
                ma 标记当前行
                'a 跳转到标记行
                `a 跳转到标记列
                d'a 删除当前行到标记行
                d`a 删除当前行到标记列
                y'a 复制当前行到标记行
                y`a 复制当前行到标记列
                :marks 查看所有标记
        
## 界面和页面操作
### 界面操作
        Ctrl+w s或者 :sp {path}    水平分屏
        Ctrl+w v或者 :vsp {path}   垂直分屏
        (分屏后用Ctrl+p 打开文件)
        Ctrl+w hjkl 移动窗口焦点
### 标签操作
        :tabenew {file} 创建新标签
        :tabn 下一个标签
        :tabp 上一个标签
        :tabo 只保留当前标签
        
### 标签切换
        gt 切换到下一个标签
        gT 切换到上一个标签
        {page}gt 切换到第{page}标签

## 多光标操作
### 单词搜索
        gb 添加相同词到多光标
        
### 行操作
        shift + v 进入 v-block 模式
        hjkl 调整
        ctrl + a 取消block
        或者
        I 或 A 进入 insert 模式

## Vscode 特有操作
### 函数查看
        gd gi 跳转函数定义/实现
        gh 显示（鼠标悬停时出现的）解释文字
        ctrl + d 返回函数
        gh 查看参数
        za 展开/缩略函数
        zM 全部隐藏
        zR 全部展开
        
        
        ZZ 退出保存文件
        ZQ 强制退出

## Vim插件
### vim-urround
        {operation}s{count}{motion}
        
        ds{char} 删除外面的引号、括号、花括号等
        cs{old_char}{new_char} 替换...
        ysapt{text} 段落外面加上<text>
        ysw{(/)} 整个单词加上带空格/不带空格括号
        yswb B 整个单词加上带不带空格圆括号/花括号
        
        
        进入visual code, S{desired character} 在外面加上...
### vim-neak(需开启)
#### 向下/上快速搜索
        s/S{char}{char}
        
#### 操作行为
        {operation}z{char}{char}  
### vim-easymotion(需开启)
         <Leader> + <Leader> + {motion}  快速跳转行为

         <Leader> + <Leader> + w/b 快速跳转到单词开头/结尾
         <Leader> + <Leader> + f/F{char} 快速向下/上跳转搜索
         <Leader> + <Leader> + s{char} 快速跳转到{char}
         
#### 一些命令
         不跟参： j k h l b w e ge 
         跟参: f F t T s(全文搜索) 
         
         
        
#### Neo-vim
### 复制与剪贴
        :[range]co(py)/t {address}   复制
        :[range]m(ove) {address}   剪贴
        
        比如：
        :,+3co $ 复制当前3行到行尾
        :,+3m $ 剪切当前3行到行尾
        
### 普通模式
        :[range]norm(al) {commands}  普通模式下执行命令
        :exe(cute) ":{...}"  执行命令
        
        比如：
        :%norm A; 在全文末尾加上:
        :%exe
### Gand V
        :[range]g[lobal]/{pattern}/[cmd]
        :[range]v[global]/{pattern}/[cmd]
        
        :g 默认整个文件生效
        :g! 不满足匹配
        :v 反向匹配
        :v! 反向不满足匹配
        
        常见的range: 
        % 全文
        . 当前行
        1,10 1-10行
        1,$ 1-最后一行
        1,. 1-当前行
        .,.+5 当前行-当前行+5行

        常见的pattern:
        norm [commands] 执行命令
        +1d 每隔一行删除
        s/old/new 替换
        t. 复制到本行


        比如:
        :g!/;$/norm A; 在所有没有分号的文章后面加分号
        :g/^#/norm x 在对所有markdown标题降级
        :v/watch/d 删除所有不包含watch的行


## 技巧
        v选择后，跳至区域开头或结尾
        vo vO

        命令行历史(设置后)
        ctrl+j/k 命令上下选择

        防止水平滑动的时候失去选择

        更加智能的当前行高亮
