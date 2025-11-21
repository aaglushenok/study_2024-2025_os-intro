---
## Front matter
lang: ru-RU
title: Лабораторная работы №12. Настройки сети в Linux
subtitle: Презентация
author:
  - Глушенок А. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 24 октября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
---

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Глушенок Анна Александровна
  * Студент НПИбд-01-24
  * Факультет физико-математических и естественных наук
  * Российский университет дружбы народов
  * [1132246844@pfur.ru](mailto:1132246844@pfur.ru)
  * <https://github.com/aaglushenok>

:::
::: {.column width="30%"}

:::
::::::::::::::

## Цель работы

Получить навыки настройки сетевых параметров системы.

## Задание  

1. Продемонстрируйте навыки использования утилиты ip (см. раздел 12.4.1).
2. Продемонстрируйте навыки использования утилиты nmcli (см. раздел 12.4.2 и 12.4.3).

# Выполнение лабораторной работы

# Проверка конфигурации сети

## Проверка конфигурации сети

1. Получите полномочия администратора: su -
2. Выведите информацию о существующих сетевых подключениях, статистику о количестве отправленных пакетов и связанных с ними ошибках: ip -s link

![Задание 1-2](image/1.png){#fig:001 width=40%}

## Проверка конфигурации сети

3. Выведите информацию о текущих маршрутах: ip route show
4. Выведите информацию о текущих назначениях адресов для сетевых интерфейсов на устройстве: ip addr show

![Задание 3-4](image/2.png){#fig:002 width=40%}

## Проверка конфигурации сети

5. Используйте ping для проверки правильности подключения к Интернету. Для отправки четырёх пакетов на IP-адрес 8.8.8.8 введите: ping -c 4 8.8.8.8

![Задание 5](image/3.png){#fig:003 width=40%}

## Проверка конфигурации сети

6. Добавьте дополнительный адрес к интерфейсу: ip addr add 10.0.0.10/24 dev esp0s3
7. Проверьте, что адрес добавился: ip addr show

![Задание 6-7](image/4.png){#fig:004 width=40%}

## Проверка конфигурации сети

8. Сравните вывод информации от утилиты ip и от команды ifconfig: ifconfig 

![Задание 8](image/5.png){#fig:005 width=40%}

## Проверка конфигурации сети

9. Выведите список прослушиваемых системой портов UDP и TCP: ss -tul

![Задание 9](image/6.png){#fig:006 width=40%}

# Управление сетевыми подключениями с помощью nmcl

## Управление сетевыми подключениями с помощью nmcl

1. Получите полномочия администратора. Выведите информацию о текущих соединениях: nmcli connection show
2. Добавьте соединение dhcp к интерфейсу: nmcli connection add con-name "dhcp" type ethernet ifname enp0s3
3. Добавьте соединение static: nmcli connection add con-name "static" ifname enp0s3 autoconnect no type ethernet ip4 10.0.0.10/24 gw4 10.0.0.1 ifname enp0s3
4. Выведите информацию о текущих соединениях: nmcli connection show

![Задание 1-4](image/7.png){#fig:007 width=40%}

## Управление сетевыми подключениями с помощью nmcl

5. Переключитесь на статическое соединение: nmcli connection up "static". Проверьте успешность переключения

![Задание 5](image/8.png){#fig:008 width=40%}

## Управление сетевыми подключениями с помощью nmcl

6. Вернитесь к соединению dhcp: nmcli connection up "dhcp". Проверьте успешность переключения при помощи

![Задание 6](image/9.png){#fig:009 width=40%}

# Изменение параметров соединения с помощью nmcl

## Изменение параметров соединения с помощью nmcl

1. Отключите автоподключение статического соединения: nmcli connection modify "static" connection.autoconnect no
2. Добавьте DNS-сервер в статическое соединение: nmcli connection modify "static" ipv4.dns 10.0.0.10
3. Добавьте второй DNS-сервер (через +): nmcli connection modify "static" +ipv4.dns 8.8.8.8
4. Измените IP-адрес статического соединения: nmcli connection modify "static" ipv4.addresses 10.0.0.20/24
5. Добавьте другой IP-адрес для статического соединения: nmcli connection modify "static" +ipv4.addresses 10.20.30.40/16

![Задание 1-5](image/10.png){#fig:010 width=40%}

## Изменение параметров соединения с помощью nmcl

6. После изменения свойств соединения активируйте его: nmcli connection up "static". Проверьте успешность переключения

![Задание 6](image/11.png){#fig:011 width=40%}

## Изменение параметров соединения с помощью nmcl

7. Используя nmtui, посмотрите настройки сети на устройстве

![Задание 7](image/12.png){#fig:012 width=40%}

## Изменение параметров соединения с помощью nmcl

![Задание 7](image/13.png){#fig:013 width=40%}

## Изменение параметров соединения с помощью nmcl

8. Посмотрите настройки сетевых соединений в графическом интерфейсе операционной системы

![Задание 8](image/14.png){#fig:014 width=40%}

## Изменение параметров соединения с помощью nmcl

9. Переключитесь на первоначальное сетевое соединение: nmcli connection up enp0s3

![Задание 9](image/15.png){#fig:015 width=40%}

## Вывод

В ходе выполнения лабораторной работы №12 мне удалось получить навыки настройки сетевых параметров системы.

# Благодарю за внимание!
