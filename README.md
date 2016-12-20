# WiKi
## win10小狼毫兼容问题(删除注册表):
1. `HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/CTF/TIP/`下搜索"小狼毫".
2. 在上一层的Category目录下找到所有的`{13A016DF-560B-46CD-947A-4C3AF1E0E35D}`(一共两个),删除这两个注册表.

## vim-airline显示问题：
1. 需要特殊字体,可从airline官网下载.
2. (win)设置vim字体:
	- `set guifont=*`选中想要的字体.
	- 然后再`:set guifont`得到已经临时设置的字体的名称.
	- 在_vimr中添加得到的字体名称.
3. gvim for win 中字体间的空格可以用`_`代替，linux 中可用`\ `代替.

## win10 mysql的zip压缩包安装方式：
1. 账户密码:
        
        username:root  
        password:root

2. 解压zip压缩包到指定文件夹.
3. 新建一个my.ini配置文件：
        
        [mysql]
        ; 设置mysql客户端默认字符集
        default-character-set=utf8
        [mysqld]
        ;设置3306端口
        port = 3306 
        ; 设置mysql的安装目录
        basedir=E:\mysql5.7
        ; 设置mysql数据库的数据的存放目录
        datadir=E:\mysql5.7\data
        ; 允许最大连接数
        max_connections=200
        ; 服务端使用的字符集默认为8比特编码的latin1字符集
        character-set-server=utf8
        ; 创建新表时将使用的默认存储引擎
        default-storage-engine=INNODB 

3. 以管理员身份打开cmd窗口后，将目录切换到你的解压文件bin目录下。再输入`mysqld install`回车运行就可以了，注意是`mysqld`不是`mysql`.
4. 接下来执行`mysqld  --initialize` 初始化data目录.(mysql会自动新建date文件夹)
5. 在提示命令管理工具输入如下命令,进入安全模式：`mysqld --defaults-file="E:\mysql5.7\my.ini" --console --skip-grant-tables`,路径根据安装的实际路径修改,保持该窗口运行.
6. 然后以管理员权限打开新的命令提示窗口,cd到mysql的bin目录.
7. 修改密码,`use mysql;`,`update user set authentication_string=password("此处输入密码") where user="root"`
8. 刷新数据库`flush privileges;`
9. 添加mysql的bin目录到Path环境变量.
10. [百度经验][1]

## Java环境变量配置:
- 安装目录结构:
        
        D:\Java\---jdk  
                ---jre

- 用户环境变量配置:
        
        JAVA_HOME:      `D:\Java\jdk`(jdk安装目录)
        CLASS_PATH:     `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`
        PATH:           `;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`

## CapsLock键与L-Ctrl互换:
1. `win+R`+`regedit`打开注册表.
2. `HKEY_LOCAL_MACHINE`-->`System`-->`CurrentControlSet`-->`Control`-->`KeyBoard Layout`(不是Layouts).
3. 新建二进制值`New`-->`Binary value`.
4. 重命名:`New Value #1`-->`Scancode Map`.
5. `Scancode Map`-->`Modify`.
6. 输入:
		
		0000  00 00 00 00 00 00 00 00
		0008  03 00 00 00 1D 00 3A 00
		0010  3A 00 1D 00 00 00 00 00
		0018

## PortableGit设置.ssh:
1. 打开`git-bash.exe`-->`ssh-keygen -t rsa -C “username@example.com”`,然后一路next.
2. 在user目录下的.ssh文件夹中打开`id_rsa.pub`,把其中的内容填到github的ssh中.

## ConEmu 
1. Startup-->Command line: `%windir%\system32\bash.exe ~ -cur_console:p1`(直接启动bash,主目录)

## 实用的PY:
1. python -m SimpleHTTPServer [port]
2. python -m http.server [port]

[1]:http://jingyan.baidu.com/article/af9f5a2d16fa4d43150a4552.html
