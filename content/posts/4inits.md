+++
title = "4 альтернативные малоизвестные системы инициализации"
date = "2022-08-10"
description = "4 альтернативных малоизвестных инита"
[taxonomies]
tags=["Linux", "init", "pid1"]
+++

4 альтернативных малоизвестных инита

1. Runit

Написан на языке Си Герритом Пэйпом. Заимствует концепцию из sysvinit. Также является супервизором, для логгирования есть утилита svlogd
Применяется как стандартный init в Void, Dragora GNU/Linux, Artix, также доступен для FreeBSD, OpenBSD, NetBSD

http://smarden.org/runit/

2. Dinit

Изначально написанный Дэвином МакКолом, неожиданно быстро получил признание в виде включения по умолчанию в Chimera Linux — Linux-дистрибутив с окружением FreeBSD, LLVM, Musl. Также доступен в Artix Linux. При разработке учитывались недостатки и достоинства других инитов и супервизоров

https://github.com/davmac314/dinit

3. Finit

Проект по реверс-инжинирингу fastinit от Asus EeePC. Разрабатывается совместно с сопутствующими инструментами sysklogd, watchdogd. Есть скрипты для быстрой установки в Alpine, Void и Debian

https://troglobit.com/projects/finit/

4. shinit

Невероятно простой инит в 5 строк кода, написанный на shell

https://github.com/cemkeylan/shinit
