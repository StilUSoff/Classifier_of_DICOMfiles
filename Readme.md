# Проект по обработке DICOM-файлов

Этот проект разработан для работы с медицинскими данными в формате DICOM. Он включает в себя скрипты и утилиты, которые обеспечивают преобразование, сортировку и анализ данных, а также создание и обучение классификатора по определению модальности снимков и частей тела, изображенного на них. 

## Описание исходной модели

- Поддерживаются следующие модальности и части тела: КТ Головного мозга, брюшной полости и грудной клетки, Рентген кисти, брюшной полости и грудной клетки
- Для запуска классификатора введите в консоль "python3 path_to_project/bin/classifier/classifier.py", затем введите путь к папке с изображениями для классификации


## Структура директории

- bin: Здесь находятся основные скрипты для обработки данных.
- checkpoints: Папка для сохранения контрольных точек модели.
- classwork: Рабочие файлы, связанные с проектом.
- env: Виртуальное окружение Python (в случае использования).
- logs: Журналы и логи проекта.
- requirements.txt: Файл с настройками и конфигурациями.

## Инструкции по обучению

1. Предобработка DICOM файлов: Для предобработки DICOM файлов, вы можете использовать dicom_refactor.py. Он конвертирует DICOM файлы в изображения формата JPEG и сохраняет их в подпапке /img. Запустите его следующим образом:

python dicom_refactor.py [путь к директории с DICOM файлами]

2. Преобразование изображений в RGB: Если вы хотите преобразовать изображения в формат RGB, вы можете использовать jpg_rgb_refactor.py. Он выполняет эту операцию и сохраняет обновленные файлы в той же директории. Вы можете запустить его следующим образом:

python jpg_rgb_refactor.py [путь к директории с изображениями] [0 или 1 или 2]

   - 0: Только конвертация в формат JPEG.
   - 1: Только конвертация в формат RGB.
   - 2: Оба шага (JPEG и RGB).

3. Сортировка DICOM файлов: Если вы хотите сортировать DICOM файлы по метаданным (например, Modality или BodyPartExamined), вы можете использовать sort.py. Он сортирует файлы в соответствующие подпапки внутри начальной директории. Запустите его следующим образом:

python sort.py [путь к начальной директории] [y или n]

   - y: Выполняет сортировку всех файлов по модальности и частям тела.
   - n: Сортирует файлы только по модальности.

4. Подготовка данных для обучения модели: Если вы хотите сортировать DICOM файлы по метаданным (например, Modality или BodyPartExamined), вы можете использовать sort.py. Он сортирует файлы в соответствующие подпапки внутри начальной директории. Запустите его следующим образом:

python sort.py [путь к начальной директории] [y или n]

   - y: Выполняет сортировку всех файлов по модальности и частям тела.
   - n: Сортирует файлы только по модальности.

5. Обучение модели: перед тем, как начать обучение модели по распознаванию модальности и частей тела снимков, следует разбить данные на обучающие и тестирующие, используя split_data.py. Этот скрипт создает файлы train.csv и val.csv, содержащие названия изображений, их модальность и части тела. Однако берется эта информация из заранее созданного пользователем .csv файла с расставленными метками. Вы можете запустить его следующим образом:

python split_data.py [путь к начальной директории с изображениями] [путь к рабочей директории, куда будут сохранены файлы train.csv и val.csv] [путь к .csv файлу, содержащего информацию о изображениях]


## Рекомендации по окружению

- Создайте виртуальное окружение Python для изоляции зависимостей проекта
- Установите все необходимые библиотеки, выполнив в терминале команду "py -m pip install -r requirements.txt"
- Однако для создания и полноценной работы приложения на основе этого репозитория вам понадобится JS. В таком случае можете выполнить в терминале следующий перечень команд:
   - npm install -g electron
   - python -m venv venv
   - source venv/bin/activate (or venv\Scripts\activate for Windows)
   - pip install -r requirements.txt
   - npm install electron-builder --save-dev
   - npm install electron electron-reload
   - npx electron-builder build

## Требования

- Python 3.9.xx
- Библиотеки Python, указанные в requirements.txt
- В случае, если обучение модели не происходит с использованием CUDA, однако конфигурация вашей системы соответствует требованиям, советуем использовать команду "pip install torch==1.7.0 -f https://download.pytorch.org/whl/torch_stable.html"
