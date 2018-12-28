#wordpress-ansible

Плейбук Ansible для автоматизированной установки веб-сервера с wordpress на Ubuntu Server
хост Ubuntu 16.04.1 LTS
создан на CentOS 7

(Применимо в случае, если хост подключается впервые и на нем не установлен Ansible)
Перед запуском плейбука необходимо подготовить удаленный хост. Установить на него Phyton-minimal. Сгенерировать ключи для доступа по SSH без пароля.

$ apt-get update
$ apt-get install python-minimal

Генерация ключей и копирование на хост

$  ssh-keygen

Копирование ключа на хост 
$ ssh-copy-id root@ip хоста

Проверка авторизации (Должен заходить без пароля)

$ ssh root@ip хоста

После выполнения условий, можно переходить к установке плейбука ansible. Плейбук зашифрован с помощью ansible-vault. Для выполнения команды можно воспользоваться 2 способами.

1. Выполнить команду ansible-vault decrypt (в этом случае файл дешифруется, и снимется защита)

$ ansible-vault decrypt WP-playbook.yml
В строке Vault password: ввести пароль

#mysql_root_password=#password# вместо "#password#" ввести свой пароль от базы MySQL, используется для настройки MySQL и задания таблиц при уставки WordPress

$ ansible-playbook WP-playbook.yml -i hosts -e mysql_root_password=#password# 

2. Запустить плейбук с оператором --ask-vault-pass (в этом случае файл дешифруется только для выполнения, файл останется зашифрованным)

$ ansible-playbook WP-playbook.yml -i hosts -e mysql_root_password=#password# --ask-vault-pass

В строке Vault password: ввести пароль

После успешной установки можно переходить в админку Wordpress по адресу хоста для последующей настройки.
