# lab01
Отчёт по первой лабораторной работе.

 ## Report

В этом блоке происходит настройка переменных среды и выбор редактора
```bash
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GIST_TOKEN=<сохраненный_токен>
$ alias edit=<nano|vi|vim|subl>
```

Создается рабочая директория с именем пользователя с последующим созданием папки `/workspace` и переходом в нее.
Команда `$ pwd` выводит полный путь к данной директории.
Команда `$ cd ..` позволяет подняться по дереву на 1 директорию.
```sh
$ mkdir -p ${GITHUB_USERNAME}/workspace
$ cd ${GITHUB_USERNAME}/workspace
$ pwd
$ cd ..
$ pwd
```
Пример работы: 
`/root/barsik20/workspace`

Приведенные ниже команды позволяют создать директории `/tasks`, `/projects`, `/reports` в директории `workspace/`.
```sh
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
$ cd workspace
```



В данном блоке производится загрузка, распаковка и подготовка среды выполнения Node.js для локального использования без системной установки.
```sh
# Debian
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
$ tar -xf node-v6.11.5-linux-x64.tar.xz
$ rm -rf node-v6.11.5-linux-x64.tar.xz
$ mv node-v6.11.5-linux-x64 node
```



Выполняется добавление директории с исполняемыми файлами Node.js в переменную окружения. Выводим содержимое папки node/bin и значение переменной окружения PATH.
```sh
$ ls node/bin
$ echo ${PATH}
$ export PATH=${PATH}:`pwd`/node/bin
$ echo ${PATH}
```
Далее создаётся скрипт `scripts/activate` с помощью команды `cat > ... <<EOF`. В этот файл записывается строка, которая при выполнении будет снова добавлять тот же путь в `PATH`. Это полезно, чтобы каждый раз при открытии нового терминала не вводить export вручную.
```sh
$ mkdir scripts
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
$ source scripts/activate
```
Результат работы команды `$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF`:

```sh
export PATH=${PATH}:/home/ilya_ilyasov/Ilya/workspace/node/bin
```


Установка утилиты gist через Ruby
```sh
$ gem install gist
```
Результат работы команды:

```sh
Fetching gist-6.0.0.gem
Successfully installed gist-6.0.0
Parsing documentation for gist-6.0.0
Installing ri documentation for gist-6.0.0
Done installing documentation for gist after 0 seconds
1 gem installed

```

Токен доступа GitHub сохраняется в конфигурационный файл с ограниченными правами доступа.
```sh
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```


Производится клонирование репозитория с заданием, создание отчёта на основе шаблона, его редактирование и публикация в GitHub Gist.
```sh
$ export LAB_NUMBER=01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```
## Вывод
В ходе лабораторной работы была настроена рабочая среда, изучены основы работы с GitHub Gist и подготовлен отчёт лабораторной работы с последующей публикацией.

## Шаг 1
Команды: 
```sh
cd ~
wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz

```
Скачали библиотеку `boost` с помощью утилиты `wget`
<details>
<summary>Вывод команды</code></summary>
--2026-02-24 09:11:33--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
Resolving sourceforge.net (sourceforge.net)... 104.18.12.149, 104.18.13.149, 2606:4700::6812:d95, ...
Connecting to sourceforge.net (sourceforge.net)|104.18.12.149|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/ [following]
--2026-02-24 09:11:34--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download [following]
--2026-02-24 09:11:34--  https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz/download
Reusing existing connection to sourceforge.net:443.
HTTP request sent, awaiting response... 302 Found
Location: https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpnWtGj0GDm68t2LCTKGFuUHNSXX_uMDt2DV24SLb6owh09Y2raZ-dN8orRvOXSMMwGZ638QC203oegtIQt1HPW_0C2Q%3D%3D&use_mirror=altushost-swe&r= [following]
--2026-02-24 09:11:34--  https://downloads.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?ts=gAAAAABpnWtGj0GDm68t2LCTKGFuUHNSXX_uMDt2DV24SLb6owh09Y2raZ-dN8orRvOXSMMwGZ638QC203oegtIQt1HPW_0C2Q%3D%3D&use_mirror=altushost-swe&r=
Resolving downloads.sourceforge.net (downloads.sourceforge.net)... 104.18.12.149, 104.18.13.149, 2606:4700::6812:c95, ...
Connecting to downloads.sourceforge.net (downloads.sourceforge.net)|104.18.12.149|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://altushost-swe.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1 [following]
--2026-02-24 09:11:35--  https://altushost-swe.dl.sourceforge.net/project/boost/boost/1.69.0/boost_1_69_0.tar.gz?viasf=1
Resolving altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)... 79.142.76.130
Connecting to altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)|79.142.76.130|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 111710205 (107M) [application/x-gzip]
Saving to: ‘boost_1_69_0.tar.gz’

boost_1_69_0.tar.gz  100%[====================>] 106.53M  1.36MB/s    in 1m 42s  

2026-02-24 09:13:17 (1.05 MB/s) - ‘boost_1_69_0.tar.gz’ saved [111710205/111710205]
</details>

## Шаг 2
Разархивировал скаченный файл в директорию `~/boost_1_69_0`

Команды:
```sh
cd ~
tar -xzf boost_1_69_0.tar.gz
ls -ld ~/boost_1_69_0
```
<details>
  <summary>Вывод команды </summary>
  drwxrwxr-x 8 1000 1000 4096 Dec  5  2018 /root/boost_1_69_0
</details> 

## Шаг 3
Количество файлов только в корне библиотеки (без поддиректорий)

Команды:

```sh
find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l
```

<details>
  <summary>Вывод команды </summary>
12


</details>

## Шаг 4
Количество всех файлов, включая поддиректории

Команды:

```sh
find ~/boost_1_69_0 -type f | wc -l
```

<details>
  <summary>Вывод команды </summary>
  61191

</details>

## Шаг 5

Подсчёт заголовочных файлов, .cpp и остальных

Команды:

```sh
hpp_count=$(find ~/boost_1_69_0 -type f -name "*.hpp" | wc -l)
cpp_count=$(find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l)
total_files=$(find ~/boost_1_69_0 -type f | wc -l)
other_count=$((total_files - hpp_count - cpp_count))
echo "Заголовочных .hpp: $hpp_count"
echo "Файлов .cpp: $cpp_count"
echo "Остальных: $other_count"
```

<details>
  <summary>Вывод команды </summary>
  Заголовочных .hpp: 14912
Файлов .cpp: 13789
Остальных: 33450


</details>

## Шаг 6

Полный путь до файла any.hpp

Команды:

```sh
find ~/boost_1_69_0 -name "any.hpp" -type f
```

<details>
  <summary>Вывод команды </summary>
/home/ilya_ilyasov/boost_1_69_0/boost/proto/detail/any.hpp <br>
/home/ilya_ilyasov/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/hana/fwd/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/hana/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/type_erasure/any.hpp  <br>  
/home/ilya_ilyasov/boost_1_69_0/boost/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/xpressive/detail/utility/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/fusion/include/any.hpp   <br>
/home/ilya_ilyasov/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp  <br>  
/home/ilya_ilyasov/boost_1_69_0/boost/fusion/algorithm/query/any.hpp   <br>


</details>

## Шаг 7

 Найти все файлы, содержащие "boost::asio" (вывести имена)

Команды:

```sh
grep -rl "boost::asio" ~/boost_1_69_0

```

<details>
  <summary>Вывод команды </summary>
