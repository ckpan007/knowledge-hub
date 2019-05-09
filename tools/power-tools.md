

# Unix/BSD/Linux/Cygwin
* awk, sed 是最常用的文本处理工具
* grep 搜索文件内容, fgrep, egrep 等等都是 grep 的快捷方式
* find 支持很多很复杂的规则来查找并处理文件
* dirname, basename 获取文件路径或者文件名
* mktemp 生成临时文件或者目录
* cut, paste, join 分割与合并文本
* tac 反向输出文件内容
* sort 进行排序
* uniq 把已经排序过的文本去掉重复
* wc 统计行数
* bc 计算器
* tee 输出到控制台的同时，也要保存到文件
* tail 滚动查看日志
* diff 对比文件
* [colordiff](https://www.colordiff.org/) 用不同的颜色区分 diff 结果
* [icdiff](http://www.jefftk.com/icdiff) 另一个增强的支持高亮的 diff 工具
* [colortail](https://github.com/joakim666/colortail) 高亮的 tail 应用
* [mawk – pattern scanning and text processing language](https://invisible-island.net/mawk/), 一个交互式的 AWK
* dos2unix, unix2dos 转换文件的换行符
* dig, whois, nslookup 域名相关工具
* timeout 限定程序必须在指定时间内结束，否则会杀掉此程序
* wget 下载工具
* curl 也是一个下载工具，但经常被用于 web 开发和调试
* [GNU screen](https://www.gnu.org/software/screen/), [tmux](https://tmux.github.io/), [byobu](http://byobu.co/) 多窗口的终端，可以保证在注销以后程序保持执行。Byobu 是 screen 和 tmux 的一个前端，增强了很多的功能
* pkill 按进程的名字来杀掉
* pgrep 按进程的名字来搜索，使用正则表达式
* tree 输出目录的树形结构
* pstree 输出进程是树形结构
* top 查看当前系统的执行状况
* nohup 让程序忽略 HUP 信号
* lsof 查看开启的套接字和文件
* rsync 同步文件，支持本地与远程
* [laurent22/rsync-time-backup: Time Machine style backup with rsync](https://github.com/laurent22/rsync-time-backup).
* xargs 把输入作为命令的参数，可以让命令分批执行
* [parallel](https://savannah.gnu.org/projects/parallel/) 更高级的 xargs，支持跨机器执行
* 推荐看官方的视频 https://www.youtube.com/watch?v=OpaiGYxkSuQ&list=PL284C9FF2488BC6D1
* netstat 查看网络
* [pv](https://www.ivarch.com/programs/pv.shtml) 用管道传输数据的时候显示进度条
* nc 一个网络的瑞士军刀级别的工具
* [peco](https://github.com/peco/peco) 通过管道来手工过滤并选择
* [fzy: A better fuzzy finder](https://github.com/jhawthorn/fzy) 另一个更简单一些的模糊匹配搜索的工具，类似 peco，而且可以和 VIM 整合
* [pick](https://github.com/calleerlandsson/pick) 也是一个类似 peco 的工具
* [akavel/up: Ultimate Plumber is a tool for writing Linux pipes with instant live preview](https://github.com/akavel/up)
* [ack](https://beyondgrep.com/) 更高级的 grep，速度非常快
* [ag](https://github.com/ggreer/the_silver_searcher) 另一个 ack
* [jq](https://stedolan.github.io/jq/) 在命令行处理 json 格式
* antonmedv/fx: Command-line tool and terminal JSON viewer 🔥
* jo 在命令行生成 json 格式
* [shyaml](https://github.com/0k/shyaml) 在命令行处理 yaml 格式
* [mikefarah/yq: yq is a portable command-line YAML processor](https://github.com/mikefarah/yq) 也是一个在命令行处理 yaml 的工具，类似 jq
* [xmlstarlet](https://xmlstar.sourceforge.io/) 在命令行处理 xml 格式
* [jump](https://github.com/gsamokovarov/jump) 快速跳转目录，支持模糊匹配
* clvv/fasd: Command-line productivity booster, offers quick access to files and directories, inspired by autojump, z and v.: https://github.com/clvv/fasd
* [rlwrap](https://github.com/hanslub42/rlwrap) 让不支持 readline 的程序支持 readline
* [mitmproxy](https://mitmproxy.org/) 中间人代理服务器，可降级 https，用于开发
* [wuzz](https://github.com/asciimoo/wuzz) 支持 GUI 交互式操作的 curl
* [HTTPie](https://httpie.org/) 类似 curl，仅支持 http。但是使用更简单，支持语法高亮
* [socat](http://www.dest-unreach.org/socat/) 一个套接字代理及转换工具，比如把 socket 监听到特定的端口上
* [magic-wormhole](https://github.com/warner/magic-wormhole) 在两个机器之间点对点传输文件
* bats: Bash 自动化测试系统: https://github.com/sstephenson/bats
* [wait_on](https://www.freshports.org/sysutils/wait_on/) 监控文件系统的变化，可以配合实现实时处理的文件处理
* [watchexec](https://github.com/mattgreen/watchexec) 监控文件变化然后执行特定的命令
* [aria2](https://aria2.github.io/) 支持 http/https/ftp/bt/magnet 的下载工具
* [axel](https://github.com/eribertomota/axel) 命令行的多线程下载工具
* [You-Get](https://you-get.org/) 一个更智能一点儿的下载工具，类似 youtube-get，但还支持其他的格式
* [pssh](https://code.google.com/archive/p/parallel-ssh/) 并行 ssh 到机器上执行命令
* [osquery](https://osquery.io/) 使用 SQL 的语法来管理机器，比如查看进程和打开的文件
* [darkhttpd](https://unix4lyfe.org/darkhttpd/) 简单快速的 web server，比 python -mSimpleHTTPServer 性能好很多
* coway, cowthink, lolcat, figlet, toilet 有趣的 Ascii Art 应用
* [boxes](http://boxes.thomasjensen.com/) 把文字用注释框起来
* [pgcli](https://www.pgcli.com/) PostgreSQL 的命令行客户端，比自带的好用很多
* okbob/pspg: Postgres Pager: https://github.com/okbob/pspg
* [gotty](https://github.com/yudai/gotty) 结对工作的好工具，因为基于命令行和 web，所以速度超级快
* [ttyd - Share your terminal over the web](https://tsl0922.github.io/ttyd/) 另一个共享 terminal 的工具，从 GoTTY 这里获得灵感
* [shellshare - live terminal broadcast](https://shellshare.net/) 也是一个分享 terminal 的工具，会创建一个分享的 url 出来
* [Jeffail/leaps: A pair programming service using Operational Transforms](https://github.com/jeffail/leaps) 如果只是希望一起来编辑一个文件，leaps 通过 web 界面来允许多人实时编辑任意的文本文件
* [pipes.sh](https://github.com/pipeseroni/pipes.sh) Terminal 下的屏幕保护程序
* [mps-youtube](https://github.com/mps-youtube/mps-youtube) 在命令行下面浏览 YouTube
* [moreutils](https://joeyh.name/code/moreutils/)
* johnkerl/miller: Miller is like awk, sed, cut, join, and sort for name-indexed data such as CSV, TSV, and tabular JSON: https://github.com/johnkerl/miller
* SDKMAN! the Software Development Kit Manager: http://sdkman.io/
* [exa - A modern replacement for ls](https://the.exa.website/) 一个现代的 ls 命令，增强了很多功能，比如与 git 整合
* [sharkdp/fd: A simple, fast and user-friendly alternative to find](https://github.com/sharkdp/fd). 一个简单、快速、易用的 find
* [ctop](https://bcicen.github.io/ctop/) 容器的 top 命令，监控容器的运行状况
* pre-commit，一个通用的在提交代码之前的代码框架，可以用于检测是否包含敏感信息，去除空格，格式化代码等: http://pre-commit.com/
* aragozin/jvm-tools: Small set of tools for JVM troublshooting, monitoring and profiling. https://github.com/aragozin/jvm-tools
* Packer by HashiCorp，用于自动化构建虚拟机镜像，比如用于 Vagrant: https://www.packer.io/
* pressly/goose: Goose database migration tool - fork of https://bitbucket.org/liamstask/goose
* agedu: track down wasted disk space: https://www.chiark.greenend.org.uk/~sgtatham/agedu/
* willthames/ansible-lint: Best practices checker for Ansible: https://github.com/willthames/ansible-lint/
* Welcome to DocFX website! | DocFX website, .Net only: https://dotnet.github.io/docfx/
* [The MOST pager](http://www.jedsoft.org/most/) - less is more than more, most is more than less.
* moul/advanced-ssh-config: assh: ssh wrapper using ProxyCommand that adds regex, aliases, gateways, dynamic hostnames to SSH and ssh-config: https://github.com/moul/advanced-ssh-config
* [Masterminds/vert: Command line version testing: Compare versions at the CLI for use in shell scripts and make files](https://github.com/Masterminds/vert). 比较版本号的一个命令行工具
* p-e-w/maybe: :rabbit2: See what a program does before deciding whether you really want it to happen. https://github.com/p-e-w/maybe
* [Sshguard](https://www.sshguard.net/) sshguard protects hosts from brute-force attacks against SSH and other services.
* GNU Source-highlight - GNU Project - Free Software Foundation (FSF): https://www.gnu.org/software/src-highlite/
* [RedPen](http://redpen.cc/) is a proofreading tool to help writers or programmers who write technical documents or manuals that need to adhere to a writing standard.
* [Dockerfile Linter](http://hadolint.lukasmartinelli.ch/)
* DAG: unoconv: Convert between any document format supported by OpenOffice: http://dag.wiee.rs/home-made/unoconv/
* [rclone - rsync for cloud storage](https://rclone.org/), Rclone is a command line program to sync files and directories to and from: local/sftp/Google drive/AWS S3/Box/Dropbox/…
* [chneukirchen/nq](https://github.com/chneukirchen/nq): Unix command line queue utility
* restic · Backups done right! https://restic.github.io/
* tomnomnom/gron: Make JSON greppable! https://github.com/tomnomnom/gron
* dvorka/hstr: Bash and Zsh shell history suggest box - easily view, navigate, search and manage your command history. https://github.com/dvorka/hstr
* [ditaa](http://ditaa.sourceforge.net/), ditaa is a small command-line utility written in Java, that can convert diagrams drawn using ascii art (‘drawings’ that contain characters that resemble lines like | / - ), into proper bitmap graphics.
* whohas: software package and repository meta-search: http://www.philippwesche.org/200811/whohas/intro.html
* [MyTop](http://www.mysqlfanboy.com/mytop-3/) is a console-based (non-gui) tool for monitoring the threads and overall performance of a MySQL.
* lunaryorn/mdcat: Cat for markdown: Show markdown documents in TTYs: https://github.com/lunaryorn/mdcat
* MAT: Metadata Anonymisation Toolkit: https://mat.boum.org/
* [Duc: Dude, where are my bytes!](http://duc.zevv.nl/), Duc is a collection of tools for indexing, inspecting and visualizing disk usage. Duc maintains a database of accumulated sizes * of directories of the file system, and allows you to query this database with some tools, or create fancy graphs showing you where your bytes are.
* Xfennec/progress: Linux tool to show progress for cp, mv, dd, … (formerly known as cv): https://github.com/Xfennec/progress
* [Shell script compiler (shc) | Neurobin](https://neurobin.org/projects/softwares/unix/shc/), compiling shell code into c source code
* solidsnack/arx: Bundles code and a job to run for local or remote execution. https://github.com/solidsnack/arx
* jbruchon/jdupes: A powerful duplicate file finder and an enhanced fork of ‘fdupes’. https://github.com/jbruchon/jdupes
* ios-control/ios-deploy: Install and debug iPhone apps from the command line, without using Xcode: https://github.com/ios-control/ios-deploy
* vi/websocat: Command-line client for WebSockets, like netcat (or curl) for ws:// with advanced socat-like functions: https://github.com/vi/websocat

# macOS

* iTerm2 - macOS Terminal Replacement: https://iterm2.com/
* [cliclick](https://www.bluem.net/jump/cliclick/) 自动化鼠标键盘操作工具
* pbcopy/pbpaste 在命令行复制粘贴
* mdfind 命令行的 Spotlight
* chflags 修改文件的属性，比如 chflags hidden /path/to/folder/ 可以在 Finder 中隐藏指定的文件，而无需是点文件
* say 文字转语音

# Windows

- Cygwin
- [Mintty — Cygwin Terminal emulator](https://mintty.github.io/)
- [PuTTY](https://note.cn.odd-e.com/Fg3Hag7eScioiQfFG7q_eA)
    - plink
    - pagent
    - psftp
    - [中文教程](https://chaifeng.com/blog/2007/06/putty_200611.html)
- [WinSCP](https://winscp.net/)

# 其他

* Org mode for Emacs – Your Life in Plain Text: http://orgmode.org/
* [Commandline Challenge](https://cmdchallenge.com/)
* Fn Project - The Container Native Serverless Framework: http://fnproject.io/
* [Træfik](https://traefik.io/), Træfik (pronounced like traffic) is a modern HTTP reverse proxy and load balancer made to deploy microservices with ease. It supports several backends (Docker, Swarm mode, Kubernetes, Marathon, Consul, Etcd, Rancher, Amazon ECS, and a lot more) to manage its configuration automatically and dynamically.
* [websocketd](http://websocketd.com/), Full duplex messaging between web browsers and servers
* [Oh, shit, git!](http://ohshitgit.com/)
* [hastebin](https://hastebin.com/)

# Development
* [SpotBugs](https://spotbugs.github.io/)
* [Flyway by Boxfuse • Database Migrations Made Easy](https://flywaydb.org/).