+++
title = "Linux Survival Guide. Оптимизация загрузки"
date = "2022-01-19"
description = "Как оптимизировать Linux, чтобы получать удовольствие"
[taxonomies]
tags=["Linux", "optimization", "Linux Desktop"]
+++

# Linux Survival Guide #1 | Оптимизация загрузки

Если вам кажется, что systemd — отвратительная служба запуска, то самое время проверить ваш журнал

```shell
sudo journalctl --disk-usage
```

Если их ОЧЕНЬ много, то время уборки:

```shell
sudo journalctl --vacuum-size=96M
```

Также можно использовать аргументы `vacuum-time=2days` или `vacuum-files=50files`

Просмотреть время загрузки дистрибутива очень просто:

```shell
systemd-analyze
```

Однако, помните, что loader не включает grub (только если вы, как я, грузитесь из systemd-boot)

Хотите увидеть загрузку в виде графа? Пожалуйста:

```shell
systemd-analyze plot > boot.svg
```

Так, а почему так много времени занимает загрузки graphics.target? Сейчас узнаем:

```shell
systemd-analyze critical-chain
```

Удалите старые ядра (и вообще все потерянные пакеты заодно), в Debian/Ubuntu:

```shell
sudo apt-get --purge autoremove
```

В Solus:

```shell
sudo clr-boot-manager update
# (удаляет старые ядра)
sudo eopkg rmo 
#удаляет все потерянные пакеты
```
