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
export PATH=${PATH}:/root/barsik20/workspace/node/bin
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
17


</details>

## Шаг 4
Количество всех файлов, включая поддиректории

Команды:

```sh
find ~/boost_1_69_0 -type f | wc -l
```

<details>
  <summary>Вывод команды </summary>
  62116

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
Файлов .cpp: 13786
Остальных: 33418


</details>

## Шаг 6

Полный путь до файла any.hpp

Команды:

```sh
find ~/boost_1_69_0 -name "any.hpp" -type f
```

<details>
  <summary>Вывод команды </summary>
/root/boost_1_69_0/boost/type_erasure/any.hpp <br>
/root/boost_1_69_0/boost/any.hpp <br>
/root/boost_1_69_0/boost/xpressive/detail/utility/any.hpp <br>
/root/boost_1_69_0/boost/hana/fwd/any.hpp<br>
/root/boost_1_69_0/boost/hana/any.hpp <br>
/root/boost_1_69_0/boost/proto/detail/any.hpp <br>
/root/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp <br>
/root/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp <br>
/root/boost_1_69_0/boost/fusion/algorithm/query/any.hpp <br>
/root/boost_1_69_0/boost/fusion/include/any.hpp 


</details>

## Шаг 7

 Найти все файлы, содержащие "boost::asio" (вывести имена)

Команды:

```sh
grep -rl "boost::asio" ~/boost_1_69_0

```

<details>
  <summary>Вывод команды </summary>
