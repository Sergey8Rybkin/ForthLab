# Лабораторная работа № 4 Доработка интерактивного приложения и его подготовка к сборке

Отчет по лабораторной работе #4 выполнил:
- Рыбкин Сергей Денисович
- РИ-300012

[Репозиторий с проектом](https://github.com/Sergey8Rybkin/Dragon-Picker)

[Черновик игры на Яндекс Играх](https://yandex.ru/games/app/198497?draft=true&lang=ru)

Отметка о выполнении заданий:

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

### Задание 1
Используя видео-материалы практических работ 1-5 повторить реализацию
приведенного ниже функционала:
– 1 Практическая работа «Создание анимации объектов на сцене»
– 2 Практическая работа «Создание стартовой сцены и переключение
между ними»
– 3 Практическая работа «Доработка меню и функционала с остановкой
игры»
– 4 Практическая работа «Добавление звукового сопровождения в игре»
– 5 Практическая работа «Добавление персонажа и сборка сцены для
публикации на web-ресурсе»

### Задание 2
Привести описание того, как происходит сборка проекта проекта под другие
платформы. Какие могут быть особенности?

### Задание 3
Добавить в меню Option возможность изменения громкости (от 0 до 100%)
фоновой музыки в игре.

## Задание 1.

Нам необходимо сделать стартовую сцену, которую увидит наш игрок как только войдёт в игру.
Делаем копию нашей существующей сцены, попробуем реализовать меню элементами уже сущаствующими.

![image](https://user-images.githubusercontent.com/100475554/200386297-992457ac-6b15-440f-9f2b-06b255607879.png)

На нашей новой сцене удаляем *plane*, удаляем скрипты из дракона и главной камеры (весь функционал игры не интересует нас до момента пока игрок не нажмёт ***play***). Теперь нужно заняться расстановкой дракона и горы, чтобы это интересно выглядело. Сменим расположение и размер горы, а так-же перенесём на неё дракона. Мы будем иметь следующие значения *transform* :
![image](https://user-images.githubusercontent.com/100475554/200387291-2e08456f-3068-4d5c-bd59-245e2e2d6cc4.png) ![image](https://user-images.githubusercontent.com/100475554/200387313-aed67b29-a0d0-48aa-908f-099df26ab9fa.png)
Нам так-же нужно добавить дракону другую анимацию. Создаём новый *Animation Controller* и добавляем туда другую анимацию.

### Получаем довольного дракона, ждущего когда с ним уже поиграют
![unknown_2022 11 07-23 32_1](https://user-images.githubusercontent.com/100475554/200388004-e445ca8b-a3c0-4df6-98b4-329c379031a4.gif)

