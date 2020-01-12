---
title: vim使用与命令
date: 2019-07-02 23:24:04
category: 工具
tags: 工具
author: lemon
---


# 实践出真知

- 在用vim打开.vue文件时在空格和中文的地方背景会显示为白色，输入`:colo default`可重置
- 在用vim时，当我想要将vim中的代码直接通过鼠标复制到其它地方的时候，会将行号也复制过去，解决方法是：`:set nonu`关闭行号，复制完再输入`:set nu`打开行号。目前还没有找到更好的方法（180911）（更好的方法就是通过vim的快捷键）
- [tabs切换](https://zhuanlan.zhihu.com/p/25946307)

## 常用操作：
    
- `:tabe <file>`    打开一个标签页
- `gt/gT`           切换标签页
- `:tabn/:tabp`     切换标签页
- `:tabonly`        仅留下当前标签页
- `:tabclose`       关闭当前标签页

### vim 分栏
- 直接以分栏方式打开多个文件
    ```
        $ vim -on file1 file2 ... filen       上下分栏打开n个文件
        $ vim -On file1 file2 ... filen       左右分栏打开n个文件
    ```
- 当前编辑文件分栏，打开的两栏内容相同
    ```
    :sp   xxx    在当前文件上方栏打开文件xxx，并且xxx变为可编辑状态
    :vsp  xxx   在当前文件左侧打开文件xxx>，并且xxx变为可编辑状态
    ```
- 在各栏切换的方法
    ```
    ctrl+w+ h/j/k/l     切换到前/下/上/后栏
    ctrl+w+ 方向键      功能同上
    ctrl+ww             切换到下一个窗格中，周而复始
    ```
- 关闭分栏  
    `ctrl+w+c       使用时需要松开ctrl再按c`
- 调整分栏大小
    ```
    ctrl+w+n>       左右扩大n列
    ctrl+w+n<       左右缩小n列
    ctrl+w+n+       上下扩大n行
    ctrl+w+n-       上下缩小n行
    ````

### 配置插件

想给自己本机的vim装一个NERDTree的插件。由于之前捣鼓vue-vim插件的时候装过vundle（用来管理插件的插件），所以选择使用nerdTree 来安装。由于之前已经clone过vundle的包，这次我只需要在.vimrc文件中配置如下：

```
set nocompatible              " be iMproved, required
filetype off                  " required

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'scrooloose/nerdtree' " 加入NERDTree

call vundle#end()            " required
filetype plugin indent on    " required

```
然后保存退出，重新进入vim，执行 `:PluginInstall`即可自动安装。对于NERDTree，可以映射它的快捷键.
```
Plugin 'scrooloose/nerdtree'
let NERDTreeWinPos='right'
let NERDTreeWinSize=30
map <C-f> :NERDTreeToggle<CR>
```
### 关于NERDTree的树形目录，常用快捷键：
```
ctrl + w + w    光标自动在左右侧窗口切换
m       显示文件系统菜单
i和s可以水平分割或纵向分割窗口打开文件，前面加g类似go的功能
t 在标签页中打开
T 在后台标签页中打开
p 到上层目录
P 到根目录
K 到同目录第一个节点
J 到同目录最后一个节点

enter目录会默认打开MinBufExplore，t或T才是在标签页打开

MinBuffExplore和相关的快捷键：

当光标停留在这个窗口时,MinBuffExplore高亮时。

<Tab>   向前循环切换到每个buffer名上

<s-Tab> 打开一个和当前Buffer一样的tab，水平排列

<S-Tab> 向后循环切换到每个buffer名上

<Enter> 在打开光标所在的buffer

d       删除光标所在的buffer

在命令模式下：
:bn   打开当前buffer的下一个buffer

:bp   打开当前buffer的前一个buffer

:b"num"   打开指定的buffer，"num"指的是buffer开始的那个数字，比如上图，我想打开list_audit.erb，输入:b7就ok了
```

### Vundle 的命令
```
:BundleList -列举出列表中(.vimrc中)配置的所有插件
:BundleInstall -安装列表中全部插件
:BundleInstall! -更新列表中全部插件
:BundleSearch foo -查找foo插件
:BundleSearch! foo -刷新foo插件缓存
:BundleClean -清除列表中没有的插件
:BundleClean! -清除列表中没有的插件
```
目前配置如下，后续有需要再进行配置
```
syn on                      "语法支持                                                                       

"common conf {{             通用配置
set ai                      "自动缩进
set bs=2                    "在insert模式下用退格键删除
set showmatch               "代码匹配
set laststatus=2            "总是显示状态行
set expandtab               "以下三个配置配合使用，设置tab和缩进空格数
set shiftwidth=4
set tabstop=4
set ruler                   "显示标尺
set showmatch               "显示匹配的括号
set cursorline              "为光标所在行加下划线
set number                  "显示行号
set autoread                "文件在Vim之外修改过，自动重新读入
set ignorecase              "检索时忽略大小写
set fileencoding=gb18030
set fileencodings=utf-8,gb18030,utf-16,big5
set hls                     "检索时高亮显示匹配项
set helplang=cn             "帮助系统设置为中文
set foldmethod=syntax       "代码折叠
set scrolloff=3             "顶部底部保持3行距离
"}}

set ignorecase              "检索时忽略大小写
let mapleader = ','         "conf for tabs, 为标签页进行的配置，通过ctrl h/l切换标签等
nnoremap <C-l> gt
nnoremap <C-h> gT
nnoremap <leader>t : tabe<CR>

set guifont=PowerlineSymbols\ for\ Powerline        "状态栏的配置 
set nocompatible
set t_Co=256
let g:Powerline_symbols = 'fancy'

" vundle 插件配置
set nocompatible " be iMproved, required
filetype off " required

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
"call vundle#begin('~/some/path/here')

Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'        " 加入NERDTree 
let NERDTreeWinPos='right'
let NERDTreeWinSize=30
map <C-f> :NERDTreeToggle<CR>
Plugin 'bling/vim-airline'          " 状态栏配置
set laststatus=2

call vundle#end() " required
filetype plugin indent on " required
" Brief help
" :PluginList - lists configured plugins
" :PluginInstall - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean - confirms removal of unused plugins; append `!` to auto-approve removal
```
---

# 基本操作

1. 光标在屏幕文本中的移动既可以用箭头键，也可以使用 hjkl 字母键。
    - h (左移)
    - j (下行)
    - k (上行)
    - l (右移)
2. 欲进入 Vim 编辑器(从命令行提示符)，请输入：`vim 文件名 <回车>`
3. 欲退出 Vim 编辑器，请输入` <ESC>   :q!   <回车>` 放弃所有改动。或者输入` <ESC>   :wq   <回车> `保存改动。
4. 在正常模式下删除光标所在位置的字符，请按： `x`
5. `a、i 和 A` 都会带您进入插入模式，惟一的区别在于字符插入的位置
- ` i   输入欲插入文本   <ESC>`：在光标前插入文本

- `A   输入欲添加文本   <ESC>`：在一行后添加文本:

- `a	输入欲插入文本`：在光标后插入文本

6. 	移动光标

- e	    向后移动到一个单词的结尾
- w	    向后移动到一个单词的开头
- b     向前移动到一个单词的开头
- 0 	数字零，到行头
- ^     到本行第一个不是`blank`字符的位置（所谓`blank`字符就是空格，tab，换行，回车等）
- $	    到本行行尾
- g_ 	到本行最后一个不是`blank`字符的位置。
`/pattern` 	搜索 `pattern` 的字符串（陈皓注：如果搜索出多个匹配，可按n键到下一个）
7. v 	进入可视，进行选择

特别提示：按下 `<ESC>` 键会带您回到正常模式或者撤消一个不想输入或部分完整
的命令。

## 关于命令和对象

在正常模式下修改命令的格式是：
    `operator   [number]   motion`

其中：
      
```
operator 	- 操作符，代表要做的事情，比如d代表删除
[number] 	- 可以附加的数字，代表动作重复的次数
motion   	- 动作，代表在所操作的文本上的移动

例如 w 代表单词(word)，$ 代表行末等等。
如：使用删除操作符 d 的删除命令格式如下：
d motion
```
其中：

```
d		-删除操作符
motion	-操作符的操作对象
```

一个简短的动作列表：

```
w		-从当前光标当前位置直到下一个单词起始处，不包括它的第一个字符(其实是包含的)
e		-从当前光标当前位置直到单词末尾，包括最后一个字符
$		-从当前光标位置直到当前行末
```

## 使用计数指定动作
在动作前输入数字会使它重复那么多次
如：

```
0	-移动行标到行首
2w	-使光标向前移动两个单词
3e	-使光标向前移动到第三个单词的末尾
r	-替换
```

## 定位及文件状态

```
CTRL-G		显示当前编辑文件中当前光标所在行位置以及文件状态信息
G			使当前光标跳转到文件中的最后一行
gg			使当前怪表跳转到文件第一行
行号+G		返回到第一次按下CTRL-G所在的行
```

# 文本操作

## 删除类命令

```
dw	-从光标处删除至一个单词的末尾,会包括空格
de	-从当前光标当前位置直到单词末尾，包括最后一个字符，不包括空格
d$	-从当前光标删除到行末
```
使用操作符时输入数字可以使它重复那么多次

- 在 d motion 中间加入 number 以删除更多，如d3e
使用dd可以删除整一个当前行
- 在命令前加数字如：3dd，可删除三行

## 撤销类命令

```
u		-撤销最后执行的命令
U		-撤销对整行的修改
CTRL-R	-撤销以前的撤销命令，恢复以前的操作结果
```

## 置入类命令

```
p		-输入 p 将最后一次删除的内容置入光标之后，如果删除的是一个整行，那么该行将至于当前光标所在的下一行。
```

## 替换类命令

```
r		-输入 r 和一个字符替换光标所在位置的字符
```

## 更改类命令

```
ce/cw	-要改变文本直到一个单词的末尾，请输入 ce/cw（会直接进入插入模式）
c$	    -替换当前光标到行末的内容
```

## 使用计数操作

```
c  [number] motion	-使得从当前光标处至行末的全部都可被更改。
```

## 搜索类命令

```
/   + 字符串	-用以在当前文件中查找该字符串
n	-查找同上一次的字符串
N	-相反方向查找同上一次的字符串
?   + 字符串	-逆向查找字符串
回到之前的位置按CTRL-0，重复按可以退回更多步，CTRL-I 会跳转到较新的位置。
如果查找已经到达文件末尾，查找会自动从文件头部继续查找，除非‘wrapscan’选项被复位。
```

## 配对括号的查找

```
%		-输入 % 可以查找配对的括号如： ）、]、}。
```

## 替换命令

```
:s/old/new			-在一行内替换头一个字符串 old 为新的字符串 new
:s/old/new/g		-在一行内替换所有的字符串 old 为新的字符串 new
:#,#s/old/new/g	    -在两行内替换所有的字符串 old 为新的字符串 new	 
:%s/old/new/g		-在文件内替换所有的字符串 old 为新的字符串 new  
:%s/old/new/gc		-进行全文替换时询问用户确认每个替换需添加 c 标志       
R					-输入大写的 R 可连续替换多个字符
```

## vim内执行外部命令

```
:! command		-输入 :! 
然后紧接着输入一个外部命令可以执行该外部命令，如：ls、dir等
```

## 打开类命令

```
o		-输入 o 将在光标的下方打开新的一行并进入插入模式
O		-输入O将在光标的上方打开新的一行并进入插入模式
```

## 复制粘贴文本命令

```
y		-复制文本
p		-粘贴文本
```

## 折叠代码
vim折叠的方式, 有几种: manual, indent , marker当折叠方式采用indent方式时：
在.vimrc文件中设置
`set foldmethod=indent`
```
zn  打开所有
zm  关闭所有
zc	折叠
zC	对所在范围内所有嵌套的折叠点进行折叠
zo	展开折叠
zO	对所在范围内所有嵌套的折叠点展开
[z	到当前打开的折叠的开始处。
]z	到当前打开的折叠的末尾处。
zj	向下移动。到达下一个折叠的开始处。关闭的折叠也被计入。
zk	向上移动到前一折叠的结束处。关闭的折叠也被计入。
```


# 文件操作
## vim保存文件

```
:w FILENAME			-将对文件的改动保存到文件中，并命名该文件
v motion :w FILENAME	-保存部分文本到文件中
1. 将光标停留在要保存区域的开始，按v键，移动光标选择区域范围
2. 选定范围之后按 ：键，会出现:'<,'> 
3. 现在输入 w 文件名。将会保存它
```

## 提取和合并文件

```
:r FILENAME			-向当前文件中插入另外的文件的内容
:r !dir/ls 			-读取 dir/ls 命令的输出并将其放置到当前文件的光标位置后面。
```

## 设置类命令的选项

```
:set xxx                -可以设置 xxx 选项。一些有用的选项如下： 在选项前加上 no 可以关闭选项：  :set noic
'ic' 'ignorecase'       -查找时忽略字母大小写
:set noic		        -移除设置的选项
'is' 'incsearch'        -查找短语时显示部分匹配
'hls' 'hlsearch'        -高亮显示所有的匹配短语
:nohlssearch	        -移除匹配项的高亮显示
```

## vim帮助系统

```
按下 <HELP> 键 (如果键盘上有的话)
按下 <F1> 键 (如果键盘上有的话)
输入  :help  command <回车>
:help user-manual vim用户手册
```

## vim创建启动脚本
创建一个.vimrc 文件
1. 开始编辑 vimrc文件，具体命令取决于您所使用的操作系统：
        
```
:edit ~/.vimrc          这是 Unix 系统所使用的命令
:edit $VIM/_vimrc       这是 MS-Windows 系统所使用的命令
```

2. 接着读取 vimrc 示例文件的内容：
        	
```
:r $VIMRUNTIME/vimrc_example.vim
```

3. 保存文件，命令为：
      		
```
:write
```
## 帮助文档
```
:help vimrc-intro	-查看vimrc 的帮助文档
```


## vim补全

```
CTRL-D		-可以查看可能的补全结果
TAB			-使用一个补全
```

## 学习资料

```
Vim - Vi Improved
- 作者：Steve Oualline
- 出版社：New Riders
这是第一本完全讲解 Vim的书籍。它对于初学者特别有用。其中包含有大量实例和图示。
欲知详情，请访问 http://iccf-holland.org/click5.html
以下这本书比较老了而且内容更多是关于 Vi 而非 Vim，但是也值得推荐：
    Learning the Vi Editor 
    - 作者：Linda Lamb
    - 出版社：O'Reilly & Associates Inc.
