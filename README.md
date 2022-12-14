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
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

____

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

Попробуем добавить новых элементов на сцену. Добавим новый ассет пак для добавления облаков на сцену, как для кнопок так и просто разнообразие визуала.
![image](https://user-images.githubusercontent.com/100475554/200399924-0a1e8a63-6005-40cd-ab56-41398ae5c6b8.png)

Создаём дупликат облака, добавляем его себе в проект. Облако мы прикрепляем к интерфейсу игрока. В *Canvas* можем выполнить расположение объекта на сцене. Но нам не нужно чтобы наше облако просто висело в воздухе. Нужно добавить ему движения. Для этого создаём элемент анимации (в папке анимаций конечно же) и создаём точки изменения позиции нашего облачка.
Также якорим наше облако в левом углу, чтобы его позиция оставалась одной при разных разрешениях.
### Вуаля, облачко плавает по нашему экрану.

![unknown_2022 11 08-01 09_clip_1_1](https://user-images.githubusercontent.com/100475554/200405748-ca19e848-5fa6-4e96-9659-2fe70bb49748.gif)

Продолжим работу с начальной сценой. Наша цель чтобы нажав кнопку `играть`, наш игрок мог непосредственно начать **играть**. Бля этого нам нужны
+ сама кнопка
+ скрипт который позволит переключать сцены
Так-же не маловажным заданием будет добавить название игры на сцену. Создаём элемент текст, пишем название, в моём случае это ***Dragon Masonry***

![image](https://user-images.githubusercontent.com/100475554/200413712-d7998251-c8b9-4378-92e1-2a02c5679736.png)

Создаём кнопки в нашем канвасе, располагаем на экране. Так-же можно заменить само изображение за текстом кнопки. Дополнительно я создал кнопки для настройки и выхода из игры. Когда кнопки настроенны и расположенны, можно переходить к созданию скрипта нашей кнопки `play`

![image](https://user-images.githubusercontent.com/100475554/200414495-b857a4c9-6cb7-45eb-950b-a1d349659be6.png)

Создаём *C# Script*, в нём нас интересует добавление библиотеки **SceneManagement** для управления сценой. Прописываем два метода, входа в игру и выхода из неё.

```c#
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenuScript : MonoBehaviour
{
    public void PlayGame(){
        SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex+1);
    }
    
    public void QuitGame(){
        Application.Quit();
    }
}
```

Остаётся включить. Создаём пустой объект *Main menu* в него закидываем наш скрипт. Далее заходим в кнопку `Play` и в ней *"по нажатию"* добавляем Главное Меню и выбираем интересующий нас метод PlayGame. То же самое делаем для кнопки выход, но пока без эфектов.

![image](https://user-images.githubusercontent.com/100475554/200416019-4a0a07f2-3988-4115-a1c9-3dc88d09a3d0.png)

Далее остаётся только добавить наши обе сцены в раздел "Build" и всё заработает.

![image](https://user-images.githubusercontent.com/100475554/200416169-abb5d783-75fc-4d0a-9425-b1f7a32df352.png)
### Проверяем работу
![unknown_2022 11 08-02 10_1](https://user-images.githubusercontent.com/100475554/200417116-0947dac0-2b67-4087-8e2d-00eb34879e7f.gif)

Сделаем предварительную настройку кнопки `Options` добавив переход к настройкам и кнопкой `Back`. Дублируем наше главное меню. Переименовывем пункт выход Quit в Back.
Теперь без кода нужно настроить поведение кнопок по нажатию. 

Такие я сделал настройки для кнопки `Options`, и обратные для `Back`

![image](https://user-images.githubusercontent.com/100475554/200644167-42340174-ae67-40ec-b7b6-e5561c21ba6f.png)

### А так выглядит работа в *Unity*
![unknown_2022 11 08-23 20_1](https://user-images.githubusercontent.com/100475554/200645513-15c56587-3ce6-4af0-b638-78a9d41fe50d.gif)

Нужно сделать паузу. Для этого нам нужен новый скрипт, и две панели, одна для текста, другая для непрозрачного фона. 
В скрипте нам нужно изменять значение *timeScale*. Пишем скрипт ниже, и в разделе *Inspector* добавляем наши настроенные панели

```c#
using UnityEngine.SceneManagement;

public class PauseScript : MonoBehaviour
{
    private bool paused = false;

    public GameObject textPanel;
    public GameObject panel;

    void Update() 
    {
        if (Input.GetKeyDown(KeyCode.Space)){
            if (!paused){
                Time.timeScale = 0;
                paused = true;
                panel.SetActive(true);
                textPanel.SetActive(true);
            }
            else {
                Time.timeScale = 1;
                paused = false;
                panel.SetActive(false);
                textPanel.SetActive(false);
            }
        }
        if (Input.GetKeyDown(KeyCode.Escape)) {
            SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex - 1);
        }
    }

}

```

### Получаем такой результат
![unknown_2022 11 09-15 21_1](https://user-images.githubusercontent.com/100475554/200806197-97a17672-3af6-43cc-8437-c960d243f016.gif)

Сделаем нашу игру более живой, добавив в неё звуков. Мы хотим добавить саундтрек, который будет сопровождать игрока в меню и во время игры. Так-же необходимо добавить звуки для взаимодействий объектов **Egg** и **Shield**. Нам в этом помогут следующие два ассет пака:

![image](https://user-images.githubusercontent.com/100475554/201058318-52f97bf2-3ed8-411b-846a-7dee3ff94ccd.png)
![image](https://user-images.githubusercontent.com/100475554/201059525-59329035-18d2-4c0a-9f10-573f06020fb2.png)

Для того чтобы добавить любому из объектов необходимо добавить ему компонент ***Audio Source*** и добавить ему необходимую звуковую дорожку. Покажу на примере подключения музыки во время игры

![image](https://user-images.githubusercontent.com/100475554/201089388-c6da6de8-3aa1-4031-8759-de71dbb7df9f.png)

В настройках нас интересуют два момента. Если мы подключаем саундтрек который будет звучать всё время что играет игрок, нас интересует кнопка *Loop* чтобы композиция не заканчивалась. А в случае евентов, как например уничтожение яйца, нужно выключить *On awake* чтобы звук не проигрывался сразу при начале игры. 
В случае евентов нам нужно сделать так чтобы по колизии звучал наш звук. Интересующие меня звуки я перенёс в свой проект, и прописал данную конструкцию в коде **Яйца** и **Щита**.
```c#
public AudioSource audioSource;

audioSource = GetComponent<AudioSource>();
        audioSource.Play();
```

Гифкой звук не передать, но в [ссылке на игру](https://yandex.ru/games/app/198497?draft=true&lang=ru) вы можете убедиться в работе.

Добавим нового персонажа в нашу игру. Теперь это будет маг управляющий щитом, с которым игрок сможет себя ассоциировать. Для этого нам потребуется сайт [mixamo.com](https://www.mixamo.com/#/). Тут нам необходимо найти интересующую нас модельку и анимацию для него. 
Мой выбор пал на такую модельку чернокнижницы, и такую анимацию "управления щитом"

![unknown_2022 11 10-18 36_1](https://user-images.githubusercontent.com/100475554/201107297-a7e5483b-7d95-40c9-a42c-02664fd2867e.gif)

Теперь нам нужно загрузить её, и добавить в проект.
Добавить её можно простым перетаскиванием в префабы проекта. Дальше важным моментом является распаковка текстур. 

![image](https://user-images.githubusercontent.com/100475554/201107569-d771f7f0-b617-4c28-9e5e-f8545e11cfe9.png)

Распаковав текстуры, нам нужно сделать дупликат анимации, добавить её в соответствующую папку нашего проекта, и добавить её в новый *Animation controller*.
Располагаем нашу героиню на сцене, добавляем ей анимацию. Так-же крутым дополнением будет добавить героине небольшую подсветку. Создаём настраиваем элемент *Point Light* и располагаеи рядом с нашей героиней.

![image](https://user-images.githubusercontent.com/100475554/201109163-b2136255-9f4b-4a70-80ad-514093b5f855.png)

### Вот как это выглядит в Unity.

![unknown_2022 11 10-18 51_1](https://user-images.githubusercontent.com/100475554/201112130-a4f35fbc-f89c-459d-9687-748c33c19c44.gif)

## Задание 2.

На момент написание лабораторной существуют множество разных платформ. Игроки сами могут выбрать удобную для себя, наша же задача как разработчиков, дать им возможность беспрепятсвтенно играть в наш проект

Первый пример особенности сборки проектка под разные платформы, это то какоt расширение имеет файл конечного продукта. К примеру на **Android** это **.apk**, в то время как на **ПК** это **.exe** 

Второй пример чуть больше связан с тем чем мы занимаемся на этом курсе. Выпуск игры в разных игровых магазинах тоже может влиять на то как мы будем делать билд, и что будем в него включать, ведь на этом могут быть завязаны как система достижений, так и более сложные механики вроде Лидербордов, или например как система Steam Remote Play? для запуска игры почти на любом устройстве.

Так-же при создании и сборке проекта стоит учитывать какое управление будет включено в сборку.

Ещё может иметь смысл создание билда под 32 и 64 разрядные процессоры и системы. 

Последним примером приведу одну из особенностей сборки под WebGL. Дело в том что в Unity собирая проект есть параметр ***Development Build*** необходимый для отладки и тестировки приложения. Но для WebGl функция ***Script Debugging*** недоступна, тк билд собирается несколько иначе, чем под другие платформы.

![image](https://user-images.githubusercontent.com/100475554/201335733-3b531b39-0031-4293-b875-531775adae4f.png)
![image](https://user-images.githubusercontent.com/100475554/201335751-8017c0b8-7e37-4c21-91c0-abf5b099d165.png)



Таким образом каждая платформа может иметь свои различия в сборке, начиная от размера проекта до отладки, и все эти моменты нужно учитывать.

## Задание 3.

Для того чтобы сделать контроль звука нам нужны две вещи
1. Слайдер
2. Скрипт который будет передавать значения слайдера и менять звук

На стартовой сцене я добавил через меню UI слайдер.
![image](https://user-images.githubusercontent.com/100475554/201149806-a6ad8125-8f98-474d-ad8e-db173725837b.png)

Реализацию слайдера и звуков сделал с помощью двух скриптов

```c#
using UnityEngine.UI;

public class SliderCTRL : MonoBehaviour
{

    public GameObject AudioSource;

    public float oldVolume;
    public Slider slider;
    // Start is called before the first frame update
    void Start()
    {
        
        oldVolume = slider.value;
    }

    // Update is called once per frame
    void Update()
    {
        if (oldVolume != slider.value){
            PlayerPrefs.SetFloat("volume", slider.value);
            PlayerPrefs.Save();
            oldVolume = slider.value;
        }

    }
}
```

```c#
public class AudioCTRL : MonoBehaviour
{
    public AudioSource audio_;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        audio_.volume = PlayerPrefs.GetFloat("volume");
    }
}

```

Работу звуков и игры вы можете увидеть по [ссылке на игру](https://yandex.ru/games/app/198497?draft=true&lang=ru)

## Выводы
За время лабораторной я ознакомился и усвоил следующие навыки:
1. Создание главного меню, с его настройкой, UI и звуками
2. Подключение звуков в игру
3. Создание механики паузы
4. Импорт анимированных персонажей из mixamo
5. Настройка звуков с помощью слайдера
6. Ознакомился с особенностями разработки билда под разные платформы

[Черновик игры на Яндекс Играх](https://yandex.ru/games/app/198497?draft=true&lang=ru)
