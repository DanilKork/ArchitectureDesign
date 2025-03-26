# Диаграмма контейнеров и компонентов

![image](https://github.com/user-attachments/assets/2a483d0a-77e4-4d84-8d56-fc758fc80029)
![image](https://github.com/user-attachments/assets/f658507d-20a1-432e-bbf7-337970ee63eb)

# Диаграмма последовательности
![image](https://github.com/user-attachments/assets/ef35a650-b469-493f-8862-f6bad7b88399)

``` @PlantUML
@startuml
title Диаграмма последовательностей: Запуск кластеризации и получение результата

actor Analyst as "Аналитик (Web-клиент)"

participant WebClient as "Web-клиент"
participant Auth as "Auth Controller"
participant ClusterCtrl as "Clustering Controller"
participant Clusterizer as "Сервис кластеризации"
participant Results as "Cluster Results Manager"
participant DBAdapter as "Database Adapter"
database DB as "База данных"

Analyst -> WebClient : Заполняет форму анализа
WebClient -> Auth : Проверка авторизации
Auth --> WebClient : OK

WebClient -> ClusterCtrl : Отправка параметров кластеризации
ClusterCtrl -> Clusterizer : Передача данных и параметров
Clusterizer -> Clusterizer : Выполнение алгоритма кластеризации
Clusterizer --> ClusterCtrl : Результат кластеризации

ClusterCtrl -> Results : Передача результатов
Results -> DBAdapter : Сохранение в БД
DBAdapter -> DB : INSERT кластеров
DB --> DBAdapter : OK

WebClient -> Results : Запрос результата кластеризации
Results -> DBAdapter : SELECT кластеров
DBAdapter -> DB : Чтение результатов
DB --> DBAdapter : Данные кластеров
DBAdapter --> Results : Данные кластеров
Results --> WebClient : Данные кластеров
WebClient -> Analyst : Отображает граф кластеров
@enduml
```

# База данных
![image](https://github.com/user-attachments/assets/24721b33-e7bc-4b2b-af10-80c35dfb726a)

User — хранит данные о пользователях системы (аналитиках), включая email и дату регистрации.

AnalysisTask — представляет задание на кластеризацию. Содержит параметры анализа (в JSON-формате), статус выполнения и ссылку на пользователя, который его создал.

VKObject — содержит импортированные из VK объекты: пользователей, посты, комментарии. Каждый объект имеет тип, ID и текстовое содержимое.

Cluster — описывает один из кластеров, полученных в результате анализа. Привязан к конкретному заданию (AnalysisTask) и содержит метаинформацию, например, размер кластера.

ClusterMember — связывает объекты VK с кластерами. Для каждого участника кластера может быть указана степень вовлеченности или значимости (score).

``` @PlantUML
@startuml
title UML-диаграмма классов: Модель базы данных системы кластеризации

class User {
  +id: UUID
  +email: string
  +passwordHash: string
  +createdAt: datetime
}

class AnalysisTask {
  +id: UUID
  +userId: UUID
  +name: string
  +status: string
  +createdAt: datetime
  +parameters: json
}

class VKObject {
  +id: UUID
  +vkId: string
  +type: string <<enum: 'user', 'post', 'comment'>>
  +content: text
  +createdAt: datetime
}

class Cluster {
  +id: UUID
  +taskId: UUID
  +label: string
  +size: int
}

class ClusterMember {
  +id: UUID
  +clusterId: UUID
  +vkObjectId: UUID
  +score: float
}

' Связи между сущностями
User "1" -- "0..*" AnalysisTask : создает >
AnalysisTask "1" -- "0..*" VKObject : включает >
AnalysisTask "1" -- "0..*" Cluster : порождает >
Cluster "1" -- "0..*" ClusterMember : содержит >
VKObject "1" -- "0..*" ClusterMember : участвует в >

@enduml
```
