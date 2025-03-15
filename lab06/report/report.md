---
## Front matter
title: "Лабораторная работа № 6"
subtitle: "Модель «хищник–жертва"
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

Реализовать модель "хищник-жертва" в *xcos*.

# Задание

1. Реализовать модель "хищник-жертва" в xcos;
2. Реализовать модель "хищник-жертва" с помощью блока Modelica в xcos;
3. Реализовать модель "хищник-жертва" в OpenModelica

# Выполнение лабораторной работы

Модель «хищник–жертва» (модель Лотки — Вольтерры) представляет собой модель
межвидовой конкуренции. В математической
форме модель имеет вид:

$$
\begin{cases}
  \dot x = ax - bxy \\
  \dot y = cxy - dy,
\end{cases}
$$

где $x$ — количество жертв; $y$ — количество хищников; $a, b, c, d$ — коэффициенты, отражающие взаимодействия между видами: $a$ — коэффициент рождаемости
жертв; $b$ — коэффициент убыли жертв; $c$ — коэффициент рождения хищников; $d$ —
коэффициент убыли хищников.

## Реализация модели в xcos

Зафиксируем начальные данные: $a = 2, \, b = 1, \, c = 0.3, \, d = 1, \, x(0) = 2, \, y(0) = 1$.
В меню Моделирование, Задать переменные окружения зададим значения коэффициентов $a, \, b, \, c, \, d$ ъ\.

![Задание переменных окружения в xcos для модели](image/23.png)

Для реализации модели "хищник-жертва" в дополнение к блокам `CLOCK_c`, `CSCOPE`, `TEXT_f`,
`MUX`, `INTEGRAL_m`, `GAINBLK_f`, `SUMMATION`, `PROD_f` потребуется блок `CSCOPXY` --
регистрирующее устройство для построения фазового портрета.
Готовая модель «хищник–жертва» представлена на рис. .

![Модель «хищник–жертва» в xcos](image/1.png)

В параметрах блоков интегрирования необходимо задать начальные значения $x(0) = 2, y(0) = 1$ .

![Задание начальных значений в блоках интегрирования](image/2.png)

![Задание параметров моделирования](image/4.png)

В меню Моделирование, Установка необходимо задать конечное время интегрирования, равным времени моделирования: 30.

Результат моделирования представлен на рис.. Черной линией обозначен график $x(t)$ (динамика численности жертв), зеленая линия определяет $y(t)$ — динамику численности хищников

![Динамика изменения численности хищников и жертв модели Лотки-Вольтерры при $a = 2, b = 1, c = 0.3, d = 1, x(0) = 2, y(0) = 1$](image/21.png)

На рис.  приведён фазовый портрет модели Лотки-Вольтерры.

![Фазовый портрет модели Лотки-Вольтерры при $a = 2, b = 1, c = 0.3, d = 1, x(0) = 2, y(0) = 1$](image/12.png)

## Реализация модели с помощью блока Modelica в xcos

Для реализации модели с помощью языка Modelica потребуются следующие
блоки *xcos*: `CLOCK_c`, `CSCOPE`, `CSCOPXY`, `TEXT_f`, `MUX`, `CONST_m` и `MBLOCK` (Modelica
generic).
Как и ранее, задаём значения коэффициентов $a, b, c, d$ .
Готовая модель «хищник–жертва» представлена на .
Параметры блока Modelica представлены на рис. Переменные на входе (“a”,
“b”, “c”, “d”) и выходе (“x”, “y”) блока заданы как внешние (“E”).

![Модель «хищник–жертва» в xcos с применением блока Modelica](image/14.png)

![Параметры блока Modelica для модели "хищник–жертва"](image/19.png)

![Параметры блока Modelica для модели "хищник–жертва"](image/13.png)

В результате моделирования получаем следующие графики . Они идентичны построенным без блока Modelica.

![Динамика изменения численности хищников и жертв модели Лотки-Вольтерры при $a = 2, b = 1, c = 0.3, d = 1, x(0) = 2, y(0) = 1$](image/20.png)

![Фазовый портрет модели Лотки-Вольтерры при $a = 2, b = 1, c = 0.3, d = 1, x(0) = 2, y(0) = 1$](image/22.png)


# Выводы

В процессе выполнения данной лабораторной реализована модель "хищник-жертва" в *xcos*.
