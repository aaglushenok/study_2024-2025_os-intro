---
## Front matter
lang: ru-RU
title: Индивидуальный проект. Стадия 1.
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

# Информация

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

Размещение на Github pages заготовки для персонального сайта.

## Задание

1. Установить необходимое программное обеспечение.
2. Скачать шаблон темы сайта.
3. Разместить его на хостинге git.
4. Установить параметр для URLs сайта.
5. Разместить заготовку сайта на Github pages.

## Установка необходимого ПО

Скачаем hugo sites с github:

![Скачивание hugo sites (1)](image/1.jpg){#fig:001 width=40%}

![Скачивание hugo sites (2)](image/2.jpg){#fig:002 width=40%}

## Распаковка архива

Распакуем ахив, переместим hugo в каталог /usr/local/bin:

![Распаковка архива, перемещение hugo](image/3.jpg){#fig:003 width=60%}

## Скачивание шаблона темы сайта

Откроем репозиторий с шаблоном, "use this template" -> "create new repository", создав новый репозиторий

![Переход к шаблону](image/4.jpg){#fig:004 width=40%}

![Создание репозитория по шаблону](image/5.jpg){#fig:005 width=40%}

## Создание и елонирование нового репозитория

Зададим имя website (далее изменен на "blog"), клонируем в папку work:

![Ввод имени репозитория](image/6.jpg){#fig:006 width=40%}

![Клонирование репозитория](image/7.jpg){#fig:007 width=40%}

## Установка go

Скачаем go через sudo dnf install go:

![Скачивание go](image/8.jpg){#fig:008 width=60%}

## Сборка сайта, открытие

Введем hugo server, сайт "соберется", в терминале получим ссылку и номер порта для открытия 

![Сборка сайта](image/9.jpg){#fig:009 width=60%}

## Создание 2-го репозитория

Создадим еще один репозиторий, зададим имя "aaglushenok.github.io

![Создание 2-го нового репозитория](image/10.jpg){#fig:010 width=40%}

![Именование репозитория](image/11.jpg){#fig:011 width=40%}

## Клонирование репозитория, выполнение коммита

Клонируем 2-ой репозиторий в work, используя "git checkout -b main" переключимся на ветку main. Создадим фиктивный файл README.md. Пропишем git add ., выполним коммит

![Клонирование репозитория, переход на ветку main](image/12.jpg){#fig:012 width=40%}

![Выполнение коммита](image/13.jpg){#fig:013 width=40%}

## Удаление public, добавление submodule, повторная сборка

Перейдем в blog (бывш. website), удалим public. Добавим submodule. Пропишем hugo, убедимя, что puplic удален, введем "git remote -v"

![Добавление submodule, удаление public](image/14.jpg){#fig:014 width=40%}

![Повторная сборка; Проверка удаления public](image/15.jpg){#fig:015 width=40%}

## Коммит, отправка файлов

Введем git add ., выполним коммит. Пропишем git push для отправки файлов, с указанием ветки origin main

![Выполнение коммита](image/16.jpg){#fig:016 width=40%}

![Отправка файлов](image/17.jpg){#fig:017 width=40%}

## Проверка правильности создания репозитория

Откроем репозиторий, убедимся, что он заполнен необходимыми файлами

![Проверка наличия файлов](image/18.jpg){#fig:018 width=60%}

## Открытие сайта через ссылку

Копируем имя репозитория, введем в виде ссылки в FireFox. Убедимся, что по ссылке открывается наш сайт:

![Копирование имени репозитория](image/19.jpg){#fig:019 width=40%}

![Открытие сайта по ссылке](image/20.jpg){#fig:020 width=40%}

## Выводы

В ходе выполнения первой стадии индивидуального проекта мне удалось разместить на Github pages заготовки для персонального сайта.

## Благодарю за внимание!
