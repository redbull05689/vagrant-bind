Домашнее задание
настраиваем split-dns
взять стенд https://github.com/erlong15/vagrant-bind

добавить еще один сервер client2

завести в зоне dns.lab

имена
web1 - смотрит на клиент1
web2 смотрит на клиент2
завести еще одну зону newdns.lab

завести в ней запись www - смотрит на обоих клиентов

настроить split-dns

клиент1 - видит обе зоны, но в зоне dns.lab только web1

клиент2 видит только dns.lab

*) настроить все без выключения selinux Критерии оценки: 4 - основное задание сделано, но есть вопросы 5 - сделано основное задание 6 - выполнено задания со звездочкой

Основное задание
Запустить стенд командой vagrant up && sudo ansible-playbook -i provisioning/inventory.yml provisioning/playbook.yml . 
Проветить роботоспособность командой dig.

Клиент1 - видит обе зоны, но в зоне dns.lab только web1
[vagrant@client1 ~]$ dig @192.168.50.11 web1.dns.lab +short
192.168.50.15
[vagrant@client1 ~]$ dig @192.168.50.11 web2.dns.lab +short
[vagrant@client1 ~]$ dig @192.168.50.11 www.newdns.lab +short
192.168.50.15
192.168.50.16
[vagrant@client1 ~]$ 

Клиент2 видит только dns.lab
[vagrant@client2 ~]$ dig @192.168.50.10 web1.dns.lab +short
192.168.50.15
[vagrant@client2 ~]$ dig @192.168.50.10 web2.dns.lab +short
192.168.50.16
[vagrant@client2 ~]$ dig @192.168.50.10 www.newdns.lab +short
[vagrant@client2 ~]$
