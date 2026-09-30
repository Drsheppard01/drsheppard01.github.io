+++
title = "Linux Survival Guide"
date = "2022-01-19"
description = "Как оптимизировать Linux, чтобы получать удовольствие"
[taxonomies]
tags=["Linux", "optimization", "Linux Desktop"]
+++

# Сила Терминала

Первое, что я советую новичкам на Linux — смените стандартный интерпретатор командной строки с Bash на Zsh:

Сперва установим Zsh:

Для Debian/Ubuntu:

```shell
sudo apt-get install zsh
```

Для Fedora:

```shell
sudo apt-get install zsh
```

Для Arch:

```shell
sudo pacman -Suy zsh
```

Сменить bash на zsh можно следующей командой:

```shell
sudo chsh -s /bin/zsh $(whoami)
```

Далее, установите плагин менеджеров, их бесчисленное множество, но я предпочитаю zim

Установка zim:

```shell
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

Установите micro - консольный редактор с привычными сочетаниями клавиш для быстрой работы

Для Debian/Ubuntu:

```shell
sudo apt-get install micro
```

Для Fedora:

```shell
sudo apt-get install micro
```

Для Arch:

```shell
sudo pacman -Suy micro
```

Я также ставлю fastfetch - консольная информация о системе, bottom - консольный менеджер ресурсов, gdu - анализ использования дисков

# Стероиды для гномов

Многие согласятся, что GNOME по умолчанию лишён многих важных вещей. Вот список некоторых дополнений, который упростит взаимодействие с ним:

1. AppIndicator для значков в трее: <https://extensions.gnome.org/extension/615/appindicator-support/>
2. Desktop Icons для иконок рабочего стола: <https://extensions.gnome.org/extension/5263/gtk4-desktop-icons-ng-ding/>
3. User Themes для применения темы GTK к теме GNOME: <https://extensions.gnome.org/extension/19/user-themes/>

Для Nautilus я использую следующие дополнения:

1. Начальный вид Nautilus как в проводнике Windows: со всеми папками и устройствами: <https://github.com/yannmasoch/nautilus-my-computer>
2. BackSpace for Nautilus для возврата на предыдущую страницу по нажатию BackSpace <https://github.com/jesusferm/Nautilus-BackSpace/blob/main/BackSpaceGnome49.py>
3. Open-any-terminal для открытия папок и файлов в терминале отличных от стандартного <https://github.com/Stunkymonkey/nautilus-open-any-terminal>

# Наряжаем ёлку

Для внешнего вида я использую: 

Тему GTK: <https://github.com/vinceliuice/Colloid-gtk-theme> Colloid-Yellow-Light-Nord
Тему иконок: <https://github.com/darkomarko42/Marwaita-Icons> Marwaita
Шрифт: <https://fonts.google.com/specimen/Geist> Geist

# Чистим хвосты

Если вам кажется, что systemd — отвратительная служба запуска, то ~~вы правы~~ самое время проверить ваш журнал:

```shell
sudo journalctl --vacuum-size=48M # эта функция удаляет все ранние журналы, пока их размер не сократится на 48 мегабайт
```

Смотрим другие службы, которые могут мешать:

```shell
systemd-analyze
```

Чаще всего это служба проверки интернета NetworkManager-wait-online. Удаляем её из автозапуска:

```shell
sudo systemctl disable NetworkManager-wait-online.service
```

> [!NOTE]  
>  Осиротевшие пакеты - это пакеты, установленные как зависимости для других пакетов. Пример: вы ранее удалили fastfetch. Для конфигураций fastfetch использует библиотеку yyjson, которая является зависимостью к пакету fastfetch. Если пакет с библиотекой yyjson больше не нужен другой программе, то после выполнения следующей операции он будет удалён.

В Debian/Ubuntu:

```shell
sudo apt-get --purge autoremove
```

Для Fedora:

```shell
sudo dnf autoremove ## обычно включён по умолчанию
```

Для Arch:

```shell
sudo pacman -Qdttq | pacman -Rs -
```
