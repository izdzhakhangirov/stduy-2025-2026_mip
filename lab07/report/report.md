---
## Front matter
title: "Лабораторная работа № 7"
subtitle: "Модель M|M|1|"
author: "Джахангиров Илгар Залид оглы"

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
lot: false # List of tables
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
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
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

Рассмотреть пример моделирования в *xcos* системы массового обслуживания типа $M|M|1|\infty$.

# Задание

1. Реализовать модель системы массового обслуживания типа $M|M|1|\infty$;
2. Построить график поступления и обработки заявок;
3. Построить график динамики размера очереди.

# Выполнение лабораторной работы

Зафиксируем начальные данные: $\lambda = 0.3, \, \mu = 0.35, \, z_0 = 6$. В меню Моделирование, Установить контекст зададим значения коэффициентов (рис. [-@fig:001]).

![Задание переменных окружения в xcos для модели](image/1.png)

Суперблок, моделирующий поступление заявок, представлен на рис. [-@fig:002]. Тут у нас заявки поступают в систему по пуассоновскому закону. Поступает заявка в суперблок, идет в синхронизатор входных и выходных сигналов, происходит равномерное распределение на интервале $[0; 1]$ (также заявка идет в обработчик событий), далее идет преобразование в экспоненциальное распределение с параметром $\lambda$, далее заявка опять попадает в обработчик событий и выходит из суперблока.

![Суперблок, моделирующий поступление заявок](image/2.png)

Суперблок, моделирующий процесс обработки заявок, представлен на рис. [-@fig:003]. Тут происходит обработка заявок в очереди по экспоненциальному закону.

![Суперблок, моделирующий обработку заявок](image/3.png)

Готовая модель$M|M|1|\infty$ представлена на рис. [-@fig:004]. Тут есть селектор, два суперблока, построенных ранее, первоначальное событие на вход в суперблок, суммирование, оператор задержки (имитация очереди), также есть регистрирующие блоки: регистратор размера очереди и регистратор событий.

![Модель $M|M|1|\infty$ в xcos](image/4.png)

Результат моделирования представлен на рис. [-@fig:005] . График динамики размера очереди начинается со значения 6, потому что мы указали $z_0 = 6$.

![Динамика размера очереди](image/5.png)

# Выводы

В процессе выполнения данной лабораторной работы я рассмотрел пример моделирования в *xcos* системы массового обслуживания типа $M|M|1|\infty$.
