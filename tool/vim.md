### gvim 安装vundle
https://github.com/VundleVim/Vundle.vim
普通模式
w	移动到下一个单词
b	移动到上一个单词

从普通模式进入插入模式
i	在当前光标处进行编辑
I	在行首插入
A	在行末插入
a	在光标后插入编辑
o	在当前行后插入一个新行
O	在当前行前插入一个新行
cw	替换从光标所在位置后到一个单词结尾的字符

从普通模式输入:进入命令行模式，输入w回车，保存文档。输入:w 文件名可以将文档另存为其他文件名或存到其它路径下

以下为其它几种退出方式：

命令	说明
:q!	强制退出，不保存
:q	退出
:wq!	强制保存并退出
:w <文件路径>	另存为
:saveas 文件路径	另存为
:x	保存并退出
:wq	保存并退出

普通模式下输入Shift+zz即可保存退出vim

进入普通模式，使用下列命令可以进行文本快速删除：

命令	说明
x	删除游标所在的字符
X	删除游标所在前一个字符
Delete	同x
dd	删除整行
dw	删除一个单词（不适用中文）
d$或D	删除至行尾
d^	删除至行首
dG	删除到文档结尾处
d1G	删至文档首部
2dd表示一次删除2行

在普通模式下.(小数点)表示重复上一次的命令操作

进入普通模式输入N<command>，N表示重复后面的次数
输入10x，删除10个连续字符
输入3dd，将会删除3行文本

在普通模式下，你还可以使用dw或者daw(delete a word)删除一个单词，所以你可以很容易的联想到dnw(n替换为相应数字)表示删除n个单词

1.行间跳转

命令	说明
nG(n Shift+g)	游标移动到第 n 行(如果默认没有显示行号，请先进入命令模式，输入:set nu以显示行号)
gg	游标移动到到第一行
G(Shift+g)	到最后一行
你在完成依次跳转后，可以使用Ctrl+o快速回到上一次(跳转前)光标所在位置,

行内跳转

普通模式下使用下列命令在行内按照单词为单位进行跳转

命令	说明
w	到下一个单词的开头
e	到下一个单词的结尾
b	到前一个单词的开头
ge	到前一个单词的结尾
0或^	到行头
$	到行尾
f<字母>	向后搜索<字母>并跳转到第一个匹配的位置(非常实用)
F<字母>	向前搜索<字母>并跳转到第一个匹配的位置
t<字母>	向后搜索<字母>并跳转到第一个匹配位置之前的一个字母(不常用)
T<字母>	向前搜索<字母>并跳转到第一个匹配位置之后的一个字母(不常用)

普通模式中使用y复制

普通模式中，yy复制游标所在的整行（3yy表示复制3行）
普通模式中，y^ 复制至行首，或y0。不含光标所在处字符。
普通模式中，y$ 复制至行尾。含光所在处字符。
普通模式中，yw 复制一个单词。
普通模式中，y2w 复制两个单词。
普通模式中，yG 复制至文本末。
普通模式中，y1G 复制至文本开头。
普通模式中使用p粘贴

普通模式中，p(小写)代表粘贴至光标后（下）
普通模式中，P(大写)代表粘贴至光标前（上）

其实前面讲得dd删除命令就是剪切，你每次dd删除文档内容后，便可以使用p来粘贴，也这一点可以让我们实现一个很爽快的功能——交换上下行：

ddp,就这么简单，即实现了快速交换光标所在行与它下面的行

1.替换和撤销(Undo)命令

替换和Undo命令都是针对普通模式下的操作

命令	说明
r+<待替换字母>	将游标所在字母替换为指定字母
R	连续替换，直到按下Esc
cc	替换整行，即删除游标所在行，并进入插入模式
cw	替换一个单词，即删除一个单词，并进入插入模式
C(大写)	替换游标以后至行末
~	反转游标所在字母大小写
u{n}	撤销一次或n次操作
U(大写)	撤销当前行的所有修改
Ctrl+r	redo，即撤销undo的操作

:set shiftwidth?
设置缩进为10个字符

:set shiftwidth=10
Vim多行缩进技巧
1.按v进入visual状态，选择多行，用>或<缩进或缩出

