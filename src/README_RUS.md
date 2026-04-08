# DO1_Linux

## Part 1
![version](./misc/version.jpg)  

- *screenshot with currently installed Ubuntu server version*

## Part 2  

![adduser](./misc/adduser.jpg)  

- *adding user with `useradd` command*  

 ![passwd](./misc/etc_passwd_log.jpg)  

- *new user (student) in output of `cat /etc/passwd` 
(the last one)*

## Part 3

- to set the machine name as user-1 we'll go to `/etc/hostname` and rewrite it using `sudo` and our text editor **vim** 
- to set the time zone we will create a symlink from `/usr/share/zoneinfo/` to
`/etc/localtime/` using this command `sudo ln -sf /usr/share/zoneinfo/Asia/Yekaterinburg /etc/localtime/`
checking with `timedatectl`  
![timedatectl](./misc/time_and_date.jpg)
- outputing names of the network interfaces using `ip link` command, which shows 2 interfaces  
![ip_link](./misc/ip_link.jpg)
1. lo
 > **lo** (loopback) network interface is used by device to send data to itself for testing and local communication  
2. actual  router interface connected through Ethernet cable *(enp03s)*, which has *ipv6* address
- getting ip address from DHCP server using `sudo dhclient -v` with `-v`(verbose) flag to get more information. DHCP (Dynamic Host Configuration Protocol) is a network manager protocol which automatically assigns ip addresses to devices on a network. It's also responsible for masking our ip address  

![dhclient](./misc/dhclient.jpg)

- we can use `ip a` in a console to see all the ip addresses on all network interfaces and redirect its input into **grep** comand fot it to show all the internal ip adresses.  

![internal_ip](./misc/internal_ip.jpg)  

- to get external ip address of the gateway, which is the address of my router i'm curling the ifconfig with `curl ifconfig.me` command. also I'm adding an empty line to separate it from my hostname and username)  

![external_ip](./misc/external_ip.jpg)  

- setting static ip address and dns settings through changing the config in `/etc/netplan/"my network config.yaml"`.  

![open_ip_config](./misc/open_ip_config.jpg)  

 - using vim i'm setting my static gateway ip to `192.168.1.175/24`(/24 for masking first 3 numbers and leaving the last one for everyone else to see) and dns servers to `1.1.1.1` and `8.8.8.8`  
 ![netplan_config](./misc/netplan_config.jpg)  
 next, using `ip route show` command we can assure that we have changed our ip address to this in config file  
 ![changed_ip](./misc/changed_ip.jpg)  
 - pinging 1.1.1.1 and ya.ru to see if we are connected to network and do we have any packet loss (spoiler: we don't)  
 ![ping_dns](./misc/ping_dns.jpg)  
 ![ping_yandex](./misc/ping_yandex.jpg)  

## Part 4  
- Прописав в терминале комманды `sudo apt update` и `sudo apt upgrade` мы можем обновить системные пакеты до последней версии
- Прилагаю скриншот терминала, который говорит нам о том, что система обновлена и дальше обновлять нечего  

![sys_update](./misc/sys_update.jpg)

## Part 5

- Назначение команды `sudo` заключается в том, чтобы юзер мог выполнять определенные команды от лица суперюзера (или рута) или от лица любого друга юзера, если это необходимо. Устанавливать пакеты, добавлять/менять/удалять файлы в системных директориях, сидя не на рут аккаунте, можно в том числе c помощью sudo  

- Меняем название самой машины, открывая конфигурацию с правами суперюзера `sudo vim /etc/hostname`на `ubuntu server`  
![change_hostname](./misc/change_hostname.jpg)

## Part 6

- Вывод системной службы `timedatectl` и настроек этой службы `timedatectl show` показывают правильное время/часовой пояс и синхронизируют его через интернет `Ntpsynchronized=yes`  

![timedate](./misc/timedate.jpg)

## Part 7

- Я выбрал редакторы Vim, Nano и Ne. создал для каждого txt файл командами `<текстовый редактор> <текстовый редактор.txt>`и вписал в каждый файл свой ник
1. vim  
![vim](./misc/vim.jpg)  
чтобы выйти из vim с сохранением файла нужно сначала выйти в режим ввода комманд с помощью `Escape`и дальше ввести команду `:wq`. Вот так вот просто!) 
2. nano  
 ![nano](./misc/nano.jpg)  
чтобы выйти из нано достаточно нажать `CTRL + S` чтобы перезаписать файл и `CTRL + X`. Готово!  
3. ne  
![ne](./misc/ne.jpg)  
 чтобы выйти из Ne и сохранить файл жамкаем на клавиатуре `ALT + X`
 
- далее меняем во всех трех файлах содержимое на *21 School 21* и выходим без сохранения изменений    
4. vim  
![vim_2](./misc/vim_2.jpg)  
чтобы выйти без сохранения `Escape` и вводим `:q!` чтобы выйти без записи в файл  
5. nano  
![nano_2](./misc/nano_2.jpg)  
выходим через `CTRL + X`и далее отказываемся от записи в буфер нажимая клавишу `n`  
6. ne  
![ne_2](./misc/ne_2.jpg)  
тут достаточно будет нажать комбинацию `ALT + Q`  

- в этот раз в каждом файле нужно найти и заменить слово на любое другое. Я выбрал заменить свой никнейм bookagus на слово babaganush. Итак  
7. vim  
![vim_3](./misc/vim_3.jpg)  
чтобы найти и поменять слово в vim нам нужно выйти в режим ввода команд и ввести команду `:s/bookagus/babaganush`она найдет и заменит первое попавшееся в строке слово bookagus на babaganush. У команды `:s` есть много настроек и флагов. Например, с помощью знака `%` мы можем запросить замену одного слова на другое во всем  файле  
8. nano  
![nano_3](./misc/nano_3.jpg)  
в nano нам нужно нажать `CTRL + \`. редактор попросит нас ввести слово которое нужно заменить и на какое слово нужно его заменить. после этого можно пройтись по каждому совпадению в файле и решить, хотим мы его заменить или нет (или заменить сразу все совпадения в файле)  
9. ne   
![ne_3](./misc/ne_3.jpg)  
в ne нужно ввести на клавиатуре сочетание `CTRL + R`а дальше все как в нано, устал писать)
