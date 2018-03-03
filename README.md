# VKAnalysis
[Фото]

Приложение для анализа данных персональных страниц и сообществ социальной сети Вконтакте.
Может быть эффективно использовано для помощи HR-специалисту в принятии кадровых решений, для защиты имиджа организаций, для решения задач социологических исследований и т.д.
Доступно из коробки:
- анализ текстов постов пользователей и сообществ
- анализ фото пользователей и сообществ на неприемлемый контент
- определение круга общения пользователей
- определение интересов пользователей
- определение времени активности пользователей [пока не размещено]

## Функции
### Анализ текстовой информации
[фото]

Позволяет проверять на наличие неприемлемого (или интересующего) контента посты пользователей и сообществ. Реализуемая на основе библиотеки pymorphy2 поддержка морфологии позволяет значительно уменьшить размер словарей, оставив при этом высокую точность распознавания.
По умолчанию доступны следующие словари, которые были созданы на основе страниц пользователей:
- нецензурная лексика (брань)
- алкоголь и тусовки
- курение
- наркотики
- жестокость
- инфантилизм
Предусмотрена возможность простого добавления своих словарей а также их генерации на основе страниц Вконтакте.

### Анализ фотографий
[фото]

Позволяет проверять фото пользователей и сообществ на наличие неприемлемого (NSFW) контента на основе OpenNSFW от Yahoo.
Можно заменить модель нейросети на свою, что позволит искать на фото, например, логотип компании.

### Определение круга общения пользователя
[фото]

Помогает определить возможный круг общения пользователя на основе параметров:
- общий город
- общий возраст
- общие друзья
- лайки друзьям
- лайки друзей

### Определение интересов пользователя
[фото]

Помогает сделать выводы об интересах пользователя на основе понравившихся публикаций. Заглядывает к друзьям и в сообщества пользователя и показывает публикации, на которых пользователь поставил лайк или отрепостил.

### Определение времени онлайна пользователя
[фото]
[временно не доступно]

Позволяет построить график пользовательской активности: когда заходил и выходил из сети.

## Установка
### Установка Python 
Первым делом необзодимо установить Python 3.5 (Можно любую 3-ю версию, но тогда не будет работать библиотека Caffe, а, значит, и модуль анализа фотографий).
Для установки Python идем на сайт https://www.python.org/downloads/, качаем версию 3.5.* и устанавливаем
### Добавление окружения
Для того, чтобы не зависеть от изменений пакетов, можно (но не необходимо) добавить виртуальное окружение.
Можно скачать уже готовое, ссылку, наверное, скину.

Для этого открываем командную строку и пишем: `python -m venv venv/`

Активируем окружение: `venv/Scripts/activate`

### Установка пакетов
Теперь необходимо установить пакеты.
Если не нужен модуль анализа фотографий, то нужно выполнить только:

`pip install -r stdreq.txt`

и затем отключить модуль анализа фотографий (как -- написано ниже).

Для того, чтобы использовать модуль анализа фото, нужно совершить чуть больше действий из-за особенностей используемой библиотеки:
идем на сайт http://www.silx.org/pub/wheelhouse/ и ищем версию numpy c MKL(!!!) для своей версии ПК и Python35. Например, для Windows10 с 64 разрядным процессом подойдет версия numpy-1.13.3+mkl-cp35-cp35m-win_amd64.whl
Также необходимо скачать scipy-1.0.0rc1-cp35-cp35m-win_amd64.whl

Устанавливаем эти пакеты:

```
pip install numpy-1.13.3+mkl-cp35-cp35m-win_amd64.whl
pip install scipy-1.0.0rc1-cp35-cp35m-win_amd64.whl
```
Затем выполняем `pip install -r pic_req.txt`

Все готово=)
Теперь, находясь в окружении, приложение можно запускать командой `python .\VKAnalysis.py`
Чтобы не нужно было каждый раз через командную строку входить в окружение, создадим файл run.bat:

```
@echo off
@call venv\Scripts\activate.bat
python VKAnalysis\VKAnalysis.py
```

## Установка и удаление модулей
Приложение позволяет добавлять и удалять модули. За это отвечает файл manage.py

Посмотреть список установленных модулей: `python .\manage.py list`

Добавить модуль: `python .\manage.py add <filepath>`

Удалить модуль: `python .\manage.py delete <modulename>`

Очистить кэш cookie и access_token: `python .\manage.py clear`