2. 通常根据语言特征使用自动缩进排版：在命令状态下对当前行用== （连按=两次）, 或对多行用n==（n是自然数）表示自动缩进从当前行起的下面n行。你可以试试把代码缩进任意打乱再用n==排版，相当于一般IDE里的code format。使用gg=G可对整篇代码进行排版。
3.gg   shift+G 首尾
4.全文字眼替换  %s/source/dist/g 或者 :1,$ s/source/dist/g
　　:s/vivian/sky/ 替换当前行第一个 vivian 为 sky
　　:s/vivian/sky/g 替换当前行所有 vivian 为 sky
　　:n,$s/vivian/sky/ 替换第 n 行开始到最后一行中每一行的第一个 vivian 为 sky
　　:n,$s/vivian/sky/g 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky
　　n 为数字，若 n 为 .，表示从当前行开始到最后一行
　　:%s/vivian/sky/(等同于 :g/vivian/s//sky/) 替换每一行的第一个 vivian 为 sky
　　:%s/vivian/sky/g(等同于 :g/vivian/s//sky/g) 替换每一行中所有 vivian 为 sky
　　可以使用 # 作为分隔符，此时中间出现的 / 不会作为分隔符
　　:s#vivian/#sky/# 替换当前行第一个 vivian/ 为 sky/
　　:%s+/oradata/apras/+/user01/apras1+ (使用+ 来 替换 / )： /oradata/apras/替换成/user01/apras1/
　　* ************************************
　　1.:s/vivian/sky/ 替换当前行第一个 vivian 为 sky
　　:s/vivian/sky/g 替换当前行所有 vivian 为 sky
　　2. :n,$s/vivian/sky/ 替换第 n 行开始到最后一行中每一行的第一个 vivian 为 sky
　　:n,$s/vivian/sky/g 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky
　　(n 为数字，若 n 为 .，表示从当前行开始到最后一行)
　　3. :%s/vivian/sky/(等同于 :g/vivian/s//sky/) 替换每一行的第一个 vivian 为 sky
　　:%s/vivian/sky/g(等同于 :g/vivian/s//sky/g) 替换每一行中所有 vivian 为 sky
　　4. 可以使用 # 作为分隔符，此时中间出现的 / 不会作为分隔符
　　:s#vivian/#sky/# 替换当前行第一个 vivian/ 为 sky/
　　5. 删除文本中的^M
　　问题描述：对于换行,window下用回车换行(0A0D)来表示，linux下是回车(0A)来表示。这样，将window上的文件拷到unix上用时，总会有个^M.请写个用在unix下的过滤windows文件的换行符(0D)的shell或c程序。
　　· 使用命令：cat filename1 | tr -d “^V^M” > newfile;
　　· 使用命令：sed -e “s/^V^M//” filename > outputfilename。需要注意的是在1、2两种方法中，^V和^M指的是Ctrl+V和Ctrl+M。你必须要手工进行输入，而不是粘贴。
　　· 在vi中处理：首先使用vi打开文件，然后按ESC键，接着输入命令：%s/^V^M//。
　　· :%s/^M$//g
　　如果上述方法无用，则正确的解决办法是：
　　· tr -d "\r" < src >dest
　　· tr -d "\015" dest
　　· strings A>B
　　6. 其它
　　利用 :s 命令可以实现字符串的替换。具体的用法包括：
　　:s/str1/str2/ 用字符串 str2 替换行中首次出现的字符串 str1
　　:s/str1/str2/g 用字符串 str2 替换行中所有出现的字符串 str1
　　:.,$ s/str1/str2/g 用字符串 str2 替换正文当前行到末尾所有出现的字符串 str1
　　:1,$ s/str1/str2/g 用字符串 str2 替换正文中所有出现的字符串 str1
　　:g/str1/s//str2/g 功能同上
　　从上述替换命令可以看到：g 放在命令末尾，表示对搜索字符串的每次出现进行替换;不加 g，表示只对搜索
　　字符串的首次出现进行替换;g 放在命令开头，表示对正文中所有包含搜索字符串的行进行替换操作。


3.调整文本位置

命令行模式下输入:ce(center)命令使本行内容居中

:ce
命令行模式下输入:ri(right)命令使本行文本靠右

:ri
命令行模式下输入:le(left)命令使本行内容靠左

:le

1.快速查找

普通模式下输入/然后键入需要查找的字符串 按回车后就会进行查找。 ？与/功能相同，只不过？是向上而/是向下查找。 进入查找之后，输入n和N可以继续查找 n表示继续查找，N反向查找

高级查找

普通模式下输入\*寻找游标所在处的单词
普通模式下输入\#同上，但 \* 是向前（上）找，#则是向后（下）找
普通模式下输入g\*同\* ，但部分符合该单词即可
普通模式下输入g\#同\# ，但部分符合该单词即可

### 文件管理
另一种就是进入vim后再编辑其他的文件。 同时创建两个新文件并编辑

$ vim 1.txt 2.txt
默认进入1.txt文件的编辑界面

命令行模式下输入:n编辑2.txt文件，可以加!即:n!强制切换，之前一个文件的输入没有保存，仅仅切换到另一个文件
命令行模式下输入:N编辑1.txt文件，可以加!即:N!强制切换，之前文件内的输入没有保存，仅仅是切换到另一个文件
2.进入vim后打开新文件

命令行模式下输入:e 3.txt 打开新文件3.txt
命令行模式下输入:e# 回到前一个文件
命令行模式下输入:ls可以列出以前编辑过的文档
命令行模式下输入:b 2.txt（或者编号）可以直接进入文件2.txt编辑
命令行模式下输入:bd 2.txt（或者编号）可以删除以前编辑过的列表中的文件项目
命令行模式下输入:e! 4.txt，新打开文件4.txt，放弃正在编辑的文件
命令行模式下输入:f 显示正在编辑的文件名
命令行模式下输入:f new.txt，改变正在编辑的文件名字为new.txt



在普通模式下输入v（小写），进入字符选择模式，就可以移动光标，光标走过的地方就会选取。再次按下v会后就会取消选取。
在普通模式下输入Shift+v（小写），进入行选择模式，按下V之后就会把整行选取，您可以上下移动光标选更多的行，同样，再按一次Shift+v就可以取消选取。
在普通模式下输入 Ctrl+v（小写），这是区域选择模式，可以进行矩形区域选择，再按一次Ctrl+v取消选取。
在普通模式下输入d删除选取区域内容
在普通模式下输入y复制选取区域内容


### 窗口管理  
1. 除了:new命令，下述列举的多种方法也可以在命令模式或普通模式下打开新的视窗：

	* 命令行模式下输入:sp 1.txt 打开新的横向视窗来编辑1.txt
	* 命令行模式下输入:vsp 2.txt 打开新的纵向视窗来编辑1.txt
	* 普通模式下Ctrl-w s 将当前窗口分割成两个水平的窗口
	* 普通模式下Ctrl-w v 将当前窗口分割成两个垂直的窗口
	* 普通模式下Ctrl-w q 即 :q 结束分割出来的视窗。如果在新视窗中有输入需要使用强制符！即:q!
	* 普通模式下Ctrl-w o 打开一个视窗并且隐藏之前的所有视窗
	* 普通模式下Ctrl-w j 移至下面视窗
	* 普通模式下Ctrl-w k 移至上面视窗
	* 普通模式下Ctrl-w h 移至左边视窗
	* 普通模式下Ctrl-w l 移至右边视窗
	* 普通模式下Ctrl-w J 将当前视窗移至下面
	* 普通模式下Ctrl-w K 将当前视窗移至上面
	* 普通模式下Ctrl-w H 将当前视窗移至左边
	* 普通模式下Ctrl-w L 将当前视窗移至右边
	* 普通模式下Ctrl-w - 减小视窗的高度
	* 普通模式下Ctrl-w + 增加视窗的高度

### 创建加密文档

>`$ vim -x file1`  
输入您的密码 确认密码 这样在下一次打开时，vim就会要求你输入密码

### 在vim执行外部(shell)命令

* 在命令行模式中输入!可以执行外部的shell命令

* :!ls 用于显示当前目录的内容
* :!rm FILENAME用于删除名为 FILENAME 的文件
* :w FILENAME可将当前 VIM 中正在编辑的文件另存为 FILENAME 文件

获取目前的设定

命令行模式下输入:set或者:se显示所有修改过的配置
命令行模式下输入:set all 显示所有的设定值
命令行模式下输入:set option? 显示option的设定值
命令行模式下输入:set nooption 取消当期设定值
:sy on 语法高亮
:set go=
:colo (tabs)
:tabnew (tabs/enter)
set guifont=Consolas\ 12 设置默认字体
：reg 12个粘贴板
删除空白行
：g/^\s*$/d

x        删除当前光标下的字符
dw       删除光标之后的单词剩余部分。
d$       删除光标之后的该行剩余部分。
dd       删除当前行。

c        功能和d相同，区别在于完成删除操作后进入INSERT MODE
cc       也是删除当前行，然后进入INSERT MODE
删除每行第一个字符    :%s/^.//g

## 插入补全 和 正则搜索
 在插入模式下，为了减少重复的击键输入，VIM 提供了若干快捷键，当你要输入某个上下文曾经输入过的字符串时，你只要输入开头若干字符，使用快捷键，VIM 将搜索上下文，找到匹配字符串，把剩下的字符补全，你就不必敲了。这样，编程序时你起多长的变量名都没关系了，:-) 而且还可以减少输入错误。我认为，插入补全是 VIM 最为突出的一项功能。


 i<C-P>   向上搜索，补全一个词。例如，上文中出现过 filename 这个词，当你想再输入 filename 时，只要按 f<C-P> 即可。假如 VIM 向上搜索，找到以 f 开头的第一个匹配不是 filename，你可以继续按 <C-P> 搜索下一个匹配进行补全。当然，如果你想一次 <C-P> 就成功，你可以多输入几个字符比如 filen 再按 <C-P> 补全

 i<C-N>   向下搜索，补全一个词

 i<C-X><C-L>      补全一行。比如你写过一行 for (int i = 0; i < 100; i++)，你想再写一模一样的一行，只要输入 for<C-X><C-L> 即可。如果补全出来的不是你想要的那一行，你可以按 <C-P> 或 <C-N> 选择上一个或下一个匹配行
 i<C-X><C-F>      在文件系统中搜索，补全一个文件名

 如果按 <C-P> 或 <C-N> 补全一个词，在当前文件中没有找到匹配，VIM 将搜索 #include 语句中的文件，而文件的位置将在 path 中搜索。

 搜索字符串用的是正规表达式(Regular expression)，其中许多字符都有特殊含义：
 \        取消后面所跟字符的特殊含义。比如
 vim
 匹配字符串“[vim]”
 []       匹配其中之一。比如 [vim] 匹配字母“v”、“i”或者“m”，[a-zA-Z] 匹配任意字母
 [^]      匹配非其中之一。比如 [^vim] 匹配除字母“v”、“i”和“m”之外的所有字符
 .        匹配任意字符
 *        匹配前一字符大于等于零遍。比如 vi*m 匹配“vm”、“vim”、“viim”……
 \+       匹配前一字符大于等于一遍。比如 vi\+m 匹配“vim”、“viim”、“viiim”……
 \?       匹配前一字符零遍或者一遍。比如 vi\?m 匹配“vm”或者“vim”
 ^        匹配行首。例如 /^hello 查找出现在行首的单词 hello
 $        匹配行末。例如 /hello$ 查找出现在行末的单词 hello
      括住某段正规表达式
      \数字    重复匹配前面某段括住的表达式。例如 hello.*\1 匹配一个开始和末尾都是“hello”，中间是任意字符串的字符串

      对于替换字符串，可以用“&”代表整个搜索字符串，或者用“\数字”代表搜索字符串中的某段括住的表达式。

      举一个复杂的例子，把文中的所有字符串“abc……xyz”替换为“xyz……abc”可以有下列写法：
      :%s/abc.∗xyz/xyz\1abc/g
      :%s/abc.∗xyz/\3\2\1/g
      其它关于正规表达式搜索替换的更详细准确的说明请看 :help pattern

      例如：在文本中搜索所有包含amount大于0的以[ ] 括住的字符串的行，如 “amount[123]“,  ”amount[200]“ 等：

                首先按 ：进入命令 模式，然后输入下面的串再回车开始查找：/amount\[[1-9]\([0-9]*\)\+\]

		     解释如下：

		           /  表示进行串搜索, 其它字符为 正则表达式的内容

			        amount  表示匹配串包含amount

				     \[  转义字符，表示匹配左中括号 [

				          [1-9]  表示匹配一位1到9之间任何数字

					          转义的左右括号，表示括住某段正则表达式，

						      \+  转义字符+，表示前面一个字符或一个正则串重复1次或多次，所以，\([0-9]*\) 表示 任意个0-9之间的数字

						          \]   转义字符 ]


## vim 键映射
* vim 有多个模式并不是什么大问题，但在模式间切换的时候会感觉很糟。ESC 键有点远，这太麻烦了。当我面对新的 vim 环境时，所做的第一件事就是添加如下映射
> inoremap jj <ESC>