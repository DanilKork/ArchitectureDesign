![image](https://github.com/user-attachments/assets/1a484f58-a5ed-48d6-a050-92f05e1ede32)
```@PlantUML
@startuml
title Диаграмма системного контекста: Система кластеризации сообществ социальных медиа
left to right direction

actor "Аналитик данных / Исследователь" as Analyst
actor "Маркетолог / Бренд" as Marketer
actor "Программист / Инженер" as Developer
actor "VK API / Социальные сети" as VKAPI
actor "BI-инструменты\n(Excel, Power BI)" as BI

rectangle "Система кластеризации\nсообществ социальных медиа" as System {
}

' Взаимодействие с пользователями
Analyst --> System : Импорт данных\nНастройка параметров\nЗапуск кластеризации\nПросмотр результатов
Marketer --> System : Получение информации\nо кластерах для анализа
Developer --> System : Интеграция и поддержка

' Внешние системы
System --> VKAPI : Запрос данных\n(посты, комментарии,\nсвязи пользователей)
System --> BI : Экспорт результатов\nв формате CSV / JSON
@enduml
```
# Диаграмма контейнеров

![image](https://github.com/user-attachments/assets/947e70a4-a556-42e3-b523-676e32b238e6)

```@PlantUML
@startuml
title Диаграмма контейнеров: Система кластеризации сообществ социальных медиа

skinparam rectangle {
  BackgroundColor #F9F9F9
  BorderColor Black
}
skinparam componentStyle rectangle
skinparam defaultTextAlignment center
left to right direction

actor "Аналитики / Исследователи" as Analyst
actor "Маркетологи / Бренды" as Marketer
actor "VK API / Социальные сети" as VK
actor "BI-инструменты\n(Excel, Power BI)" as BI

package "Система кластеризации сообществ\nв социальных медиа [System]" {
    
    rectangle "Web-клиент аналитика\n[React / TypeScript]" as WebClient
    rectangle "Backend API\n[Python / FastAPI]" as Backend
    rectangle "Сервис кластеризации\n[Python / NetworkX]" as Clusterizer
    database "База данных\n[PostgreSQL / Neo4j]" as Database
}

' Взаимодействие пользователей
Analyst --> WebClient : Управляет анализом\nПросматривает результаты
Marketer --> WebClient : Просматривает отчёты\n(через экспортированные файлы)

' Взаимодействие между контейнерами
WebClient --> Backend : HTTP (REST API)\nЗапросы на импорт/кластеризацию
Backend --> VK : Получение данных\nпо токену
Backend --> Clusterizer : Задания на кластеризацию
Clusterizer --> Database : Сохраняет результаты
Backend --> Database : Чтение / запись
Backend --> WebClient : Отправка результатов
Backend --> BI : Экспорт CSV/JSON
@enduml
```


# Диаграмма компонентов для одного контейнера
![image](https://github.com/user-attachments/assets/befab524-5cb1-492b-8355-f7a3e51e4faf)

```@PlantUML
@startuml
title Диаграмма компонентов контейнера: Backend API [Python / FastAPI]

package "Контейнер: Backend API\n[Python / FastAPI]" {
    
    [Auth Controller] as Auth
    [Data Import Service] as Import
    [Clustering Controller] as ClusterCtrl
    [Cluster Results Manager] as Results
    [Export Module] as Export
    [Database Adapter] as DBAdapter
}

actor "Web-клиент" as WebClient
actor "VK API" as VK
actor "Сервис кластеризации" as Clusterizer
actor "База данных" as DB
actor "BI-инструменты" as BI

WebClient --> Auth : Авторизация\nOAuth 2.0
WebClient --> Import : Настройка импорта\nданных
WebClient --> ClusterCtrl : Запуск кластеризации
WebClient --> Results : Получение результатов

Auth --> VK : Получение токена
Import --> VK : Импорт данных
ClusterCtrl --> Clusterizer : Отправка задания
Results --> DBAdapter : Сохранение/получение кластеров
Export --> BI : Экспорт CSV / JSON
Export --> DBAdapter : Чтение данных
DBAdapter --> DB : SQL / Graph-запросы

@enduml
```

#
