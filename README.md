Библиотека смартаппов для Сбер Салюта
======
Смартаппы для экосистемы СБЕРа. Разработаны на базе фреймворка [smart_app_framework](#https://github.com/sberdevices/smart_app_framework) https://github.com/sberdevices/smart_app_framework на Python

#### Боты работают с версиями Python 3.6-3.7 <br>С другими версиями боты не работают!


## Настройка для использования на личном ПК под управлением  Windows
How to on Windows:

1. Download as zip and unzip it somewhere
2. Create your virtual environment and activate it
3. Go to `smart_app_framework/setup.py` and add `encoding='utf-8'` to string 5 in `open` function<br>
    How it will look like:<br>
    `with open("README.md", "r") as file:` => `with open("README.md", "r", encoding='utf-8') as file:`
4. Start installing using this command: <br>
    `python -m pip install path_to_your_unzip_smart_app_framework`
5. Relax for a few minutes while pip will do his job
6. After a few minutes you may get error like this: `error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.micro
soft.com/visual-cpp-build-tools/`
    1. If you are so lucky, go to [MS site](#https://visualstudio.microsoft.com/visual-cpp-build-tools/) https://visualstudio.microsoft.com/visual-cpp-build-tools/  and download installer.
    2. Start it, choose `C++ build tools` and a path for files, because it is about **6,4-8.0 GB** (LOL)
    3. Relax while it will be downloading
7. Start your project

<br><br>
## Проблемы при установке фреймворка

При установке фреймворка нет папки `template` в `d:\ProgramData\Anaconda3\envs\NLPF\lib\site-packages\smart_kit\template`<br>
Удаление и переустановка фреймворка не помогли - папки все еще нет<br>

Okay, похоже на вызов =)<br>
Добавим папку `template` вручную из исходников в `\Anaconda3\envs\NLPF\Lib\site-packages\smart_kit`<br>

Создаем апп командой `python -m smart_kit create_app test`<br>
python test/manage.py local_testing<br>

Ошибка: <br>
    `Using TensorFlow backend.
    FileRepository.load  template_settings repo loading completed.
    OSAdapter run failed with [Errno 2] No such file or directory: 'C:\\Users\\misha\\Desktop\\Python Projects\\Sberbank_Bot\\test\\./static\\./configs\\kafka_config.yml'.
    `
 
В папке `<YOUR_APP_NAME>\static\configs` только `logging_config.yml` и `template_config.yml`<br>
Отсутствуют 2 файла (их нет и в исходниках): `kafka_config.yml` и `ceph_config.yml` <br>

Создали их и добавили `---` в каждый из них <br>

Снова ошибка: `ValueError: Unable to configure handler 'file_app_handler'` <br>

Проблема идет из файла `logging_config.yml` <br>

Меняем путь в `file_app_handler.filename` с `/tmp/app.log` на `app.log` (прям на одном уровне с папкой смартаппа, для тестов самое то) <br>
Меняем путь в `file_handler.filename` с `/tmp/system.log` на `system.log` (прям на одном уровне с папкой смартаппа, для тестов самое то) <br>

Решение - создавать папки с логами вручную, сейчас они почему-то не создавались (?) <br>

Вот и все, после всего этого я смог запустить смартапп на виндовсе <br>
