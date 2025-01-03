# FileBasedAIChat

## Описание
FileBasedAIChat — это инструмент, разработанный для облегчения диалога с передовыми языковыми моделями, такими как GPT-3.5-turbo, GPT-4, а также с моделями Claude от Anthropic. Основная особенность проекта заключается в ведении диалога через файлы, что позволяет пользователям полностью контролировать контекст, редактировать свои вводы и получать ответы от модели. Это предоставляет возможность не только адаптировать ответы AI, но и задавать индивидуальные шаблоны поведения для каждого диалога. Теперь проект также поддерживает работу с изображениями в диалогах с моделями Anthropic.

## Установка
Перед началом работы с FileBasedAIChat рекомендуется настроить виртуальное окружение:

```bash
python3.10 -m venv venv
source venv/bin/activate
```

После активации виртуального окружения установите необходимые зависимости:

```bash
pip install -r requirements.txt
```

Перед началом использования скопируйте и переименуйте все `.example` файлы в директории `configs/` и `dialogs/`, удалив суффикс `.example`. Заполните файл `models.json` своими данными API ключей для доступа к моделям AI.

## Использование
Для запуска FileBasedAIChat используйте команду:

```bash
python fbac.py <путь к файлу диалога>
```

Если указанный файл диалога не существует, он будет автоматически создан с настройками по умолчанию. Если файл уже создан, программа обработает существующий диалог.

### Работа с текстом
Внутри файла диалога вы можете задать желаемую модель и шаблон поведения. Пользователь создаёт файл диалога, вводит свой запрос после маркера `human`, запускает обработку командой и получает ответ от ai после маркера `ai`. Затем программа вновь добавляет маркер `human`, и пользователь может продолжить диалог. Этот процесс повторяется до тех пор, пока пользователь не решит его завершить.

### Работа с изображениями
Теперь в диалогах с моделями Anthropic вы можете включать изображения в свои запросы. Для этого используйте специальную конструкцию `img('путь_к_изображению')` в тексте вашего сообщения. Например:

```
modell: claude-3-5-sonnet-20240620
behaviorr: test_kitty

H: Что ты видишь на этом изображении? img('/path/to/image.jpg') Опиши его подробно.
ai: [Ответ модели с описанием изображения]

H: А теперь сравни это изображение img('/path/to/image1.jpg') с этим img('/path/to/image2.jpg'). В чем их основные отличия?
ai: [Ответ модели с сравнением двух изображений]
```

Вы можете использовать несколько изображений в одном сообщении, и они будут корректно обработаны и отправлены в API Anthropic.

## Конфигурационные файлы
Конфигурационные файлы играют ключевую роль в настройке FileBasedaiChat:

- `models.json`: содержит данные о доступных моделях ai, включая API ключи и базовые URL для доступа к сервисам.
- `default_dialog_config.json`: определяет стандартные настройки диалога, такие как используемая модель и шаблон поведения.
- `behavior_templates.json`: включает шаблоны поведения, которые модифицируют ответы ai в соответствии с заданным контекстом и стилем.

Эти файлы позволяют настроить поведение ai, выбрать подходящую модель и управлять параметрами диалога, обеспечивая гибкость и расширяемость взаимодействия с языковыми моделями.

## Поддерживаемые модели
FileBasedaiChat поддерживает следующие модели:

- **Openai**: GPT-3.5-turbo, GPT-3.5-turbo-16k, GPT-4, GPT-4o, o1, o1-preview.
- **Anthropic**: Claude 3 Opus, Claude 3 Sonnet, Claude 3 Haiku (с поддержкой изображений).

### Модели с GPT-like API
FileBasedaiChat также поддерживает взаимодействие с моделями, использующими GPT-like API, такими как LLaMA, Mistral, Mixtral, когда они запущены через проекты, такие как llama-api.

## Примечание
Обратите внимание, что работа с изображениями в настоящее время поддерживается только для моделей Anthropic. При использовании других моделей изображения будут игнорироваться.