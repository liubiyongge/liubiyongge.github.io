---
layout:     post
title:      "Write a Shell"
subtitle:   ""
date:       2019-11-15
author:     "LiuBiyongge"
header-img: "img/in-post/all.jpg"
tags:

  - c
---

# Write a Shell

[TOC]

## code

### main.cpp

```c++
#include <iostream>
#include <vector>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <cstring>
#include <fstream>
#include <sys/fcntl.h>
#include "builtinCommand.h"
#include "specialCommand.h"
using namespace std;



string PS1;




//shell框架
void mysh_loop();
string mysh_read_line();
vector<string> mysh_split_line(string line);
int lsh_launch(vector<string> args);
int mysh_execute(vector<string> args);



int main(int argc, char **argv) {
    mysh_loop();
    return 0;
}

void mysh_loop() {
    string line;
    vector<string> args;
    PipeRedirect pipe_redirect;
    int status = 0;

    while (!status){
        if(getenv("PS1")){
            PS1 = getenv("PS1");
        } else{
            PS1 = "$";
        }
        vector<string> cmd1, cmd2;
        cout << PS1;
        line = mysh_read_line();
        if(line == ""){
            continue;
        }
        args = mysh_split_line(line);

        pipe_redirect = check_pipe_redirect(args, cmd1, cmd2);
        if(pipe_redirect == PIPE){
            pipe_cmd(cmd1, cmd2);
        } else if(pipe_redirect == REDIRECT_IN || pipe_redirect == REDIRECT_OUT){
            redirect_cmd(cmd1, cmd2, pipe_redirect);
        } else if(pipe_redirect == BACKGROUG){
            backgroung_cmd(args);
        } else{
            status = mysh_execute(args);
        }

    }

}



string mysh_read_line() {
    string str;
    char ch;
    while ((ch = cin.get()) != '\n' && (ch != EOF)){
        str += ch;
    }

    if(str == "" && ch == EOF){
        exit(0);
    }
    return str;
}

//增加空格，某些非空字符也可以划分单词
//空格 \t为界线符号
vector<string> mysh_split_line(string line) {
    vector<string> strs;
    int startIndex = 0;
    bool flag = false;
    for(int i = 0; i < line.length(); i++){
        while (!flag){
            if(line[i] != ' ' && line[i] != '\t'){
                flag = true;
                startIndex = i;
            } else{
                i++;
                if(i >= line.length()){
                    break;
                }
            }
        }
        if(flag && (line[i] == ' ' || line[i] == '\t')){
            strs.push_back(line.substr(startIndex, i - startIndex));
            flag = false;
        }
    }
    if(flag){
        strs.push_back(line.substr(startIndex));
    }
    return strs;
}

int mysh_execute(vector<string> args) {

    int i;
    //bash内置命令
    for (i = 0; i < mysh_num_builtins(); i++) {
        if (args[0].c_str() == builtin[i]) {
            return (*builtin_func[i])(args);
        }
    }
    //创建新进程的命令
    return lsh_launch(args);

}

int lsh_launch(vector<string> args){
    pid_t pid, wpid;
    int status;
    pid = fork();
    if(pid == 0){
        //Child process
        const char *command = args[0].c_str();
        char ** strs = new char*[args.size() + 1];
        for(int i = 0; i < args.size(); i++) {
            strs[i] = &args[i][0];
        }
        strs[args.size()] = NULL;
        if(execvp(command, strs) == -1){
            if(errno == 2){
                cout << command << ":command not found" << endl;
            } else{
                cout << strerror(errno) << endl;
            }

        }
        delete []strs;
        exit(EXIT_FAILURE);
    } else if(pid < 0){
        cout << "can't create new process" << endl;
    } else{
        do {
            wpid = waitpid(pid, &status, WUNTRACED);
        } while (!WIFEXITED(status) && !WIFSIGNALED(status));
    }
    return 0;
}



```

### builtinCommand.h