这是一本不错的书，通过它您几乎能够了解到任何您想要使用 Vi 做的事情。此书的第六个版本也包含了一些关于 Vim 的信息。
```

---
## vim编辑命令

```
进入vim 某文件      vim  xx.xx
插入修改            shift +i
退出插入模式        esc
保存退出            shift +  :wq
```

## vim保存命令

```
:wq   保存后退出vi，若为 :wq! 则为强制储存后退出（常用）
:w    保存但不退出（常用）
:w!   若文件属性为『只读』时，强制写入该档案
:q    离开 vim（常用）
:q!   若曾修改过档案，又不想储存，使用 ! 为强制离开不储存档案。
:e!   将档案还原到最原始的状态
```

## vim开启Mac自带的服务器

```
开启server
sudo apachectl start
python -m SimpleHTTPServer
正常关闭进程  ctrl+c
强制关闭进程  ctrl+z
查看进程占用  lsof -i tcp:[端口号]
通过pid杀死进程 kill pid
```

## 查看文件

```
ls -a 显示隐藏文件
ls -l  看到更多的内容
mv a b 将文件重命名为b
```

## 删除文件

```
rm -f a     直接删除a 不进行确认 

Vim 文件关键字搜索命令

vimgrep /匹配模式/[g][j] 要搜索的文件/范围
g：表示是否把每一行的多个匹配结果都加入
j：表示是否搜索完后定位到第一个匹配位置
vimgrep /pattern/ %           在当前打开文件中查找
vimgrep /pattern/ *           在当前目录下查找所有
vimgrep /pattern/ **          在当前目录及子目录下查找所有
vimgrep /pattern/ **/*        只查找子目录
```
## Vim文件查找跳转

```
:cn 查找下一个
:cp 查找上一个

查找的结果可以用":copen"命令查看,在列表里,将光标移动至相应的位置,按回车就打开对应的文件了
```

## mac osx显示隐藏文件

```
defaults write com.apple.finder AppleShowAllFiles -bool true
```
注意：设置完毕后finder需要重新启动 command+option+esc