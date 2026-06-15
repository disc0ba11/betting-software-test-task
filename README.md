## Шаги для проверки работоспособности, корректности настройки sshd и идемпотентности плейбука
1. Поднять контейнер с Ubuntu:24.04 `docker compose up -d --build`
2. Сгенерировать rsa-ключ для пользователя developer `ssh-keygen -t rsa -C "developer@local"`
3. Подставить содержимое `cat ~/.ssh/id_rsa.pub` вместо публичного ключа пользователя developer в inventory/group_vars/all.yml
4. Запустить плейбук `ansible-playbook init.yml`
5. Запустить плейбук ещё раз, чтобы убедиться в идемпотентности `ansible-playbook init.yml`
6. Подключиться по ssh `ssh developer@127.0.0.1 -p 2222 -i ~/.ssh/id_rsa` (пароль: developer), чтобы убедиться, что developer использует zsh с omz
7. Открыть в браузере `127.0.0.1:80/images/`, чтобы убедиться, что nginx раздаёт статику

Спасибо!
