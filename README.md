# IptablesHW
Домашнее задание на тему "Работа с  Iptables"
Задание:
Что нужно сделать?
реализовать knocking port
centralRouter может попасть на ssh inetrRouter через knock скрипт
пример в материалах.
добавить inetRouter2, который виден(маршрутизируется (host-only тип сети для виртуалки)) с хоста или форвардится порт через локалхост.
запустить nginx на centralServer.
пробросить 80й порт на inetRouter2 8080.
дефолт в инет оставить через inetRouter.
Для начала устанавливаем Vagrant, Virtualbox и Ansible
Установка Vagrant:
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
apt update && sudo apt install vagrant
Установка VirtualBox:
apt install virtualbox
Установка Ansible:
apt install software-properties-common
add-apt-repository --yes --update ppa:ansible/ansible
apt install ansible
Создаём директорию, пишем файлы и запускаем командой:
vagrant up
Попытайтесь сразу подключиться по SSH к inetRouter (192.168.10.1) – должно быть отказано в доступе (таймаут или connection refused).
Выполните последовательность ударов:
knock 192.168.10.1 1111 2222 3333
И тут же подключайтесь
ssh 192.168.10.1
Проверка маршрутизации в интернет
На любом устройстве
ping -c 3 8.8.8.8
Если есть ответ, то работает)
Проверка проброса порта
На хосте нужно откройте браузер и перейдите по адресу:
http://192.168.56.10:8080
Вы должны увидеть страницу nginx.
Задание на этом выполнено!
