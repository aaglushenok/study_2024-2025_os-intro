---
## Front matter
title: "Лабораторная работа №12. Настройки сети в Linux"
subtitle: "Отчет"
author: "Анна Александровна Глушенок"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получить навыки настройки сетевых параметров системы.

# Задание  

1. Продемонстрируйте навыки использования утилиты ip (см. раздел 12.4.1).
2. Продемонстрируйте навыки использования утилиты nmcli (см. раздел 12.4.2 и 12.4.3).

# Выполнение лабораторной работы

## Проверка конфигурации сети

1. Получите полномочия администратора: su -
2. Выведите информацию о существующих сетевых подключениях, статистику о количестве отправленных пакетов и связанных с ними ошибках: ip -s link

Пояснение: интерфейс 2 - enp0s3, в результате вывода видим статус его активности (активен, state UP), сетевой кабель (LOWER_UP), максимальный размер пакета данных равный 1500 байт (mtu 1500), MAC-адрес (08:00:27...), и информацию о статистике (принятые пакеты, отправленные пакеты, ошибки и др)

![Задание 1-2](image/1.png){#fig:001 width=80%}

3. Выведите на экран информацию о текущих маршрутах: ip route show
4. Выведите на экран информацию о текущих назначениях адресов для сетевых интерфейсов на устройстве: ip addr show

![Задание 3-4](image/2.png){#fig:002 width=80%}

Пояснение для 3: в результате вывода видим, что весь интернет-трафик идет через шлюз 10.0.2.2, а локальнгая сеть это 10.0.2.0/24

Пояснение для 4: рассмотрим интерфейс enp0s3 - основной сетевой адаптер. IPv4-адрес устройства - 10.0.2.15. Адаптер активен (UP), подключен к кабелю (LOWER_UP), имеет MAC-адрес (08:00:27...) и получает IPv4-адрес 10.0.2.15/24 автоматически по dhcp (dynamic)

5. Используйте команду ping для проверки правильности подключения к Интернету. Для отправки четырёх пакетов на IP-адрес 8.8.8.8 введите: ping -c 4 8.8.8.8

![Задание 5](image/3.png){#fig:003 width=80%}

6. Добавьте дополнительный адрес к вашему интерфейсу: ip addr add 10.0.0.10/24 dev esp0s3 (esp0s3 — название интерфейса, которому добавляется IP-адрес)
7. Проверьте, что адрес добавился: ip addr show (добавился под номером 2)

![Задание 6-7](image/4.png){#fig:004 width=80%}

8. Сравните вывод информации от утилиты ip и от команды ifconfig: ifconfig (ip - подробный вывод с логической структурой, ifconfig - базовая статистическая информация о работе интерфейса)

![Задание 8](image/5.png){#fig:005 width=80%}

9. Выведите на экран список всех прослушиваемых системой портов UDP и TCP: ss -tul

![Задание 9](image/6.png){#fig:006 width=80%}

## Управление сетевыми подключениями с помощью nmcl

1. Получите полномочия администратора. Выведите на экран информацию о текущих соединениях: nmcli connection show
2. Добавьте Ethernet-соединение с именем dhcp к интерфейсу: nmcli connection add con-name "dhcp" type ethernet ifname enp0s3 (enp0s3 -название интерфейса)
3. Добавьте к этому же интерфейсу Ethernet-соединение с именем static, статическим IPv4-адресом адаптера и статическим адресом шлюза: nmcli connection add con-name "static" ifname enp0s3 autoconnect no type ethernet ip4 10.0.0.10/24 gw4 10.0.0.1 ifname enp0s3 (enp0s3 - название интерфейса)
4. Выведите информацию о текущих соединениях: nmcli connection show

![Задание 1-4](image/7.png){#fig:007 width=80%}

5. Переключитесь на статическое соединение: nmcli connection up "static". Проверьте успешность переключения при помощи nmcli connection show и ip addr

![Задание 5](image/8.png){#fig:008 width=80%}

6. Вернитесь к соединению dhcp: nmcli connection up "dhcp". Проверьте успешность переключения при помощи nmcli connection show
и ip addr

![Задание 6](image/9.png){#fig:009 width=80%}

## Изменение параметров соединения с помощью nmcl

1. Отключите автоподключение статического соединения: nmcli connection modify "static" connection.autoconnect no
2. Добавьте DNS-сервер в статическое соединение: nmcli connection modify "static" ipv4.dns 10.0.0.10
3. Добавьте второй DNS-сервер (через +): nmcli connection modify "static" +ipv4.dns 8.8.8.8
4. Измените IP-адрес статического соединения: nmcli connection modify "static" ipv4.addresses 10.0.0.20/24
5. Добавьте другой IP-адрес для статического соединения: nmcli connection modify "static" +ipv4.addresses 10.20.30.40/16

![Задание 1-5](image/10.png){#fig:010 width=80%}

6. После изменения свойств соединения активируйте его: nmcli connection up "static". Проверьте успешность переключения при помощи nmcli con show и ip addr

![Задание 6](image/11.png){#fig:011 width=80%}

7. Используя nmtui, посмотрите и опишите в отчёте настройки сети на устройстве

![Задание 7](image/12.png){#fig:012 width=80%}

![Задание 7](image/13.png){#fig:013 width=80%}

Пояснение: в настройках сети мы можем редактировать подключение, активировать подключение, настроить имя хоста и переключатель. Мы так же видим активные в данный момент сети (static, dhcp, enp0s3), можем изменять их, удалять или добавлять новые

8. Посмотрите настройки сетевых соединений в графическом интерфейсе операционной системы

![Задание 8](image/14.png){#fig:014 width=80%}

9. Переключитесь на первоначальное сетевое соединение: nmcli connection up enp0s3 (enp0s3 - название интерфейса)

![Задание 9](image/15.png){#fig:015 width=80%}

## Контрольные вопросы 

1. Какая команда отображает только статус соединения, но не IP-адрес?
Команда ip link show или nmcli general status.

2. Какая служба управляет сетью в ОС типа RHEL?
Служба NetworkManager.

3. Какой файл содержит имя узла (устройства) в ОС типа RHEL?
Файл /etc/hostname.

4. Какая команда позволяет вам задать имя узла (устройства)?
Команда hostnamectl set-hostname <имя>.

5. Какой конфигурационный файл можно изменить для включения разрешения имён для конкретного IP-адреса?
Файл /etc/hosts.

6. Какая команда показывает текущую конфигурацию маршрутизации?
Команда ip route или route -n.

7. Как проверить текущий статус службы NetworkManager?
Командой systemctl status NetworkManager.

8. Какая команда позволяет вам изменить текущий IP-адрес и шлюз по умолчанию для вашего сетевого соединения?
Команда nmcli connection modify или редактирование файлов в /etc/sysconfig/network-scripts/.
   
# Вывод

В ходе выполнения лабораторной работы №12 мне удалось получить навыки настройки сетевых параметров системы.

# Список литературы{.unnumbered}

::: {#refs}
:::
