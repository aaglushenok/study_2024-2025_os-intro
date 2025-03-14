---
## Front matter
lang: ru-RU
title: Лабораторная работы №1. Установка ОС Linux.
subtitle: Презентация
author:
  - Глушенок А. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 06 марта 2025

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
  * <https://github.com/aaglushenok/study_2024-2025_arh-pc>

:::
::: {.column width="30%"}

:::
::::::::::::::

## Цель 

Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

## Задание

1. Установить операционную систему.
2. Установить обновления, отключить SELinux.
3. Настроить раскладку клавиатуры.
4. Установить имя пользователя и название хоста.
5. Установить ПО ждя создания документации.

## Созднание виртуальной машины

Имя виртуальной машины, папка хранения, образ диска ISO, основную память, процессоры

![Создание ВМ](image/1.PNG){#fig:001 width=40%}

![Оборудование](image/2.PNG){#fig:002 width=40%}

## Настройка виртуальной машины

Конфигурация жесткого диска, размер диска, видеопамять, 3D-ускорение

![Виртуальный жесткий диск](image/3.PNG){#fig:003 width=40%}

![Настройка дисплея](image/4.PNG){#fig:004 width=40%}

## Запуск виртуальной машины

запуск, команда liveinst, место установки, аккаунт пользователя и учетка root: 

![Ввод команды liveinst](image/5.PNG){#fig:005 width=25%}

![Обзор установки](image/6.PNG){#fig:006 width=25%}

![Создание пользователя](image/7.PNG){#fig:007 width=25%}

![Аккаунт администратора](image/8.PNG){#fig:008 width=25%}

## Обновления, повышение комфорта работы

вход в ОС, установка средств разработки, обновление пакетов, установка автообновления, таймер

![Вход в ОС, установка обновлений](image/9.PNG){#fig:009 width=40%}

![Повышение комфорта работы](image/10.PNG){#fig:010 width=40%}

## Отключение SELinux

замена значения SELINUX=enforcing на значение SELINUX=permissive

![Внесение изменений в файл](image/11.PNG){#fig:011 width=60%}

## Настройка раскладки клавиатуры

создание конфигурационных файлов, редактирование

![Создание конфигурационного файла](image/12.PNG){#fig:012 width=25%}

![Редактирование 1-го конфигурационного файла](image/13.PNG){#fig:013 width=25%}

![Запуск конфигурационных файлов](image/14.PNG){#fig:014 width=25%}

![Редактирование 2-го конфигурационного файла](image/15.PNG){#fig:015 width=25%}

## Установка имени пользлвателя и названия хоста

пользователь и его пароль, имя хоста, проверка

![Установка имени пользователя и названия хоста](image/16.PNG){#fig:016 width=60%}

## Установка ПО для создания документации

средство pandoc, пакет pandoc-crossref, распаковка архивов, их перемещение

![Установка ПО для создания документации](image/17.PNG){#fig:017 width=40%}

![Распаковка архива](image/18.PNG){#fig:018 width=40%}

## Установка TeXlive

дистрибутив TeXlive

![Установка TeXlive](image/19.PNG){#fig:019 width=60%}

## Выполнение домашней работы (1)

1. Версия ядра Linux: 6.12.15-200.
2. Частота процессора: 2496.010.
3. Модель процессора: Intel (R) Core (TM).
4. Объем доступной оперативной памяти: 5119544K.
5. Тип обнаруженного гипервизора: KVM.
6. Тип файловой системы корневого раздела: sda4.
7. Последовательность монтирования файловых систем: BTRFS, EXT4-fs.

## Выполнение домашней работы (2)

ввод команд для домашней работы в терминал

![Выполнение домашней работы](image/20.PNG){#fig:020 width=60%}

## Выводы

В ходе выполнения лабораторной работы №1 мне удалось приобрести практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

## Благодарю за внимание!
