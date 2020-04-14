## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
***********************************
$ alias edit=<nano|vi|vim|subl>
subl
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```ShellSession
# Make configurations for working with github. Hub protocol: https
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```ShellSession
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global

[user]
        email = kulbitskij.na@phystech.edu
        name = kulbitsky99
[hub]
        protocol = https


$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status

./README.md

$ git add README.md
$ git commit -m"added README.md"
$ git push origin master

Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 649 bytes | 649.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To https://github.com/kulbitsky99/lab02.git
   669ef48..47125c5  master -> master

```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master

From https://github.com/kulbitsky99/lab02
 * branch            master     -> FETCH_HEAD
Already up to date.


$ git log

commit 47125c5ad5f178c3f0d1e9e1b33fde1dc26fa98c (HEAD -> master, origin/master)
Merge: 8633d0d 669ef48
Author: kulbitsky99 <kulbitskij.na@phystech.edu>
Date:   Fri Mar 13 22:39:34 2020 +0300

    Merge branch 'master' of https://github.com/kulbitsky99/lab02

commit 8633d0d3302b0bc3ec2144b5efa1e2daf6ea0bdc
Author: kulbitsky99 <kulbitskij.na@phystech.edu>
Date:   Fri Mar 13 22:38:35 2020 +0300

    created .gitignore

commit 669ef48733b628ba431147919c8d5ab5782daf89
Author: Kulbitski Mikita <36620760+kulbitsky99@users.noreply.github.com>
Date:   Fri Mar 13 22:26:25 2020 +0300

    create License

commit 8a9c411490b4455f4ba9cc54e95590c81fddc8b1
Author: kulbitsky99 <kulbitskij.na@phystech.edu>
Date:   Fri Mar 13 21:39:32 2020 +0300

    added README.md

```

```ShellSession
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```ShellSession
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
$ edit README.md
```

```ShellSession
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