/root/boost_1_69_0/boost/asio/datagram_socket_service.hpp
/root/boost_1_69_0/boost/asio/signal_set_service.hpp
/root/boost_1_69_0/boost/asio/basic_socket_iostream.hpp
/root/boost_1_69_0/boost/asio/use_future.hpp
/root/boost_1_69_0/boost/asio/is_executor.hpp
/root/boost_1_69_0/boost/asio/coroutine.hpp
/root/boost_1_69_0/boost/asio/ip/basic_resolver_results.hpp
/root/boost_1_69_0/boost/asio/ip/udp.hpp
/root/boost_1_69_0/boost/asio/ip/unicast.hpp
/root/boost_1_69_0/boost/asio/ip/v6_only.hpp
/root/boost_1_69_0/boost/asio/ip/basic_endpoint.hpp
/root/boost_1_69_0/boost/asio/ip/address.hpp
/root/boost_1_69_0/boost/asio/ip/network_v4.hpp
/root/boost_1_69_0/boost/asio/ip/resolver_service.hpp
/root/boost_1_69_0/boost/asio/ip/detail/socket_option.hpp
/root/boost_1_69_0/boost/asio/ip/detail/endpoint.hpp
/root/boost_1_69_0/boost/asio/ip/detail/impl/endpoint.ipp
/root/boost_1_69_0/boost/asio/ip/basic_resolver.hpp
/root/boost_1_69_0/boost/asio/ip/address_v4.hpp
/root/boost_1_69_0/boost/asio/ip/tcp.hpp
/root/boost_1_69_0/boost/asio/ip/impl/host_name.ipp
/root/boost_1_69_0/boost/asio/ip/impl/address_v4.ipp
/root/boost_1_69_0/boost/asio/ip/impl/address.ipp
/root/boost_1_69_0/boost/asio/ip/impl/basic_endpoint.hpp
/root/boost_1_69_0/boost/asio/ip/impl/address.hpp
/root/boost_1_69_0/boost/asio/ip/impl/network_v4.hpp
/root/boost_1_69_0/boost/asio/ip/impl/address_v4.hpp
/root/boost_1_69_0/boost/asio/ip/impl/network_v6.hpp
/root/boost_1_69_0/boost/asio/ip/impl/address_v6.hpp
/root/boost_1_69_0/boost/asio/ip/impl/network_v4.ipp
/root/boost_1_69_0/boost/asio/ip/impl/network_v6.ipp
/root/boost_1_69_0/boost/asio/ip/impl/address_v6.ipp
/root/boost_1_69_0/boost/asio/ip/network_v6.hpp
/root/boost_1_69_0/boost/asio/ip/basic_resolver_query.hpp
/root/boost_1_69_0/boost/asio/ip/icmp.hpp
/root/boost_1_69_0/boost/asio/ip/address_v6.hpp
/root/boost_1_69_0/boost/asio/ip/basic_resolver_iterator.hpp
/root/boost_1_69_0/boost/asio/ip/basic_resolver_entry.hpp
/root/boost_1_69_0/boost/asio/ip/multicast.hpp
/root/boost_1_69_0/boost/asio/buffered_read_stream.hpp
/root/boost_1_69_0/boost/asio/basic_seq_packet_socket.hpp
/root/boost_1_69_0/boost/asio/basic_raw_socket.hpp
/root/boost_1_69_0/boost/asio/deadline_timer_service.hpp
/root/boost_1_69_0/boost/asio/buffered_write_stream.hpp
/root/boost_1_69_0/boost/asio/local/basic_endpoint.hpp
/root/boost_1_69_0/boost/asio/local/detail/endpoint.hpp
/root/boost_1_69_0/boost/asio/local/detail/impl/endpoint.ipp
/root/boost_1_69_0/boost/asio/local/datagram_protocol.hpp
/root/boost_1_69_0/boost/asio/local/connect_pair.hpp
/root/boost_1_69_0/boost/asio/local/stream_protocol.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_serial_port_service.hpp
/root/boost_1_69_0/boost/asio/detail/handler_alloc_helpers.hpp
/root/boost_1_69_0/boost/asio/detail/conditionally_enabled_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/socket_option.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_accept_op.hpp
/root/boost_1_69_0/boost/asio/detail/noncopyable.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_connect_op.hpp
/root/boost_1_69_0/boost/asio/detail/signal_set_service.hpp
/root/boost_1_69_0/boost/asio/detail/handler_cont_helpers.hpp
/root/boost_1_69_0/boost/asio/detail/std_static_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/kqueue_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/null_static_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/resolve_endpoint_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_connect_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_io_context.hpp
/root/boost_1_69_0/boost/asio/detail/thread_group.hpp
/root/boost_1_69_0/boost/asio/detail/handler_type_requirements.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_resolve_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_wait_op.hpp
/root/boost_1_69_0/boost/asio/detail/dev_poll_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/conditionally_enabled_event.hpp
/root/boost_1_69_0/boost/asio/detail/std_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_handle_service.hpp
/root/boost_1_69_0/boost/asio/detail/descriptor_ops.hpp
/root/boost_1_69_0/boost/asio/detail/null_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/deadline_timer_service.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_descriptor_service.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_overlapped_ptr.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_sendto_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_serial_port_service.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_recvfrom_op.hpp
/root/boost_1_69_0/boost/asio/detail/descriptor_read_op.hpp
/root/boost_1_69_0/boost/asio/detail/epoll_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/resolver_service.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_recvmsg_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_recvmsg_op.hpp
/root/boost_1_69_0/boost/asio/detail/null_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_ssocket_service.hpp
/root/boost_1_69_0/boost/asio/detail/strand_service.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_accept_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_handle_write_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_handle_read_op.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_socket_recv_op.hpp
/root/boost_1_69_0/boost/asio/detail/winsock_init.hpp
/root/boost_1_69_0/boost/asio/detail/descriptor_write_op.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_resolver_service.hpp
/root/boost_1_69_0/boost/asio/detail/scheduler.hpp
/root/boost_1_69_0/boost/asio/detail/resolver_service_base.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_null_buffers_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_recv_op.hpp
/root/boost_1_69_0/boost/asio/detail/null_socket_service.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_recv_op.hpp
/root/boost_1_69_0/boost/asio/detail/impl/winrt_timer_scheduler.ipp
/root/boost_1_69_0/boost/asio/detail/impl/service_registry.ipp
/root/boost_1_69_0/boost/asio/detail/impl/dev_poll_reactor.ipp
/root/boost_1_69_0/boost/asio/detail/impl/epoll_reactor.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_iocp_io_context.hpp
/root/boost_1_69_0/boost/asio/detail/impl/socket_select_interrupter.ipp
/root/boost_1_69_0/boost/asio/detail/impl/dev_poll_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/impl/posix_event.ipp
/root/boost_1_69_0/boost/asio/detail/impl/winrt_ssocket_service_base.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_mutex.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_iocp_serial_port_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/reactive_serial_port_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_static_mutex.ipp
/root/boost_1_69_0/boost/asio/detail/impl/eventfd_select_interrupter.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_thread.ipp
/root/boost_1_69_0/boost/asio/detail/impl/buffer_sequence_adapter.ipp
/root/boost_1_69_0/boost/asio/detail/impl/scheduler.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_object_handle_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_iocp_io_context.ipp
/root/boost_1_69_0/boost/asio/detail/impl/handler_tracking.ipp
/root/boost_1_69_0/boost/asio/detail/impl/strand_service.hpp
/root/boost_1_69_0/boost/asio/detail/impl/resolver_service_base.ipp
/root/boost_1_69_0/boost/asio/detail/impl/kqueue_reactor.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_tss_ptr.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_iocp_socket_service_base.ipp
/root/boost_1_69_0/boost/asio/detail/impl/signal_set_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/select_reactor.ipp
/root/boost_1_69_0/boost/asio/detail/impl/winrt_timer_scheduler.hpp
/root/boost_1_69_0/boost/asio/detail/impl/strand_executor_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/descriptor_ops.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_iocp_handle_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/posix_tss_ptr.ipp
/root/boost_1_69_0/boost/asio/detail/impl/throw_error.ipp
/root/boost_1_69_0/boost/asio/detail/impl/socket_ops.ipp
/root/boost_1_69_0/boost/asio/detail/impl/select_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/impl/posix_thread.ipp
/root/boost_1_69_0/boost/asio/detail/impl/winsock_init.ipp
/root/boost_1_69_0/boost/asio/detail/impl/pipe_select_interrupter.ipp
/root/boost_1_69_0/boost/asio/detail/impl/posix_mutex.ipp
/root/boost_1_69_0/boost/asio/detail/impl/reactive_descriptor_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/win_event.ipp
/root/boost_1_69_0/boost/asio/detail/impl/strand_service.ipp
/root/boost_1_69_0/boost/asio/detail/impl/reactive_socket_service_base.ipp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_service.hpp
/root/boost_1_69_0/boost/asio/detail/posix_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_timer_scheduler.hpp
/root/boost_1_69_0/boost/asio/detail/win_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_send_op.hpp
/root/boost_1_69_0/boost/asio/detail/string_view.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_overlapped_op.hpp
/root/boost_1_69_0/boost/asio/detail/completion_handler.hpp
/root/boost_1_69_0/boost/asio/detail/buffer_sequence_adapter.hpp
/root/boost_1_69_0/boost/asio/detail/select_reactor.hpp
/root/boost_1_69_0/boost/asio/detail/handler_invoke_helpers.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_send_op.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_socket_send_op.hpp
/root/boost_1_69_0/boost/asio/detail/is_buffer_sequence.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_async_manager.hpp
/root/boost_1_69_0/boost/asio/detail/buffered_stream_storage.hpp
/root/boost_1_69_0/boost/asio/detail/signal_handler.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_service.hpp
/root/boost_1_69_0/boost/asio/detail/win_object_handle_service.hpp
/root/boost_1_69_0/boost/asio/detail/timer_queue.hpp
/root/boost_1_69_0/boost/asio/detail/posix_static_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_socket_service_base.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_recvfrom_op.hpp
/root/boost_1_69_0/boost/asio/detail/reactive_wait_op.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_ssocket_service_base.hpp
/root/boost_1_69_0/boost/asio/detail/wince_thread.hpp
/root/boost_1_69_0/boost/asio/detail/winapp_thread.hpp
/root/boost_1_69_0/boost/asio/detail/reactor_op_queue.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_utils.hpp
/root/boost_1_69_0/boost/asio/detail/service_registry.hpp
/root/boost_1_69_0/boost/asio/detail/consuming_buffers.hpp
/root/boost_1_69_0/boost/asio/detail/null_thread.hpp
/root/boost_1_69_0/boost/asio/detail/winrt_socket_connect_op.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_null_buffers_op.hpp
/root/boost_1_69_0/boost/asio/detail/wait_handler.hpp
/root/boost_1_69_0/boost/asio/detail/win_static_mutex.hpp
/root/boost_1_69_0/boost/asio/detail/handler_tracking.hpp
/root/boost_1_69_0/boost/asio/detail/win_iocp_socket_service_base.hpp
/root/boost_1_69_0/boost/asio/detail/resolve_query_op.hpp
/root/boost_1_69_0/boost/asio/executor.hpp
/root/boost_1_69_0/boost/asio/windows/random_access_handle.hpp
/root/boost_1_69_0/boost/asio/windows/object_handle.hpp
/root/boost_1_69_0/boost/asio/windows/basic_random_access_handle.hpp
/root/boost_1_69_0/boost/asio/windows/basic_object_handle.hpp
/root/boost_1_69_0/boost/asio/windows/stream_handle.hpp
/root/boost_1_69_0/boost/asio/windows/basic_stream_handle.hpp
/root/boost_1_69_0/boost/asio/windows/overlapped_ptr.hpp
/root/boost_1_69_0/boost/asio/windows/overlapped_handle.hpp
/root/boost_1_69_0/boost/asio/windows/random_access_handle_service.hpp
/root/boost_1_69_0/boost/asio/windows/stream_handle_service.hpp
/root/boost_1_69_0/boost/asio/windows/basic_handle.hpp
/root/boost_1_69_0/boost/asio/windows/object_handle_service.hpp
/root/boost_1_69_0/boost/asio/completion_condition.hpp
/root/boost_1_69_0/boost/asio/buffered_stream.hpp
/root/boost_1_69_0/boost/asio/serial_port_service.hpp
/root/boost_1_69_0/boost/asio/seq_packet_socket_service.hpp
/root/boost_1_69_0/boost/asio/basic_datagram_socket.hpp
/root/boost_1_69_0/boost/asio/spawn.hpp
/root/boost_1_69_0/boost/asio/socket_base.hpp
/root/boost_1_69_0/boost/asio/ts/netfwd.hpp
/root/boost_1_69_0/boost/asio/execution_context.hpp
/root/boost_1_69_0/boost/asio/basic_stream_socket.hpp
/root/boost_1_69_0/boost/asio/impl/execution_context.ipp
/root/boost_1_69_0/boost/asio/impl/buffered_read_stream.hpp
/root/boost_1_69_0/boost/asio/impl/buffered_write_stream.hpp
/root/boost_1_69_0/boost/asio/impl/spawn.hpp
/root/boost_1_69_0/boost/asio/impl/io_context.ipp
/root/boost_1_69_0/boost/asio/impl/serial_port_base.ipp
/root/boost_1_69_0/boost/asio/impl/read.hpp
/root/boost_1_69_0/boost/asio/impl/write.hpp
/root/boost_1_69_0/boost/asio/impl/read_at.hpp
/root/boost_1_69_0/boost/asio/impl/connect.hpp
/root/boost_1_69_0/boost/asio/impl/read_until.hpp
/root/boost_1_69_0/boost/asio/impl/io_context.hpp
/root/boost_1_69_0/boost/asio/impl/write_at.hpp
/root/boost_1_69_0/boost/asio/buffers_iterator.hpp
/root/boost_1_69_0/boost/asio/socket_acceptor_service.hpp
/root/boost_1_69_0/boost/asio/basic_streambuf.hpp
/root/boost_1_69_0/boost/asio/generic/seq_packet_protocol.hpp
/root/boost_1_69_0/boost/asio/generic/basic_endpoint.hpp
/root/boost_1_69_0/boost/asio/generic/detail/endpoint.hpp
/root/boost_1_69_0/boost/asio/generic/detail/impl/endpoint.ipp
/root/boost_1_69_0/boost/asio/generic/datagram_protocol.hpp
/root/boost_1_69_0/boost/asio/generic/raw_protocol.hpp
/root/boost_1_69_0/boost/asio/generic/stream_protocol.hpp
/root/boost_1_69_0/boost/asio/io_context_strand.hpp
/root/boost_1_69_0/boost/asio/read.hpp
/root/boost_1_69_0/boost/asio/ssl/stream_base.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/write_op.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/io.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/read_op.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/buffered_handshake_op.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/openssl_init.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/engine.hpp
/root/boost_1_69_0/boost/asio/ssl/detail/impl/openssl_init.ipp
/root/boost_1_69_0/boost/asio/ssl/detail/impl/engine.ipp
/root/boost_1_69_0/boost/asio/ssl/detail/stream_core.hpp
/root/boost_1_69_0/boost/asio/ssl/context.hpp
/root/boost_1_69_0/boost/asio/ssl/rfc2818_verification.hpp
/root/boost_1_69_0/boost/asio/ssl/impl/error.ipp
/root/boost_1_69_0/boost/asio/ssl/impl/context.hpp
/root/boost_1_69_0/boost/asio/ssl/impl/context.ipp
/root/boost_1_69_0/boost/asio/ssl/context_base.hpp
/root/boost_1_69_0/boost/asio/ssl/error.hpp
/root/boost_1_69_0/boost/asio/ssl/stream.hpp
/root/boost_1_69_0/boost/asio/placeholders.hpp
/root/boost_1_69_0/boost/asio/handler_invoke_hook.hpp
/root/boost_1_69_0/boost/asio/raw_socket_service.hpp
/root/boost_1_69_0/boost/asio/basic_signal_set.hpp
/root/boost_1_69_0/boost/asio/stream_socket_service.hpp
/root/boost_1_69_0/boost/asio/uses_executor.hpp
/root/boost_1_69_0/boost/asio/write.hpp
/root/boost_1_69_0/boost/asio/read_at.hpp
/root/boost_1_69_0/boost/asio/basic_serial_port.hpp
/root/boost_1_69_0/boost/asio/basic_socket_streambuf.hpp
/root/boost_1_69_0/boost/asio/connect.hpp
/root/boost_1_69_0/boost/asio/basic_socket_acceptor.hpp
/root/boost_1_69_0/boost/asio/experimental/detached.hpp
/root/boost_1_69_0/boost/asio/experimental/impl/detached.hpp
/root/boost_1_69_0/boost/asio/experimental/impl/co_spawn.hpp
/root/boost_1_69_0/boost/asio/basic_socket.hpp
/root/boost_1_69_0/boost/asio/serial_port.hpp
/root/boost_1_69_0/boost/asio/posix/basic_descriptor.hpp
/root/boost_1_69_0/boost/asio/posix/descriptor.hpp
/root/boost_1_69_0/boost/asio/posix/descriptor_base.hpp
/root/boost_1_69_0/boost/asio/posix/basic_stream_descriptor.hpp
/root/boost_1_69_0/boost/asio/posix/stream_descriptor.hpp
/root/boost_1_69_0/boost/asio/posix/stream_descriptor_service.hpp
/root/boost_1_69_0/boost/asio/async_result.hpp
/root/boost_1_69_0/boost/asio/basic_waitable_timer.hpp
/root/boost_1_69_0/boost/asio/basic_deadline_timer.hpp
/root/boost_1_69_0/boost/asio/waitable_timer_service.hpp
/root/boost_1_69_0/boost/asio/signal_set.hpp
/root/boost_1_69_0/boost/asio/buffer.hpp
/root/boost_1_69_0/boost/asio/read_until.hpp
/root/boost_1_69_0/boost/asio/error.hpp
/root/boost_1_69_0/boost/asio/io_context.hpp
/root/boost_1_69_0/boost/asio/basic_io_object.hpp
/root/boost_1_69_0/boost/asio/thread_pool.hpp
/root/boost_1_69_0/boost/asio/write_at.hpp
/root/boost_1_69_0/boost/process/io.hpp
/root/boost_1_69_0/boost/process/async.hpp
/root/boost_1_69_0/boost/process/async_system.hpp
/root/boost_1_69_0/boost/process/system.hpp
/root/boost_1_69_0/boost/process/detail/traits/async.hpp
/root/boost_1_69_0/boost/process/detail/windows/io_context_ref.hpp
/root/boost_1_69_0/boost/process/detail/windows/async_out.hpp
/root/boost_1_69_0/boost/process/detail/windows/async_in.hpp
/root/boost_1_69_0/boost/process/detail/windows/async_pipe.hpp
/root/boost_1_69_0/boost/process/detail/async_handler.hpp
/root/boost_1_69_0/boost/process/detail/posix/io_context_ref.hpp
/root/boost_1_69_0/boost/process/detail/posix/async_out.hpp
/root/boost_1_69_0/boost/process/detail/posix/async_in.hpp
/root/boost_1_69_0/boost/process/detail/posix/async_pipe.hpp
/root/boost_1_69_0/boost/process/detail/posix/sigchld_service.hpp
/root/boost_1_69_0/boost/process/spawn.hpp
/root/boost_1_69_0/boost/process/async_pipe.hpp
/root/boost_1_69_0/boost/beast/websocket/teardown.hpp
/root/boost_1_69_0/boost/beast/websocket/detail/frame.hpp
/root/boost_1_69_0/boost/beast/websocket/detail/stream_base.hpp
/root/boost_1_69_0/boost/beast/websocket/detail/mask.hpp
/root/boost_1_69_0/boost/beast/websocket/detail/utf8_checker.hpp
/root/boost_1_69_0/boost/beast/websocket/detail/pausation.hpp
/root/boost_1_69_0/boost/beast/websocket/ssl.hpp
/root/boost_1_69_0/boost/beast/websocket/role.hpp
/root/boost_1_69_0/boost/beast/websocket/rfc6455.hpp
/root/boost_1_69_0/boost/beast/websocket/impl/handshake.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/write.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/ping.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/accept.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/ssl.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/stream.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/teardown.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/close.ipp
/root/boost_1_69_0/boost/beast/websocket/impl/read.ipp
/root/boost_1_69_0/boost/beast/websocket/stream.hpp
/root/boost_1_69_0/boost/beast/http/buffer_body.hpp
/root/boost_1_69_0/boost/beast/http/basic_parser.hpp
/root/boost_1_69_0/boost/beast/http/fields.hpp
/root/boost_1_69_0/boost/beast/http/empty_body.hpp
/root/boost_1_69_0/boost/beast/http/detail/chunk_encode.hpp
/root/boost_1_69_0/boost/beast/http/impl/write.ipp
/root/boost_1_69_0/boost/beast/http/impl/fields.ipp
/root/boost_1_69_0/boost/beast/http/impl/file_body_win32.ipp
/root/boost_1_69_0/boost/beast/http/impl/basic_parser.ipp
/root/boost_1_69_0/boost/beast/http/impl/serializer.ipp
/root/boost_1_69_0/boost/beast/http/impl/read.ipp
/root/boost_1_69_0/boost/beast/http/impl/chunk_encode.ipp
/root/boost_1_69_0/boost/beast/http/chunk_encode.hpp
/root/boost_1_69_0/boost/beast/http/read.hpp
/root/boost_1_69_0/boost/beast/http/parser.hpp
/root/boost_1_69_0/boost/beast/http/serializer.hpp
/root/boost_1_69_0/boost/beast/http/string_body.hpp
/root/boost_1_69_0/boost/beast/http/write.hpp
/root/boost_1_69_0/boost/beast/http/type_traits.hpp
/root/boost_1_69_0/boost/beast/http/basic_dynamic_body.hpp
/root/boost_1_69_0/boost/beast/http/error.hpp
/root/boost_1_69_0/boost/beast/http/span_body.hpp
/root/boost_1_69_0/boost/beast/http/basic_file_body.hpp
/root/boost_1_69_0/boost/beast/http/vector_body.hpp
/root/boost_1_69_0/boost/beast/experimental/http/impl/icy_stream.ipp
/root/boost_1_69_0/boost/beast/experimental/http/icy_stream.hpp
/root/boost_1_69_0/boost/beast/experimental/test/impl/stream.ipp
/root/boost_1_69_0/boost/beast/experimental/test/stream.hpp
/root/boost_1_69_0/boost/beast/experimental/core/timeout_socket.hpp
/root/boost_1_69_0/boost/beast/experimental/core/flat_stream.hpp
/root/boost_1_69_0/boost/beast/experimental/core/detail/flat_stream.hpp
/root/boost_1_69_0/boost/beast/experimental/core/detail/service_base.hpp
/root/boost_1_69_0/boost/beast/experimental/core/detail/timeout_service.hpp
/root/boost_1_69_0/boost/beast/experimental/core/detail/impl/timeout_service.ipp
/root/boost_1_69_0/boost/beast/experimental/core/timeout_service.hpp
/root/boost_1_69_0/boost/beast/experimental/core/impl/timeout_socket.hpp
/root/boost_1_69_0/boost/beast/experimental/core/impl/timeout_service.ipp
/root/boost_1_69_0/boost/beast/experimental/core/impl/flat_stream.ipp
/root/boost_1_69_0/boost/beast/experimental/core/ssl_stream.hpp
/root/boost_1_69_0/boost/beast/core/buffers_cat.hpp
/root/boost_1_69_0/boost/beast/core/buffers_suffix.hpp
/root/boost_1_69_0/boost/beast/core/flat_static_buffer.hpp
/root/boost_1_69_0/boost/beast/core/buffered_read_stream.hpp
/root/boost_1_69_0/boost/beast/core/detail/buffers_ref.hpp
/root/boost_1_69_0/boost/beast/core/detail/bind_handler.hpp
/root/boost_1_69_0/boost/beast/core/detail/type_traits.hpp
/root/boost_1_69_0/boost/beast/core/flat_buffer.hpp
/root/boost_1_69_0/boost/beast/core/ostream.hpp
/root/boost_1_69_0/boost/beast/core/impl/flat_buffer.ipp
/root/boost_1_69_0/boost/beast/core/impl/buffers_suffix.ipp
/root/boost_1_69_0/boost/beast/core/impl/read_size.ipp
/root/boost_1_69_0/boost/beast/core/impl/buffers_cat.ipp
/root/boost_1_69_0/boost/beast/core/impl/buffers_adapter.ipp
/root/boost_1_69_0/boost/beast/core/impl/multi_buffer.ipp
/root/boost_1_69_0/boost/beast/core/impl/handler_ptr.ipp
/root/boost_1_69_0/boost/beast/core/impl/buffered_read_stream.ipp
/root/boost_1_69_0/boost/beast/core/impl/flat_static_buffer.ipp
/root/boost_1_69_0/boost/beast/core/impl/buffers_prefix.ipp
/root/boost_1_69_0/boost/beast/core/impl/static_buffer.ipp
/root/boost_1_69_0/boost/beast/core/multi_buffer.hpp
/root/boost_1_69_0/boost/beast/core/buffers_adapter.hpp
/root/boost_1_69_0/boost/beast/core/buffers_to_string.hpp
/root/boost_1_69_0/boost/beast/core/bind_handler.hpp
/root/boost_1_69_0/boost/beast/core/type_traits.hpp
/root/boost_1_69_0/boost/beast/core/buffers_prefix.hpp
/root/boost_1_69_0/boost/beast/core/static_buffer.hpp
/root/boost_1_69_0/boost/log/sinks/syslog_backend.hpp
/root/boost_1_69_0/doc/html/boost/process/async_pipe.html
/root/boost_1_69_0/doc/html/boost/process/std_in.html
/root/boost_1_69_0/doc/html/boost/process/spawn.html
/root/boost_1_69_0/doc/html/boost/process/std_out.html
/root/boost_1_69_0/doc/html/boost/process/on_exit.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__addrinfo_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_after.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_iostream/expires_from_now/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/basic_waitable_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel_one/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/cancel_one/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_after.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_from_now/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer/expires_from_now/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/error__netdb_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_waitable_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/HandshakeHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver_query/hints.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload7.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload11.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload10.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload12.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload8.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload9.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/basic_socket_acceptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/accept.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/listen/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/async_accept/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_send.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/shutdown/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/shutdown/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/remote_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/remote_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/basic_seq_packet_socket.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/async_connect.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_seq_packet_socket/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_completion/completion_handler_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer_sequence_end.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__enable_loopback.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_after.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_streambuf/expires_from_now/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/placeholders__iterator.html
/root/boost_1_69_0/doc/html/boost_asio/reference/error__ssl_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__basic_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__rfc2818_verification.html
/root/boost_1_69_0/doc/html/boost_asio/reference/use_future_t.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__leave_group.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer_copy.html
/root/boost_1_69_0/doc/html/boost_asio/reference/MutableBufferSequence.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context/make_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context/add_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/yield_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/WaitHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/generic__stream_protocol.html
/root/boost_1_69_0/doc/html/boost_asio/reference/MoveAcceptHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/work.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/work/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__work/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__ssl_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/write_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/read_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_write_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/release.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/stream_descriptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__stream_descriptor/async_read_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/signal_set.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__error__stream_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/thread_pool.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ConstBufferSequence.html
/root/boost_1_69_0/doc/html/boost_asio/reference/placeholders__endpoint.html
/root/boost_1_69_0/doc/html/boost_asio/reference/RangeConnectHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_write_stream/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_write_stream/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/experimental__detached_t.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload7.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload11.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload10.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload12.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload8.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload9.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/connect/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__netdb_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/descriptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/release.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/posix__descriptor_base/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ResolveHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__join_group.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/operator_eq_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/to_v4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__address/to_v6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__unicast__hops.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/async_write_some_at.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/random_access_handle.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/read_some_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/write_some_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/async_read_some_at.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__random_access_handle/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__boost__asio__ssl__error__stream_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload7.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload8.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/steady_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send_to/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send_to/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_to/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/shutdown/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/shutdown/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive_from/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/remote_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/remote_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive_from/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_receive_from/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/async_connect.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_datagram_socket/basic_datagram_socket.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ConnectHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/thread_pool/make_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/thread_pool/add_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer_cast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/IteratorConnectHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/signal_set.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_connect/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/null_buffers/value_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/error__misc_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/SignalHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/strand.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket_acceptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf.html
/root/boost_1_69_0/doc/html/boost_asio/reference/BufferedHandshakeHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/add_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_write_at/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_at/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/system_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_stream/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_stream/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/dynamic_vector_buffer/mutable_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/dynamic_vector_buffer/const_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__tcp/acceptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__tcp/no_delay.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__v6_only.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/basic_resolver.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/cancel.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/basic_resolver/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/async_resolve/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_resolver/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ShutdownHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/execution_context/make_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/execution_context/add_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/transfer_at_least.html
/root/boost_1_69_0/doc/html/boost_asio/reference/deadline_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/transfer_all.html
/root/boost_1_69_0/doc/html/boost_asio/reference/spawn.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/native_handle.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ssl__stream/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/socket_base/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/local__stream_protocol/acceptor.html
/root/boost_1_69_0/doc/html/boost_asio/reference/placeholders__bytes_transferred.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__strand.html
/root/boost_1_69_0/doc/html/boost_asio/reference/generic__raw_protocol.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/generic__datagram_protocol.html
/root/boost_1_69_0/doc/html/boost_asio/reference/const_buffer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__misc_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf_ref/mutable_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_streambuf_ref/const_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/Handler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__hops.html
/root/boost_1_69_0/doc/html/boost_asio/reference/error__system_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffer_sequence_begin.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write_at/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/dynamic_string_buffer/mutable_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/dynamic_string_buffer/const_buffers_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/streambuf.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/write_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/read_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/shutdown/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/shutdown/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/basic_stream_socket/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/remote_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/remote_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_write_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_send/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_connect.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/async_read_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_stream_socket/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/write_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/read_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/serial_port/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/async_write_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/serial_port/async_read_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/mutable_buffer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/executor_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/basic_io_object/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/basic_io_object.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_io_object/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/shutdown/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/shutdown/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/basic_socket/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/remote_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/remote_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/async_connect.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_socket/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/high_resolution_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_handle/overlapped_handle/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__basic_endpoint/basic_endpoint/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/system_context/make_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/system_context/add_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/spawn/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload7.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload13.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload11.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload10.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload14.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload15.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload12.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload9.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until/overload16.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_at/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_at/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel_one/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/cancel_one/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/basic_deadline_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_from_now/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer/expires_from_now/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ReadHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/set_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/set_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/do_not_route.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bind/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bind/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/keep_alive.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send_to/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send_to/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_to/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/reuse_address.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/connect/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/connect/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/bytes_readable.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/wait/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/wait/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/native_non_blocking/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/linger.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/io_control/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/io_control/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/enable_connection_aborted.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/shutdown/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/shutdown/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/debug.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_buffer_size.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive_from/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/receive/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/broadcast.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/remote_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/remote_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_send/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/basic_raw_socket/overload4.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/send_low_watermark.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/local_endpoint/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/local_endpoint/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/release/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/release/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/open/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/open/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive_from/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_receive_from/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_option/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/get_option/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/async_connect.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_raw_socket/out_of_band_inline.html
/root/boost_1_69_0/doc/html/boost_asio/reference/basic_deadline_timer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__boost__asio__ssl__error__stream_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/placeholders__signal_number.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_read_stream/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/buffered_read_stream/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload10.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload9.html
/root/boost_1_69_0/doc/html/boost_asio/reference/write/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/async_wait.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__object_handle/object_handle/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/ip__multicast__outbound_interface.html
/root/boost_1_69_0/doc/html/boost_asio/reference/WriteHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/dynamic_buffer.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__misc_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read_until.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__ssl_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/io_context__service/service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/mutable_buffers_1/value_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload6.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload5.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload10.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload3.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload9.html
/root/boost_1_69_0/doc/html/boost_asio/reference/read/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/transfer_exactly.html
/root/boost_1_69_0/doc/html/boost_asio/reference/error__addrinfo_category.html
/root/boost_1_69_0/doc/html/boost_asio/reference/AcceptHandler.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/overlapped_ptr.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/overlapped_ptr/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/reset/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__overlapped_ptr/reset.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__addrinfo_errors__gt_.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/write_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/cancel/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/cancel/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/stream_handle/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/read_some/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/get_io_service.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/async_write_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/get_io_context.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/close/overload2.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/close/overload1.html
/root/boost_1_69_0/doc/html/boost_asio/reference/windows__stream_handle/async_read_some.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__netdb_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/is_error_code_enum_lt__basic_errors__gt_/value.html
/root/boost_1_69_0/doc/html/boost_asio/reference/placeholders__results.html
/root/boost_1_69_0/doc/html/boost_asio/reference/const_buffers_1/value_type.html
/root/boost_1_69_0/doc/html/boost_asio/reference/async_read_until.html
/root/boost_1_69_0/doc/html/boost_asio/index.html
/root/boost_1_69_0/doc/html/boost_asio/net_ts.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer2/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer3.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer4.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer1.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer5/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime5.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime7/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime1.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime3.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer1/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime3/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime2.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer2.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime6.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer3/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer5.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime4/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime7.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime2/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime1/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime5/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime6/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tuttimer4/src.html
/root/boost_1_69_0/doc/html/boost_asio/tutorial/tutdaytime4.html
/root/boost_1_69_0/doc/html/boost_asio/examples/cpp03_examples.html
/root/boost_1_69_0/doc/html/boost_asio/examples/cpp11_examples.html
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/basic_logger.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/logger_service.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/logger_service.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/services/daytime_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/nonblocking/third_party_lib.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/buffers/reference_counted.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/fork/process_per_connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/fork/daemon.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_token_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_udp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/blocking_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/async_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timeouts/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/connection.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/serialization/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/icmp/ipv4_header.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/icmp/ping.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/stream_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/iostream_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/connect_pair.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/local/stream_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/socks4/sync_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/socks4/socks4.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/windows/transmit_file.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/invocation/prioritised_handlers.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/protocol.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/porthopper/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/connection.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/reply.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/reply.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server/server.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/client/async_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/client/sync_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/reply.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/request_parser.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/reply.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/server.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server4/main.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/connection.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/reply.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/reply.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server3/server.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/connection.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/reply.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/io_context_pool.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/reply.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/io_context_pool.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/http/server2/server.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/daytime_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/http_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/iostreams/daytime_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/ssl/client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/ssl/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/async_udp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_tcp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_udp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_udp_echo_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/blocking_tcp_echo_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/echo/async_tcp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/chat_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/chat_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/chat/posix_chat_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/spawn/parallel_grep.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/spawn/echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/multicast/sender.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/multicast/receiver.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/timers/time_t_timer.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp03/allocation/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/range_based_for.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/double_buffered_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/refactored_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/chat_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp17/coroutines_ts/echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/buffers/reference_counted.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/fork/process_per_connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/fork/daemon.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_token_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_udp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/blocking_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/async_tcp_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timeouts/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/stream_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/iostream_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/connect_pair.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/local/stream_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/socks4/sync_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/socks4/socks4.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/invocation/prioritised_handlers.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/connection.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/reply.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/connection.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/reply.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/http/server/server.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/handler_tracking/custom_tracking.hpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/handler_tracking/async_tcp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/bank_account_1.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/bank_account_2.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/pipeline.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/actor.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/priority_scheduler.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/executors/fork_join.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/ssl/client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/ssl/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/async_udp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_tcp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_udp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_udp_echo_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/blocking_tcp_echo_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/echo/async_tcp_echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_4.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_1.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_3.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_2.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/operations/composed_5.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/chat/chat_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/chat/chat_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/spawn/parallel_grep.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/spawn/echo_server.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/futures/daytime_client.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/multicast/sender.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/multicast/receiver.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/timers/time_t_timer.cpp
/root/boost_1_69_0/doc/html/boost_asio/example/cpp11/allocation/server.cpp
/root/boost_1_69_0/doc/html/boost_asio/overview/cpp2011/futures.html
/root/boost_1_69_0/doc/html/boost_asio/overview/cpp2011/move_handlers.html
/root/boost_1_69_0/doc/html/boost_asio/overview/signals.html
/root/boost_1_69_0/doc/html/boost_asio/overview/ssl.html
/root/boost_1_69_0/doc/html/boost_asio/overview/posix/stream_descriptor.html
/root/boost_1_69_0/doc/html/boost_asio/overview/posix/fork.html
/root/boost_1_69_0/doc/html/boost_asio/overview/networking/other_protocols.html
/root/boost_1_69_0/doc/html/boost_asio/overview/networking/protocols.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/line_based.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/coroutine.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/allocation.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/coroutines_ts.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/strands.html
/root/boost_1_69_0/doc/html/boost_asio/overview/core/spawn.html
/root/boost_1_69_0/doc/html/process/reference.html
/root/boost_1_69_0/doc/html/boost_process/tutorial.html
/root/boost_1_69_0/doc/html/boost_process/extend.html
/root/boost_1_69_0/libs/phoenix/example/adapted_echo_server.cpp
/root/boost_1_69_0/libs/asio/test/read_until.cpp
/root/boost_1_69_0/libs/asio/test/archetypes/deprecated_async_ops.hpp
/root/boost_1_69_0/libs/asio/test/archetypes/async_ops.hpp
/root/boost_1_69_0/libs/asio/test/is_write_buffered.cpp
/root/boost_1_69_0/libs/asio/test/system_timer.cpp
/root/boost_1_69_0/libs/asio/test/deadline_timer.cpp
/root/boost_1_69_0/libs/asio/test/error.cpp
/root/boost_1_69_0/libs/asio/test/signal_set.cpp
/root/boost_1_69_0/libs/asio/test/ip/address_v6.cpp
/root/boost_1_69_0/libs/asio/test/ip/network_v4.cpp
/root/boost_1_69_0/libs/asio/test/ip/icmp.cpp
/root/boost_1_69_0/libs/asio/test/ip/address.cpp
/root/boost_1_69_0/libs/asio/test/ip/address_v4.cpp
/root/boost_1_69_0/libs/asio/test/ip/udp.cpp
/root/boost_1_69_0/libs/asio/test/ip/network_v6.cpp
/root/boost_1_69_0/libs/asio/test/ip/unicast.cpp
/root/boost_1_69_0/libs/asio/test/ip/tcp.cpp
/root/boost_1_69_0/libs/asio/test/ip/host_name.cpp
/root/boost_1_69_0/libs/asio/test/ip/v6_only.cpp
/root/boost_1_69_0/libs/asio/test/ip/multicast.cpp
/root/boost_1_69_0/libs/asio/test/unit_test.hpp
/root/boost_1_69_0/libs/asio/test/io_context.cpp
/root/boost_1_69_0/libs/asio/test/is_read_buffered.cpp
/root/boost_1_69_0/libs/asio/test/local/stream_protocol.cpp
/root/boost_1_69_0/libs/asio/test/local/connect_pair.cpp
/root/boost_1_69_0/libs/asio/test/local/datagram_protocol.cpp
/root/boost_1_69_0/libs/asio/test/windows/overlapped_ptr.cpp
/root/boost_1_69_0/libs/asio/test/windows/stream_handle.cpp
/root/boost_1_69_0/libs/asio/test/windows/random_access_handle.cpp
/root/boost_1_69_0/libs/asio/test/windows/object_handle.cpp
/root/boost_1_69_0/libs/asio/test/read_at.cpp
/root/boost_1_69_0/libs/asio/test/buffered_read_stream.cpp
/root/boost_1_69_0/libs/asio/test/read.cpp
/root/boost_1_69_0/libs/asio/test/generic/raw_protocol.cpp
/root/boost_1_69_0/libs/asio/test/generic/stream_protocol.cpp
/root/boost_1_69_0/libs/asio/test/generic/seq_packet_protocol.cpp
/root/boost_1_69_0/libs/asio/test/generic/datagram_protocol.cpp
/root/boost_1_69_0/libs/asio/test/latency/udp_server.cpp
/root/boost_1_69_0/libs/asio/test/latency/tcp_server.cpp
/root/boost_1_69_0/libs/asio/test/latency/tcp_client.cpp
/root/boost_1_69_0/libs/asio/test/latency/udp_client.cpp
/root/boost_1_69_0/libs/asio/test/ssl/stream.cpp
/root/boost_1_69_0/libs/asio/test/connect.cpp
/root/boost_1_69_0/libs/asio/test/serial_port_base.cpp
/root/boost_1_69_0/libs/asio/test/streambuf.cpp
/root/boost_1_69_0/libs/asio/test/posix/stream_descriptor.cpp
/root/boost_1_69_0/libs/asio/test/coroutine.cpp
/root/boost_1_69_0/libs/asio/test/write.cpp
/root/boost_1_69_0/libs/asio/test/socket_base.cpp
/root/boost_1_69_0/libs/asio/test/serial_port.cpp
/root/boost_1_69_0/libs/asio/test/strand.cpp
/root/boost_1_69_0/libs/asio/test/buffers_iterator.cpp
/root/boost_1_69_0/libs/asio/test/buffered_write_stream.cpp
/root/boost_1_69_0/libs/asio/test/write_at.cpp
/root/boost_1_69_0/libs/asio/test/buffer.cpp
/root/boost_1_69_0/libs/asio/test/use_future.cpp
/root/boost_1_69_0/libs/asio/test/buffered_stream.cpp
/root/boost_1_69_0/libs/asio/doc/reference.xsl
/root/boost_1_69_0/libs/asio/doc/using.qbk
/root/boost_1_69_0/libs/asio/doc/examples.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/ShutdownHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/WaitHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/ReadHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/WriteHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/IteratorConnectHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/BufferedHandshakeHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/SignalHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/ConnectHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/ConstBufferSequence.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/RangeConnectHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/MutableBufferSequence.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/Handler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/AcceptHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/HandshakeHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/ResolveHandler.qbk
/root/boost_1_69_0/libs/asio/doc/requirements/MoveAcceptHandler.qbk
/root/boost_1_69_0/libs/asio/doc/reference.qbk
/root/boost_1_69_0/libs/asio/doc/overview/strands.qbk
/root/boost_1_69_0/libs/asio/doc/overview/coroutines_ts.qbk
/root/boost_1_69_0/libs/asio/doc/overview/basics.qbk
/root/boost_1_69_0/libs/asio/doc/overview/allocation.qbk
/root/boost_1_69_0/libs/asio/doc/overview/ssl.qbk
/root/boost_1_69_0/libs/asio/doc/overview/coroutine.qbk
/root/boost_1_69_0/libs/asio/doc/overview/cpp2011.qbk
/root/boost_1_69_0/libs/asio/doc/overview/line_based.qbk
/root/boost_1_69_0/libs/asio/doc/overview/spawn.qbk
/root/boost_1_69_0/libs/asio/doc/overview/other_protocols.qbk
/root/boost_1_69_0/libs/asio/doc/overview/posix.qbk
/root/boost_1_69_0/libs/asio/doc/overview/protocols.qbk
/root/boost_1_69_0/libs/asio/doc/overview/buffers.qbk
/root/boost_1_69_0/libs/asio/doc/overview/signals.qbk
/root/boost_1_69_0/libs/asio/doc/tutorial.qbk
/root/boost_1_69_0/libs/asio/example/cpp03/services/basic_logger.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/services/logger_service.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/services/logger_service.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/services/daytime_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/nonblocking/third_party_lib.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/buffers/reference_counted.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/fork/process_per_connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/fork/daemon.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_token_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_udp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timeouts/blocking_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timeouts/async_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timeouts/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/serialization/connection.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/serialization/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/serialization/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/icmp/ipv4_header.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/icmp/ping.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/local/stream_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/local/iostream_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/local/connect_pair.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/local/stream_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/socks4/sync_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/socks4/socks4.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/windows/transmit_file.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/invocation/prioritised_handlers.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/porthopper/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/porthopper/protocol.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/porthopper/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/connection.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/reply.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/reply.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server/server.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/client/async_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/client/sync_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/reply.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/request_parser.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/reply.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/server.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server4/main.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/connection.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/reply.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/reply.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server3/server.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/connection.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/reply.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/io_context_pool.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/reply.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/io_context_pool.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/http/server2/server.hpp
/root/boost_1_69_0/libs/asio/example/cpp03/iostreams/daytime_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/iostreams/http_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/iostreams/daytime_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/ssl/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/ssl/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/async_udp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_tcp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_udp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_udp_echo_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/blocking_tcp_echo_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/echo/async_tcp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime4/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime6/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime1/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer5/timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime3/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer_dox.txt
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime_dox.txt
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer3/timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime7/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime5/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer4/timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer1/timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/timer2/timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/tutorial/daytime2/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/chat/chat_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/chat/chat_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/chat/posix_chat_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/spawn/parallel_grep.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/spawn/echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/multicast/sender.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/multicast/receiver.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/timers/time_t_timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp03/allocation/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/range_based_for.cpp
/root/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/double_buffered_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/refactored_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/chat_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp17/coroutines_ts/echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/nonblocking/third_party_lib.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/buffers/reference_counted.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/fork/process_per_connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/fork/daemon.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_token_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_udp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timeouts/blocking_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timeouts/async_tcp_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timeouts/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/local/stream_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/local/iostream_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/local/connect_pair.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/local/stream_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/socks4/sync_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/socks4/socks4.hpp
/root/boost_1_69_0/libs/asio/example/cpp11/invocation/prioritised_handlers.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/connection.hpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/reply.hpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/connection.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/reply.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/http/server/server.hpp
/root/boost_1_69_0/libs/asio/example/cpp11/handler_tracking/custom_tracking.hpp
/root/boost_1_69_0/libs/asio/example/cpp11/handler_tracking/async_tcp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/iostreams/http_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/bank_account_1.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/bank_account_2.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/pipeline.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/actor.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/priority_scheduler.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/executors/fork_join.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/ssl/client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/ssl/server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/async_udp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_tcp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_udp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_udp_echo_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/blocking_tcp_echo_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/echo/async_tcp_echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/operations/composed_4.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/operations/composed_1.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/operations/composed_3.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/operations/composed_2.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/operations/composed_5.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/chat/chat_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/chat/chat_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/spawn/parallel_grep.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/spawn/echo_server.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/futures/daytime_client.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/multicast/sender.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/multicast/receiver.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/timers/time_t_timer.cpp
/root/boost_1_69_0/libs/asio/example/cpp11/allocation/server.cpp
/root/boost_1_69_0/libs/process/test/bind_stdin.cpp
/root/boost_1_69_0/libs/process/test/async.cpp
/root/boost_1_69_0/libs/process/test/async_pipe.cpp
/root/boost_1_69_0/libs/process/test/async_system_fail.cpp
/root/boost_1_69_0/libs/process/test/bind_stdout_stderr.cpp
/root/boost_1_69_0/libs/process/test/spawn_fail.cpp
/root/boost_1_69_0/libs/process/test/bind_stderr.cpp
/root/boost_1_69_0/libs/process/test/async_system_stackless.cpp
/root/boost_1_69_0/libs/process/test/async_system_future.cpp
/root/boost_1_69_0/libs/process/test/async_system_stackful_error.cpp
/root/boost_1_69_0/libs/process/test/system_test1.cpp
/root/boost_1_69_0/libs/process/test/exit_code.cpp
/root/boost_1_69_0/libs/process/test/bind_stdout.cpp
/root/boost_1_69_0/libs/process/test/system_test2.cpp
/root/boost_1_69_0/libs/process/test/async_fut.cpp
/root/boost_1_69_0/libs/process/test/spawn.cpp
/root/boost_1_69_0/libs/process/test/async_system_stackful.cpp
/root/boost_1_69_0/libs/process/test/async_system_stackful_except.cpp
/root/boost_1_69_0/libs/process/test/on_exit.cpp
/root/boost_1_69_0/libs/process/test/on_exit3.cpp
/root/boost_1_69_0/libs/process/test/wait.cpp
/root/boost_1_69_0/libs/process/test/on_exit2.cpp
/root/boost_1_69_0/libs/process/doc/autodoc.xml
/root/boost_1_69_0/libs/process/doc/extend.qbk
/root/boost_1_69_0/libs/process/doc/tutorial.qbk
/root/boost_1_69_0/libs/process/example/io.cpp
/root/boost_1_69_0/libs/process/example/async_io.cpp
/root/boost_1_69_0/libs/process/example/wait.cpp
/root/boost_1_69_0/libs/coroutine/doc/coro.qbk
/root/boost_1_69_0/libs/coroutine/doc/motivation.qbk
/root/boost_1_69_0/libs/coroutine/doc/html/coroutine/motivation.html
/root/boost_1_69_0/libs/beast/test/beast/websocket/read1.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/test.hpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/accept.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/doc_snippets.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/stream.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/read2.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/close.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/write.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/utf8_checker.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/handshake.cpp
/root/boost_1_69_0/libs/beast/test/beast/websocket/ping.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/basic_parser.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/serializer.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/test_parser.hpp
/root/boost_1_69_0/libs/beast/test/beast/http/message_fuzz.hpp
/root/boost_1_69_0/libs/beast/test/beast/http/span_body.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/read.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/parser.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/file_body.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/chunk_encode.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/write.cpp
/root/boost_1_69_0/libs/beast/test/beast/http/dynamic_body.cpp
/root/boost_1_69_0/libs/beast/test/beast/experimental/flat_stream.cpp
/root/boost_1_69_0/libs/beast/test/beast/experimental/timeout_service.cpp
/root/boost_1_69_0/libs/beast/test/beast/experimental/timeout_socket.cpp
/root/boost_1_69_0/libs/beast/test/beast/experimental/icy_stream.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/flat_buffer.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffers_prefix.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffer_test.hpp
/root/boost_1_69_0/libs/beast/test/beast/core/read_size.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffered_read_stream.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/type_traits.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/flat_static_buffer.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/multi_buffer.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffers_adapter.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffers_suffix.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/static_buffer.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffer.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/buffers_cat.cpp
/root/boost_1_69_0/libs/beast/test/beast/core/bind_handler.cpp
/root/boost_1_69_0/libs/beast/test/bench/buffers/bench_buffers.cpp
/root/boost_1_69_0/libs/beast/test/bench/wsload/wsload.cpp
/root/boost_1_69_0/libs/beast/test/bench/parser/nodejs_parser.hpp
/root/boost_1_69_0/libs/beast/test/bench/parser/bench_parser.cpp
/root/boost_1_69_0/libs/beast/test/doc/core_examples.cpp
/root/boost_1_69_0/libs/beast/test/doc/core_snippets.cpp
/root/boost_1_69_0/libs/beast/test/doc/http_snippets.cpp
/root/boost_1_69_0/libs/beast/test/doc/websocket_snippets.cpp
/root/boost_1_69_0/libs/beast/test/doc/http_examples.cpp
/root/boost_1_69_0/libs/beast/test/doc/exemplars.cpp
/root/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/sig_wait.hpp
/root/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/yield_to.hpp
/root/boost_1_69_0/libs/beast/test/extras/include/boost/beast/test/websocket.hpp
/root/boost_1_69_0/libs/beast/doc/qbk/03_core/1_asio.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/08_design/4_faq.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/08_design/3_websocket_zaphoyd.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/00_main.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/07_concepts/DynamicBuffer.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/07_concepts/Streams.qbk
/root/boost_1_69_0/libs/beast/doc/qbk/reference.qbk
/root/boost_1_69_0/libs/beast/doc/html/beast/more_examples/expect_100_continue_server.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__basic_timeout_socket/async_write_some.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__basic_timeout_socket/async_read_some.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__http__error.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload2.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload3.html
/root/boost_1_69_0/libs/beast/doc/html/beast/ref/boost__beast__websocket__async_teardown/overload1.html
/root/boost_1_69_0/libs/beast/doc/html/beast/using_io/example_detect_ssl.html
/root/boost_1_69_0/libs/beast/doc/html/beast/using_io/writing_composed_operations.html
/root/boost_1_69_0/libs/beast/doc/docca/include/docca/doxygen.xsl
/root/boost_1_69_0/libs/beast/example/websocket/server/coro-ssl/websocket_server_coro_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/sync-ssl/websocket_server_sync_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/async-ssl/websocket_server_async_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/sync/websocket_server_sync.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/stackless/websocket_server_stackless.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/fast/websocket_server_fast.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/async/websocket_server_async.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/coro/websocket_server_coro.cpp
/root/boost_1_69_0/libs/beast/example/websocket/server/stackless-ssl/websocket_server_stackless_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/coro-ssl/websocket_client_coro_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/sync-ssl/websocket_client_sync_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/async-ssl/websocket_client_async_ssl.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/sync/websocket_client_sync.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/async/websocket_client_async.cpp
/root/boost_1_69_0/libs/beast/example/websocket/client/coro/websocket_client_coro.cpp
/root/boost_1_69_0/libs/beast/example/http/server/coro-ssl/http_server_coro_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/server/sync-ssl/http_server_sync_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/server/async-ssl/http_server_async_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/server/sync/http_server_sync.cpp
/root/boost_1_69_0/libs/beast/example/http/server/stackless/http_server_stackless.cpp
/root/boost_1_69_0/libs/beast/example/http/server/fast/http_server_fast.cpp
/root/boost_1_69_0/libs/beast/example/http/server/async/http_server_async.cpp
/root/boost_1_69_0/libs/beast/example/http/server/small/http_server_small.cpp
/root/boost_1_69_0/libs/beast/example/http/server/flex/http_server_flex.cpp
/root/boost_1_69_0/libs/beast/example/http/server/coro/http_server_coro.cpp
/root/boost_1_69_0/libs/beast/example/http/server/stackless-ssl/http_server_stackless_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/client/coro-ssl/http_client_coro_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/client/sync-ssl/http_client_sync_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/client/async-ssl/http_client_async_ssl.cpp
/root/boost_1_69_0/libs/beast/example/http/client/sync/http_client_sync.cpp
/root/boost_1_69_0/libs/beast/example/http/client/crawl/http_crawl.cpp
/root/boost_1_69_0/libs/beast/example/http/client/async/http_client_async.cpp
/root/boost_1_69_0/libs/beast/example/http/client/coro/http_client_coro.cpp
/root/boost_1_69_0/libs/beast/example/common/root_certificates.hpp
/root/boost_1_69_0/libs/beast/example/common/session_alloc.hpp
/root/boost_1_69_0/libs/beast/example/common/detect_ssl.hpp
/root/boost_1_69_0/libs/beast/example/common/server_certificate.hpp
/root/boost_1_69_0/libs/beast/example/doc/http_examples.hpp
/root/boost_1_69_0/libs/beast/example/advanced/server/advanced_server.cpp
/root/boost_1_69_0/libs/beast/example/advanced/server-flex/advanced_server_flex.cpp
/root/boost_1_69_0/libs/beast/example/echo-op/echo_op.cpp
/root/boost_1_69_0/libs/beast/example/cppcon2018/net.hpp
/root/boost_1_69_0/libs/beast/CHANGELOG.md
/root/boost_1_69_0/libs/log/doc/tmp/sinks_reference.xml
/root/boost_1_69_0/libs/log/src/syslog_backend.cpp
/root/boost_1_69_0/libs/thread/test/test_9303.cpp
/root/boost_1_69_0/libs/coroutine2/doc/coro.qbk
/root/boost_1_69_0/libs/coroutine2/doc/motivation.qbk
/root/boost_1_69_0/libs/fiber/doc/asio.qbk
/root/boost_1_69_0/libs/fiber/doc/fibers.qbk
/root/boost_1_69_0/libs/fiber/doc/integration.qbk
/root/boost_1_69_0/libs/fiber/doc/callbacks.qbk
/root/boost_1_69_0/libs/fiber/examples/asio/ps/publisher.cpp
/root/boost_1_69_0/libs/fiber/examples/asio/ps/subscriber.cpp
/root/boost_1_69_0/libs/fiber/examples/asio/ps/server.cpp
/root/boost_1_69_0/libs/fiber/examples/asio/exchange.cpp
/root/boost_1_69_0/libs/fiber/examples/asio/autoecho.cpp
/root/boost_1_69_0/libs/fiber/examples/asio/round_robin.hpp
</details>