```c++
//
// Created by liubiyongge on 2019/11/15.
//

#ifndef OSLAB2_BUILTINCOMMAND_H
#define OSLAB2_BUILTINCOMMAND_H

#include <iostream>
#include <vector>
#include <unistd.h>
using namespace std;


//内嵌命令
extern string builtin[];

int mysh_cd(vector<string> args);
int mysh_exit(vector<string> args);
int mysh_num_builtins();
extern int (*builtin_func[]) (vector<string> args);
#endif //OSLAB2_BUILTINCOMMAND_H

```

### builtinCommand.c

```c++
//
// Created by liubiyongge on 2019/11/15.
//


#include "builtinCommand.h"

string builtin[] = {"cd","exit"};
int (*builtin_func[]) (vector<string> args) = {&mysh_cd,&mysh_exit};

int mysh_cd(vector<string> args)
{
    if(args.size() > 2){
        cout << "too much argument" << endl;
    } else{
        if(chdir(args[1].c_str())!=0){
            cout << "No such file or direcoty" << endl;
        }
    }

    return 0;
}


int mysh_exit(vector<string> args)
{
    cout << "exit" << endl;
    return 1;
}

int mysh_num_builtins() {
    return sizeof(builtin) / sizeof(char *);
}
```

### specialCommand.h

```c++
//
// Created by liubiyongge on 2019/11/15.
//

#ifndef OSLAB2_SPECIALCOMMAND_H
#define OSLAB2_SPECIALCOMMAND_H

#include <iostream>
#include <vector>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <cstring>
#include <fstream>
#include <sys/fcntl.h>
using namespace std;

enum PipeRedirect {PIPE, REDIRECT_IN, REDIRECT_OUT, NEITHER, BACKGROUG};

// Pipes the first command's output into the second.
void pipe_cmd(vector<string> cmd1, vector<string> cmd2);
// Redirects the output from the given command into the given file.
void redirect_cmd(vector<string> cmd1, vector<string> cmd2, PipeRedirect num);
void backgroung_cmd(vector<string> args);
PipeRedirect check_pipe_redirect(vector<string> &args, vector<string> &cmd1, vector<string> &cmd2);

#endif //OSLAB2_SPECIALCOMMAND_H

```

### specialCommand.cpp

