Это шаблон для решения **первой части** проектной работы. Структура этого файла повторяет структуру заданий. Заполняйте его по мере работы над решением.

# Задание 1. Анализ и планирование

Чтобы составить документ с описанием текущей архитектуры приложения, можно часть информации взять из описания компании условия задания. Это нормально.

### 1. Описание функциональности монолитного приложения

**Управление отоплением:**

- Пользователи могут удалённо включать/выключать отопление в своих домах.
- Пользователи могут удалённо устанавливать целевую температуру.

**Мониторинг температуры:**

- Пользователи могут просматривать текущую температуру в своих домах через веб-интерфейс.
- Система получает данные о температуре с датчиков, установленных в домах.

### 2. Анализ архитектуры монолитного приложения

- **Язык программирования:** Java
- **База данных:** PostgreSQL
- **Архитектура:** Монолитная, все компоненты системы (обработка запросов, бизнес-логика, работа с данными) находятся в рамках одного приложения.
- **Взаимодействие:** Синхронное, запросы обрабатываются последовательно.
- **Масштабируемость:** Ограничена, так как монолит сложно масштабировать по частям.
- **Развёртывание:** Требует остановки всего приложения.

### 3. Определение доменов и границы контекстов

- **Домен: Управление пользователями.** Отвечает за аутенитификацию/регистрацию пользователей
- **Домен: Управление устройствами.** Непосредственное управление устройствами (в текущем состояни включение/выключение отопления, установка целевой температуры)
- **Домен: Мониторинг устройств.** Получение текущего состояние с датчиков устройств (в текущем состоянии с датчика температуры)

### **4. Проблемы монолитного решения**

У текущего решения нет проблем, если мы говорим о его текущей функциональности и текущей нагрузке. 
Если же рассматривать переход на целевое состояние, то возникнут следующие проблемы:
- **Высокий риск ошибок.** Т.к. для внесения новой функциональности придется править весь код монолита, вероятность возникновения ошибок растет.
- **Длительные циклы разработки и развертывания.** Т.к. придется тестировать все приложение целиком при внесении любых изменений в код.
- **Трудно управлять командой.** Команда разработки уже довольно большая, поэтому управлять разработкой в рамках монолитного приложения будет довольно сложно.
- **Трудно масштабировать отдельные компоненты системы.** Масштабируемость ограничена, так как монолит сложно масштабировать по частям. А он потребуется, т.к. планируется довольно высокая производительность из-за большого кол-ва пользователей и подключенных устройств.

### 5. Визуализация контекста системы — диаграмма С4

```markdown
[Context Diagram](smart-home-monolith\diagrams\context\Context.puml)
```

# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то, как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

```markdown
[Context Diagram](smart-home-monolith\diagrams\container\Container.puml)
```

**Диаграмма компонентов (Components)**

```markdown
[Context Diagram](smart-home-monolith\diagrams\component\Component.puml)
```

**Диаграмма кода (Code)**
```markdown
[Context Diagram](smart-home-monolith\diagrams\code\UserController.puml)
[Context Diagram](smart-home-monolith\diagrams\code\Device.puml)
```
# Задание 3. Разработка ER-диаграммы
```markdown
[Context Diagram](smart-home-monolith\diagrams\entity\ER.puml)
```