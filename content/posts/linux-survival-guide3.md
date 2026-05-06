+++
title = "Linux Survival Guide. Оптимизируй то, оптимизируй это"
date = "2022-01-24"
description = "Как настроить терминал, чтобы получать удовольствие"
[taxonomies]
tags=["Linux", "optimization", "Linux Desktop", "terminal"]
+++

Linux Survival Guide #3 | Оптимизируй то, оптимизируй это

Первое, что мы делаем, в наших постинсталл (я их называю "домашние скрипты") скриптах — это обновляем всю систему до актуального состояния и заменяем программы на нужные, а ненужные удаляем

Т.к. я использую Budgie или GNOME на Solus, то первое что я удаляю — ненужные приложения GNOME:

1. gnome-photos | заменяю shotwell
2. gnome-terminal | заменяю kitty
3. eog | заменяю shotwell
4. evince | заменяю brave (.pdf), bookworm для всего остального
5. gnome-mpv | заменяю VLC
6. rhythmbox | заменяю VLC
7. hexchat | удаляю как ненужное
8. thunderbird | удаляю как ненужное или заменяю Mailspring
9. seahorse | заменяю bitwarden
10. firefox | заменяю на brave
11. gnome-system-monitor | заменяю bottom
12. gnome-weather | заменяю как ненужное, использую curl wttr.in/<мой город> либо заменяю апплетом погоды (актуально для Budgie)
13. gnome-maps | удаляю как ненужное
14. yelp | удаляю как ненужное
15. gnome-mahjongg | удаляю как ненужное
16. gnome-disk-utility | заменяю gdu

Если вы используете flatpak, не лишним будет удалить неиспользуемые среды выполнения с помощью flatpak remove --delete-data --unused

Если вы используете snap то откройте ваш редактор и вставьте следующий текст

```shell
### elegantly stolen from Alan Popey's script

snap refresh

LANG=C snap list --all | awk '/disabled/{print $1, $3}' |
    while read snapname revision; do
        sudo snap remove "$snapname" --revision="$revision"
    done
```

В некоторых случаях я также предлагаю установить sof-firmware и сменить Pulseaudio на PipeWire. На моём дистрибутиве это делается следующим образом

```shell
sudo eopkg it pipewire wireplumber sof-firmware
systemctl --user enable pipewire
systemctl --user enable --now wireplumber
systemctl --user disable pulseaudio pulseaudio.socket
systemctl --user enable pipewire-pulse.socket pipewire-pulse
```

После перезагрузитесь

Также, в некоторых случаях, для лучшей производительности системы, я настоятельно рекомендую использовать ядро Xanmod и файловую систему XFS