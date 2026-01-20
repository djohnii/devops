# Шаг 1: Настройка основного remote (fetch/pull)
git remote add origin ssh://git@prey.homelab.com:222/aloha/devops.git

# Шаг 2: Добавление push URL для всех платформ
git remote set-url --add --push origin ssh://git@prey.homelab.com:222/aloha/devops.git
git remote set-url --add --push origin git@github.com:djohnii/devops.git
git push origin main --force-with-lease
# Проверка
git remote -v

Результат: git push origin main → пушит в оба репозитория одновременно.

## VSCODE
для удобства с портами 

nano ~/.ssh/config

```
Host gitlab-homelab
    HostName prey.homelab.com
    Port 222
    User git
    IdentityFile ~/.ssh/djohnii

Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/djohnii
```

chmod 600 ~/.ssh/config

## Проблемы и решение

| Проблема                                                                     | Решение                                                                          |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Permission denied (publickey)                                                | ssh-add ~/.ssh/djohniissh -T git@github.com                                      |
| SSH-агент не запущенCould not open a connection to your authentication agent | eval "$(ssh-agent -s)"ssh-add ~/.ssh/djohnii                                     |
| Self-hosted GitLab порт 222                                                  | ssh://git@host:222/user/repo.gitили ~/.ssh/config с Port 222                     |
| No such remote 'origin'                                                      | git remote add origin URL                                                        |
| rejected (fetch first)Updates were rejected because the remote contains work | git pull origin main --allow-unrelated-historiesgit push origin main             |
| stale info на GitHub                                                         | git fetch git@github.com:USER/REPOgit push git@github.com:USER/REPO main --force |
| Удалить push URL                                                             | git remote set-url --delete --push origin URL                                    |
| Неправильные права SSH                                                       | chmod 700 ~/.sshchmod 600 ~/.ssh/id_*chmod 644 ~/.ssh/id_*.pub                   |
| Дублирующиеся push URL                                                       | git remote set-url --delete --push origin WRONG_URLдобавить заново правильный    |
| .ppk ключ (PuTTY) не читается                                                | puttygen key.ppk -O private-openssh -o keyssh-add key                            |
| Everything up-to-date но GitHub не синхронизирован                           | git push git@github.com:USER/REPO main --force-with-lease                        |