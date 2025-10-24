# Project_template

Это шаблон для решения проектной работы. Структура этого файла повторяет структуру заданий. Заполняйте его по мере работы над решением.

# Задание 1. Анализ и планирование

Чтобы составить документ с описанием текущей архитектуры приложения, можно часть информации взять из описания компании и условия задания. Это нормально.

### 1. Описание функциональности монолитного приложения

**Управление отоплением:**

- Пользователи могут включать/отключать отопление в доме
- Пользователи могут задавать температуру в доме
- Система поддерживает управление датчиками(создание, обновление, удаление,
  получение информации о всех датчиках и получение информации конкретного датчика по id)
- Система поддерживает обновление значений датчиков(температуру и статус)

**Мониторинг температуры:**

- Пользователи могут получать данные о температуре в доме
- Система поддерживает получение информации о температуре в доме по id датчик

### 2. Анализ архитектуры монолитного приложения

Язык программирования: Go (основная бизнес-логика), REST API для внешних запросов.

База данных: PostgreSQL (одна таблица sensors для датчиков).

Взаимодействие компонентов: SensorsHandler обрабатывает HTTP-запросы и вызывает сервисный слой (TemperatureService и RepositoryLayer).

TemperatureService получает данные о температуре через REST-запросы к Python-сервису TemperatureApp.

RepositoryLayer выполняет CRUD-операции с PostgreSQL.

Особенности:
Монолит объединяет управление сенсорами и логику работы с температурой.
Взаимодействие с внешним Python-сервисом выполняется синхронно через REST.

### 3. Определение доменов и границы контекстов

Sensors (Сенсоры)
Описание: Управление сенсорами, CRUD операции, получение текущего состояния.
Компоненты:
SensorsHandler — HTTP обработчик запросов к сенсорам
RepositoryLayer — слой доступа к базе данных (технический компонент, поддержка домена)
Database — хранение информации о сенсорах (инфраструктура)

Temperature (Температура / Мониторинг)
Описание: Получение актуальных данных о температуре с устройств.
Компоненты:
TemperatureService — бизнес-логика по обработке температурных данных

### **4. Проблемы монолитного решения**

Масштабирование: нельзя масштабировать отдельно обработку сенсоров или температурные вычисления.
Надёжность: сбой одного сервиса сломает всю систему.

### 5. Визуализация контекста системы — диаграмма С4

Добавьте сюда диаграмму контекста в модели C4.

Чтобы добавить ссылку в файл Readme.md, нужно использовать синтаксис Markdown. Это делают так:

Монолит:
```markdown
[Диаграмма Контекста](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/AsIs/Context.puml)
```
```markdown
[Диаграмма Контейнеров](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/AsIs/Container.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/AsIs/Component.puml)
```
```markdown
[Диаграмма Кода](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/AsIs/Code.puml)
```
# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то, как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

```markdown
[Диаграмма Контейнеров](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/warmhouse/docs/diagrams/ToBe/Container.puml)
```

**Диаграмма компонентов (Components)**

```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-api-gateway.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-auth-service.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-core-service.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-heating-service.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-lighting-service.puml)
```
```markdown
[Диаграмма Компонентов](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Component-signalling-service.puml)
```

**Диаграмма кода (Code)**

```markdown
[Диаграмма Кода](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/Code-signaling-service.puml)
```

# Задание 3. Разработка ER-диаграммы

```markdown
[ER-диаграмма](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/docs/diagrams/ToBe/ER.puml)
```

# Задание 4. Создание и документирование API

### 1. Тип API

Укажите, какой тип API вы будете использовать для взаимодействия микросервисов. Объясните своё решение.

Будет использоваться синхронный API на основе протокола HTTP. 
Выбран так как соответствует нефункциональным требованиям.

### 2. Документация API

Здесь приложите ссылки на документацию API для микросервисов, которые вы спроектировали в первой части проектной работы. Для документирования используйте Swagger/OpenAPI или AsyncAPI.

Описание OpenAPI:
```markdown
[Cервис аутентификации](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/apps/api/openapi-auth-service.yaml)
```
```markdown
[Сервис API Gateway](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/apps/api/openapi-gateway-service.yaml)
```
```markdown
[Сервис Управления отоплением](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/apps/api/openapi-heating-service.yaml)
```
```markdown
[Сервис Управления освещением](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/apps/api/openapi-lighting-service.yaml)
```
```markdown
[Сore сервис умного дома](https://github.com/AlexeyPrutik/yandexarch-architecture-warmhouse/blob/main/apps/api/openapi-core-service.yaml)
```
# Задание 5. Работа с docker и docker-compose

Перейдите в apps.

Там находится приложение-монолит для работы с датчиками температуры. В README.md описано как запустить решение.

Вам нужно:

1) сделать простое приложение temperature-api на любом удобном для вас языке программирования, которое при запросе /temperature?location= будет отдавать рандомное значение температуры.

Locations - название комнаты, sensorId - идентификатор названия комнаты

```
	// If no location is provided, use a default based on sensor ID
	if location == "" {
		switch sensorID {
		case "1":
			location = "Living Room"
		case "2":
			location = "Bedroom"
		case "3":
			location = "Kitchen"
		default:
			location = "Unknown"
		}
	}

	// If no sensor ID is provided, generate one based on location
	if sensorID == "" {
		switch location {
		case "Living Room":
			sensorID = "1"
		case "Bedroom":
			sensorID = "2"
		case "Kitchen":
			sensorID = "3"
		default:
			sensorID = "0"
		}
	}
```

2) Приложение следует упаковать в Docker и добавить в docker-compose. Порт по умолчанию должен быть 8081

3) Кроме того для smart_home приложения требуется база данных - добавьте в docker-compose файл настройки для запуска postgres с указанием скрипта инициализации ./smart_home/init.sql

Для проверки можно использовать Postman коллекцию smarthome-api.postman_collection.json и вызвать:

- Create Sensor
- Get All Sensors

Должно при каждом вызове отображаться разное значение температуры

Ревьюер будет проверять точно так же.