```c++
//
// Created by liubiyongge on 2019/11/15.
//

#include "specialCommand.h"


PipeRedirect check_pipe_redirect(vector<string> &args, vector<string> &cmd1, vector<string> &cmd2) {
    int i;
    PipeRedirect pipeRedirect = NEITHER;
    for(i = 0; i < args.size(); i++){
        if(args[i] == ">"){
            pipeRedirect = REDIRECT_OUT;
            break;
        } else if(args[i] == "<"){
            pipeRedirect = REDIRECT_IN;
            break;
        } else if(args[i] == "|"){
            pipeRedirect = PIPE;
            break;
        } else{
            cmd1.push_back(args[i]);
        }
    }
    for(i++; i < args.size(); i++){
        cmd2.push_back(args[i]);
    }
    if(args[args.size()-1] == "&"){
        pipeRedirect = BACKGROUG;
        args.pop_back();
    }
    return pipeRedirect;
}

void pipe_cmd(vector<string> cmd1, vector<string> cmd2){
    int pipefd[2];
    pid_t  p1, p2;//p2 -> p1
    int status = 0;
    if (pipe(pipefd) < 0) {
        printf("\nPipe could not be initialized");
        return;
    }
    p1 = fork();
    if(p1 < 0){
        printf("\nCould not fork");
        return;
    }

    if(p1 == 0){
        close(pipefd[0]);
        dup2(pipefd[1], STDOUT_FILENO);
        close(pipefd[1]);
        const char *command = cmd1[0].c_str();
        char ** strs = new char*[cmd1.size() + 1];
        for(int i = 0; i < cmd1.size(); i++) {
            strs[i] = &cmd1[i][0];
        }
        strs[cmd1.size()] = NULL;
        if(execvp(command, strs) == -1){
            if(errno == 2){
                cout << command << ":command not found" << endl;
            } else{
                cout << strerror(errno) << endl;
            }
            delete []strs;
            exit(0);
        }
        //cout << EOF;
        delete []strs;

    } else{
        waitpid(p1, &status, WUNTRACED);
        close(pipefd[1]);
        p2 = fork();
        if (p2 < 0) {
            printf("\nCould not fork");
            return;
        }

        if(p2 == 0){
            dup2(pipefd[0], STDIN_FILENO);
            close(pipefd[0]);
            const char *command = cmd2[0].c_str();
            char ** strs = new char*[cmd2.size() + 1];
            for(int i = 0; i < cmd2.size(); i++) {
                strs[i] = &cmd2[i][0];
            }
            strs[cmd2.size()] = NULL;
            //命令可以用标准输入作为参数
            if(execvp(command, strs) == -1){
                if(errno == 2){
                    cout << command << ":command not found" << endl;
                } else{
                    cout << strerror(errno) << endl;
                }
                delete []strs;
                exit(0);

            }
            delete []strs;
        } else{
            waitpid(p2, &status, WUNTRACED);
        }
    }
}


void redirect_cmd(vector<string> cmd1, vector<string> cmd2,PipeRedirect num){
    if(cmd2.size() != 1){
        cout << "error parameter" << endl;
        return;
    }
    pid_t pid, wpid;
    int status;
    pid = fork();
    if(pid == 0){
        //Child process
        int fd;
        int refd;
        if(num == REDIRECT_OUT){
            fd = open(cmd2[0].c_str(), O_WRONLY | O_CREAT, 0777);
        }else{
            fd = open(cmd2[0].c_str(),O_RDONLY);
        }

        if(fd==-1)
        {
            printf("open file error:%m\n");
            exit(-1);
        }
        if(num == REDIRECT_OUT){
            refd = dup2(fd, STDOUT_FILENO);
        }else{
            refd = dup2(fd, STDIN_FILENO);
        }

        if(refd== -1){
            printf("redirect standard out error:%m\n");
            exit(-1);
        }
        const char *command = cmd1[0].c_str();
        char ** strs = new char*[cmd1.size() + 1];
        for(int i = 0; i < cmd1.size(); i++) {
            strs[i] = &cmd1[i][0];
        }
        strs[cmd1.size()] = NULL;
        if(execvp(command, strs) == -1){
            if(errno == 2){
                cout << command << ":command not found" << endl;
            } else{
                cout << strerror(errno) << endl;
            }

        }
        delete []strs;
        close(fd);
        exit(EXIT_FAILURE);
    } else if(pid < 0){
        cout << "can't create new process" << endl;
    } else{
        do {
            wpid = waitpid(pid, &status, WUNTRACED);
        } while (!WIFEXITED(status) && !WIFSIGNALED(status));
    }


}

void backgroung_cmd(vector<string> args){
    pid_t pid, wpid;
    PipeRedirect pipeRedirect = NEITHER;
    int i;
    vector<string> cmd1, cmd2;
    for(i = 0; i < args.size() - 1; i++){
        if(args[i] == ">"){
            pipeRedirect = REDIRECT_OUT;
            break;
        } else if(args[i] == "<"){
            pipeRedirect = REDIRECT_IN;
            break;
        } else{
            cmd1.push_back(args[i]);
        }
    }
    for(i++; i < args.size(); i++){
        cmd2.push_back(args[i]);
    }

    int status;
    pid = fork();
    if(pid == 0){
        //Child process
        int fd;
        int refd;
        if(pipeRedirect == REDIRECT_OUT){
            fd = open(cmd2[0].c_str(), O_WRONLY | O_CREAT, 0777);
        }else{
            fd = open(cmd2[0].c_str(),O_RDONLY);
        }

        if(fd==-1)
        {
            printf("open file error:%m\n");
            exit(-1);
        }
        if(pipeRedirect == REDIRECT_OUT){
            refd = dup2(fd, STDOUT_FILENO);
        }else{
            refd = dup2(fd, STDIN_FILENO);
        }

        if(refd== -1){
            printf("redirect standard out error:%m\n");
            exit(-1);
        }
        const char *command = cmd1[0].c_str();
        char ** strs = new char*[cmd1.size() + 1];
        for(int i = 0; i < cmd1.size(); i++) {
            strs[i] = &cmd1[i][0];
        }
        strs[cmd1.size()] = NULL;
        if(execvp(command, strs) == -1){
            if(errno == 2){
                cout << command << ":command not found" << endl;
            } else{
                cout << strerror(errno) << endl;
            }

        }
        delete []strs;
        close(fd);
        exit(EXIT_FAILURE);
    } else if(pid < 0){
        cout << "can't create new process" << endl;
    } else{

    }
}
```

