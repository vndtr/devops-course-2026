\# Конфигурация виртуальной машины devops-vm



\## 1. Параметры машины

\- Объём памяти: 2048 МБ

\- Количество ядер: 2

\- Объём диска: 25 ГБ



\## 2. Сетевые интерфейсы

\- Адаптер 1: NAT (полученный адрес: 10.0.2.15)

\- Адаптер 2: Host-only (полученный адрес: 192.168.56.101)



\## 3. Правило проброса портов

\- Порт хостовой системы: 2222

\- Порт гостевой системы: 2222



\## 4. Учётные записи

\- `student` (администратор, вход по паролю)

\- `devops` (администратор (sudo), вход по SSH-ключу \~/.ssh/devops\_vm)



\## 5. Служба SSH

\- Порт: 2222

\- Изменённые директивы: PermitRootLogin no, PasswordAuthentication no, MaxAuthTries 3, AllowUsers devops

\- Расположение файла конфигурации: /etc/ssh/sshd\_config.d/99-hardening.conf



\## 6. Правила межсетевого экрана

\- Политики по умолчанию: deny incoming, allow outgoing

\- Перечень правил: 2222/tcp (LIMIT), 80/tcp (ALLOW), 443/tcp (ALLOW)



\## 7. Снимки состояния

\- 01-clean-install

\- 02-keys-configured

\- 03-ssh-hardened

\- 04-ufw-and-dns

## 8. Веб-сервер
- Устанавливаемый пакет: nginx
- Путь к конфигурации ресурса: /etc/nginx/sites-available/devops-site
- Каталог ресурса: /var/www/devops-site (владелец devops:devops, права 755 для каталога, 644 для файлов)
- Путь к сертификату: /etc/ssl/certs/devops.crt (права 644)
- Путь к ключу: /etc/ssl/private/devops.key (права 600, владелец root)
- Команда формирования сертификата: sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/devops.key -out /etc/ssl/certs/devops.crt -subj "/CN=devops.local" -addext "subjectAltName=DNS:devops.local"
- Срок действия сертификата: 1 год

