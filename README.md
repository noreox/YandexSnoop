# YandexSnoop Bot

Этот мини-проект позволяет автоматически загружать файлы, отправленные в Telegram-бота, на ваш аккаунт Yandex.Disk, очищать корзину, и искать файлы на Yandex.Disk по запросу пользователя. Файлы будут загружаться в автоматически создаваемые папки по типу 'August_2024'. В созданной папке по времени будет подсортировка по типу загружемого файла (Фото, Видео, Аудио, и прочие файлы). Функционал бота будет постепенно обновляться и расширяться.

## Установка и настройка

### Шаг 1: Создание Telegram-бота

1. Откройте Telegram и найдите @BotFather.
2. Создайте по инструкции нового бота и получите API-токен вашего бота.

### Шаг 2: Создание приложения на Yandex

1. Перейдите на [Yandex OAuth](https://oauth.yandex.ru/).
2. Создайте новое приложение.
3. Выберите пункт "Веб-сервисы".
4. В качестве "Redirect URL" укажите: `https://oauth.yandex.ru/verification_code`.
5. Затем предоставьте приложению следующие права для управления Yandex.Disk:
    - Доступ к папке приложения на Диске: `cloud_api:disk.app_folder`
    - Чтение всего Диска: `cloud_api:disk.read`
    - Запись в любом месте на Диске: `cloud_api:disk.write`
    - Доступ к информации о Диске: `cloud_api:disk.info`
6. Получите токен:
    - Скопируйте ClientID вашего созданного приложения и получите токен, перейдя по следующей ссылке, заменив `ВАШ_CLIENTID` в ней:
      `https://oauth.yandex.ru/authorize?response_type=token&client_id=ВАШ_CLIENTID`.

### Шаг 3: Установка Python

Для пользователей Linux данный шаг можно пропустить, т.к в большинстве современных дистрибутивов он установлен по умолчанию.

Если вы пользователь Windows, то можете легко установить через [официальный сайт](https://www.python.org/downloads/).
Перед установкой обязательно поставьте 'Add Python3.x to PATH'.

### Шаг 4: Клонирование репозитория

Клонируйте этот репозиторий на вашу систему:

Для пользователей Windows:
1. Установите [Git для Windows](https://gitforwindows.org/).
2. Откройте Git Bash и выполните команды ниже:
    ```bash
    # По желанию перейдите в нужную директорию перед клонированием:
    # Пример: cd Документы
    git clone https://github.com/Noreox/YandexSnoop.git
    cd YandexSnoop
    ```

Для пользователей Linux (Ubuntu):
1. Установите необходимые пакеты:
    ```bash
    sudo apt-get install git python3.x-venv # Где x - последняя доступная версия Python в вашей системе, например python3.8 и выше.
    ```
2. Клонируйте репозиторий:
    ```bash
    # По желанию перейдите в нужную директорию перед клонированием:
    # Пример: cd Документы/
    git clone https://github.com/Noreox/YandexSnoop.git
    cd YandexSnoop
    ```

### Шаг 5: Настройка виртуального окружения

1. Создайте и активируйте виртуальное окружение:
    ```bash
    python -m venv myenv

    # В некоторых случаях переменная PATH может быть установлена по другому, в таком случае пробуйте:
    python3 -m venv venv
    ```
2. Активируйте созданное окружение:
    - На Linux:
        ```bash
        source myenv/bin/activate
        ```
    - На Windows:
        ```bash
        .\myenv\Scripts\activate
        ```

### Шаг 6: Установка зависимостей

Установите необходимые зависимости, находясь в виртуальном окружении:
```bash
pip install aiogram yadisk requests python-dotenv
```

### Шаг 7: Настройка переменных
Создайте файл `.env` в вашей директории с программой и добавьте в него следующее содержимое:
```bash
BOT_API_TOKEN=YOUR_BOT_API_TOKEN # Поменяйте на токен вашего бота Telegram
YANDEX_DISK_TOKEN=YOUR_YANDEX_DISK_TOKEN # Поменяйте на токен вашего приложения Yandex
CHAT_ID=YOUR_CHAT_ID # См. шаг далее
```

### Шаг 8: Получение Chat ID
1. Отредактируйте файл `get_chatid.py`, заменив `YOUR_BOT_API_TOKEN` на токен вашего бота Telegram.
2. Отправьте сообщение вашему боту.
Запустите скрипт `get_chatid.py`
```bash
python get_chatid.py
```
3. Скопируйте полученный `chat_id` и добавьте его в `.env` файл в переменную CHAT_ID.

### Шаг 9: Запуск бота
Теперь почти всё готово, осталось запустить бота:
```bash
python YandexSnoop.py
```
Теперь ваш бот готов к работе. Отправляйте файлы боту в Telegram, и они будут автоматически загружены на ваш Yandex.Disk.

## License

© 2024 noreox

This project is licensed under the Apache License, Version 2.0. You may not use this file except in compliance with the License. You may obtain a copy of the License at:

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
