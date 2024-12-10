# cb-cloud-service-open-api

Этот репозиторий содержит спецификацию OpenAPI для микросервиса **CB Cloud Service**. Спецификация используется для генерации интерфейсов контроллеров и клиентских библиотек для основных сервисов и связанных приложений, таких как бот.

## Содержание

- [Описание проекта](#описание-проекта)
- [Структура репозитория](#структура-репозитория)
- [CI/CD](#cicd)
- [Использование спецификации](#использование-спецификации)

---

## Описание проекта

Основные задачи репозитория:
- **Спецификация OpenAPI**: Описывает API для микросервиса CB Cloud Service.
- **Генерация кода**: На основе OpenAPI создаются:
    - Интерфейсы контроллеров для основного микросервиса.
    - Клиенты для взаимодействия с API (например, для бота).
- **Сборка и деплой**: Используется Maven для сборки и публикации артефактов.

---

## Структура репозитория

```text
cb-cloud-service-open-api/
│
├── .github/
│   ├── workflows/
│       ├── deploy.yml          # CI/CD Workflow для сборки и деплоя
│
├── templates/
│   ├── ApiClient.mustache      # Шаблон для генерации клиентского кода
│
├── openapi.yaml                # Основной файл спецификации OpenAPI
├── pom.xml                     # Maven файл для сборки
├── .gitignore                  # Исключения для Git
└── README.md                   # Документация проекта
```

## CI/CD

Для автоматизации процессов сборки и публикации используется **GitHub Actions**.

### Workflow: `deploy.yml`

#### Триггер
- **Ручной запуск** через GitHub Actions (`workflow_dispatch`).

#### Шаги

1. **Проверка кода**:  
   GitHub Actions выполняет следующие действия:
    - Настраивает Java среду (версия 17, Temurin).
    - Проверяет, существует ли версия пакета, основанная на текущей ветке.
    - При необходимости удаляет существующую версию пакета.

2. **Сборка**:  
   Maven автоматически обновляет версию пакета и выполняет сборку.

3. **Деплой**:  
   Сборка загружается в **GitHub Packages**.

---

## Использование спецификации

1. **Генерация контроллеров**:  
   OpenAPI спецификация в `openapi.yaml` используется для создания интерфейсов контроллеров для CB Cloud Service.

2. **Артефакты**:  
   После сборки артефакты (интерфейсы и клиенты) публикуются в **GitHub**