## Шаг 8

Скомпилировать Boost

Команды:

```sh
cd ~/boost_1_69_0
./bootstrap.sh
./b2
```

<details>
  <summary>Вывод команды </summary>
 
Смотреть документ [Exersize 8]( https://github.com/barsik20/lab01/blob/main/Exersize%208 "Перейти к файлу Exersize 8")
</details>

## Шаг 9
 Перенос статических библиотек в ~/boost-libs
Команды:

```sh
mkdir -p ~/boost-libs
cp stage/lib/*.a ~/boost-libs/
```



## Шаг 10
Размер каждого файла в ~/boost-libs
Команды:

```sh
du -h ~/boost-libs/*
```
<details>
  <summary>Вывод команды </summary>
  4.5M    libboost_wave.a <br>
  2.7M    libboost_regex.a <br>
  2.7M    libboost_math_tr1l.a <br>
  2.7M    libboost_math_tr1.a <br>
  2.6M    libboost_math_tr1f.a <br>
  2.3M    libboost_unit_test_framework.a <br>
  2.3M    libboost_test_exec_monitor.a <br>
  2.0M    libboost_locale.a <br>
  1.6M    libboost_program_options.a <br>
  1.2M    libboost_serialization.a <br>
  848K    libboost_graph.a <br>
  796K    libboost_wserialization.a <br>
  544K    libboost_math_c99.a <br>
  464K    libboost_math_c99l.a <br>
  448K    libboost_math_c99f.a <br>
  416K    libboost_filesystem.a <br>
  332K    libboost_contract.a <br>
  284K    libboost_iostreams.a <br>
  236K    libboost_chrono.a <br>
  232K    libboost_fiber.a <br>
  212K    libboost_prg_exec_monitor.a <br> 
  152K    libboost_date_time.a <br>
  148K    libboost_container.a <br>
  80K     libboost_random.a <br>
  56K     libboost_timer.a <br>
  24K     libboost_stacktrace_addr2line.a <br>
  24K     libboost_context.a <br>
  20K     libboost_stacktrace_backtrace.a <br>
  16K     libboost_stacktrace_basic.a <br>
  4.0K    libboost_system.a <br>
  4.0K    libboost_stacktrace_noop.a <br>
  4.0K    libboost_exception.a <br>
  4.0K    libboost_atomic.a <br>
</details>

## Шаг 11
Top-10 самых больших файлов

Команды:

```sh

du -h ~/boost-libs/* | sort -hr | head -n 10

```
<details>
  <summary>Вывод команды </summary>
4.5M    /root/boost-libs/libboost_wave.a <br>
2.7M    /root/boost-libs/libboost_regex.a <br>
2.7M    /root/boost-libs/libboost_math_tr1l.a <br>
2.7M    /root/boost-libs/libboost_math_tr1.a <br>
2.6M    /root/boost-libs/libboost_math_tr1f.a <br>
2.3M    /root/boost-libs/libboost_unit_test_framework.a <br>
2.3M    /root/boost-libs/libboost_test_exec_monitor.a <br>
2.0M    /root/boost-libs/libboost_locale.a <br>
1.6M    /root/boost-libs/libboost_program_options.a <br>
1.2M    /root/boost-libs/libboost_serialization.a <br>

</details>
