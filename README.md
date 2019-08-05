Домашнее задание
VPN

Между двумя виртуалками поднять vpn в режимах
tun
tap Прочуствовать разницу.
Поднять RAS на базе OpenVPN с клиентскими сертификатами, подключиться с локальной машины на виртуалку
3*. Самостоятельно изучить, поднять ocserv и подключиться с хоста к виртуалке

1. Между двумя виртуалками поднять vpn
Запустить стенд vagrant up && ansible-playbook playbook-server.yml && ansible-playbook playbook-client.yml
Скопировать файл конфигурации с сервера на клиент и запустить(например: openvpn --config client.ovpn)
Стэнд поднимится с openvpn udp
Измерит скорость соеденения iper3
Примечание: !!!По необходимости добавить правила
firewall-cmd --permanent --add-port=5201/tcp --zone=internal
firewall-cmd --permanent --add-port=5201/udp --zone=internal
firewall-cmd --reload


Вывод iperf

OpenVPN with proto tcp
ok: [ovc] => {
    "result.stdout_lines": [
        "------------------------------------------------------------", 
        "Client connecting to 10.9.0.1, TCP port 5201", 
        "TCP window size: 45.0 KByte (default)", 
        "------------------------------------------------------------", 
        "[  3] local 192.168.111.59 port 60468 connected with 10.9.0.1 port 5201", 
        "[ ID] Interval       Transfer     Bandwidth", 
        "[  3]  0.0-10.0 sec   413 MBytes   345 Mbits/sec"
    ]
}
OpenVPN with proto udp
PS C:\Users\Max\Documents\OTUS\Linux-OTUS> iperf3.exe -c 10.9.0.1
Connecting to host 10.9.0.1, port 5201
[  4] local 10.9.0.6 port 54411 connected to 10.9.0.1 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  4.75 MBytes  39.8 Mbits/sec
[  4]   1.00-2.00   sec  4.12 MBytes  34.6 Mbits/sec
[  4]   2.00-3.00   sec  4.62 MBytes  38.8 Mbits/sec
[  4]   3.00-4.00   sec  3.62 MBytes  30.4 Mbits/sec
[  4]   4.00-5.00   sec  5.25 MBytes  44.1 Mbits/sec
[  4]   5.00-6.00   sec  5.25 MBytes  44.1 Mbits/sec
[  4]   6.00-7.00   sec  3.38 MBytes  28.3 Mbits/sec
[  4]   7.00-8.00   sec  4.12 MBytes  34.6 Mbits/sec
[  4]   8.00-9.00   sec  4.50 MBytes  37.7 Mbits/sec
[  4]   9.00-10.00  sec  3.62 MBytes  30.5 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  43.2 MBytes  36.3 Mbits/sec                  sender
[  4]   0.00-10.00  sec  43.2 MBytes  36.3 Mbits/sec                  receiver

iperf Done.
