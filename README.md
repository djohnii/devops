git clone ssh://git@prey.homelab.com:222/root/devops.git
## Добавляем fetch 
git remote add origin ssh://git@prey.homelab.com:222/aloha/devops.git
git remote set-url --add --push origin ssh://git@prey.homelab.com:222/aloha/devops.git

## Добавляем еще один 
git remote set-url --add --push origin git@github.com:YOUR_USERNAME/devops.git

git remote -v


## Если возникнут проблемы 
Это заберёт коммиты с GitHub и сольёт
```
git pull origin main --allow-unrelated-histories

```