## 测试程序

```shell
#!/bin/bash

if [ -z $1 ] ; then 
    echo "Usage: $0 [myShell]" >&2
    exit 1
fi
myShell=$1

export PS1=""			# supress prompt

_uname=$(which uname)
_cat=$(which cat)
_passwd=$(which passwd)

rm -f testLog.txt


chkcmd () {
    echo "Testing $2"
    echo -e "$1" | bash > /tmp/t1
    echo -e "$1" | $myShell > /tmp/t2
    if diff /tmp/t1 /tmp/t2 ; then
	result=PASSED
    else
	result=FAILED
    fi
    echo -e "$result: $2" | tee -a testLog.txt
    echo "-----------------------------------------"
}

chkcmd "$_uname" "no parameter, full pathname"
chkcmd "$_uname \n $_uname" "two commands, full pathname"
chkcmd "$_uname \n\n $_uname" "two commands, blank line in-between, full pathname"
chkcmd "uname" "no parameter, no pathname"
chkcmd "$_cat $_passwd" "one parameter, full pathname"
chkcmd "cat $_passwd" "one parameter, no pathname"
chkcmd "ls -l | sort " "pipe"
chkcmd "cat $_passwd | sort | wc " "2 pipes"
chkcmd "cat < $_passwd" "redirect input"
chkcmd "uname > /tmp/x \n cat /tmp/x" "redirect output"
(echo "sleep 1" ; echo "echo 1") > /tmp/c1
chkcmd 'bash < /tmp/c1 &\n echo 2 \n sleep 3' "background"
chkcmd 'cd .. \n pwd' "change dir"

echo -e "\n\nResults"
cat testLog.txt

rm /tmp/c1 /tmp/t1 /tmp/t2
```



## 知识

- 输入

要使用`cin.get()`，因为\n也是有效输入，echo -e string, 默认会以EOF作为结尾

- fork()[^1]
- execvp[^2]

```c++
execvp(command, command , parameter, NULL);
strerror(errno);//execvp 报错会保存在errno中
```

- waitpid[^3]
- open[^4]
- dup2[^5]

```c++
int dup2(int oldfd, int newfd);
//newfd指向oldfd所指向的文件
```

> dup2(3, STDIN_FILENO);
>
> 让STDIN_FILENO，指向3文件描述符指向的文件，从3文件描述符指向的文件获取输入.

- pipe

```c++
int pipefd[2];
pipe(pipefd);//数据pipefd[1] -> pipe[0]
```

- close

> 关闭文件描述符

```
close(pipefd[0]);
dup2(pipefd[1], STDOUT_FILENO);
close(pipefd[1]);
STDOUT_FILENO指向了pipefd[1]指向的文件pipe管道的输入端
```

每个进程都有自己的一组文件描述符。

0 标准输入

1 标准输出

2 错误输出

[^1]:  http://cighao.com/2016/07/15/c-linux-fork/ 
[^2]:  https://linux.die.net/man/3/execvp
[^3]:  https://linux.die.net/man/2/waitpid
[^4]:   https://linux.die.net/man/2/open 
[^5]:  https://linux.die.net/man/2/dup2











