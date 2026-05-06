+++
title = "Linux Survival Guide. Оптимизация загрузки"
date = "2022-01-20"
description = "Как настроить терминал, чтобы получать удовольствие"
[taxonomies]
tags=["Linux", "optimization", "Linux Desktop", "terminal"]
+++

# Linux Survival Guide #2 | Сила Терминала

Первое, что я советую новичкам на Linux — смените bash на zsh

Он более кастомизируемый и сильно помогает в работе

Сменить bash на zsh можно следующей командой:

```shell
sudo chsh -s /bin/zsh $(whoami)
```

Далее, установите плагин менеджеров, их бесчисленное множество, но я предпочитаю oh-my-zsh или zim

Установка oh-my-zsh:

```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Установка zim:

```shell
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

Установите плагины. Для oh-my-zsh

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Затем измените раздел в ~/.zshrc следующим образом:

```shell
plugins=(zsh-autosuggestions
zsh-syntax-highlighting)
```

В zim эти плагины установлены по умолчанию
