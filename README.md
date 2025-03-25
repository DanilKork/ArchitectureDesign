
# Разработка системы для кластеризации сообществ в социальных медиа

Пользователи
Аналитики / исследователи — используют систему для выявления сообществ в соцсетях, анализа их структуры и поведения.

Маркетологи / бренды — изучают выделенные кластеры для целевого маркетинга.

Разработчики / интеграторы — подключают систему к другим аналитическим решениям или BI-инструментам.

Функциональные требования
Веб-клиент для аналитиков
Импорт данных из социальных сетей
Получение постов, лайков, комментариев, связей между пользователями из VK API.
Настройка параметров импорта: по ключевым словам, дате, количеству объектов.

Кластеризация пользователей и сообществ
Запуск алгоритмов кластеризации (например, Louvain, Label Propagation).
Выбор алгоритма и настройка его параметров (глубина, количество кластеров, плотность и т.д.).

Просмотр и визуализация кластеров
Графовое представление структуры кластеров.
Подсветка связей, активных участников, лидеров кластера.

Анализ кластеров
Просмотр участников и постов каждого кластера.
Вывод статистики: размер, вовлеченность, активность.

Экспорт данных
Выгрузка результатов кластеризации в форматах CSV и JSON для последующего анализа.

Серверная часть
Принимает и обрабатывает запросы от веб-клиента

Обеспечивает авторизацию и хранение пользовательских данных

Запрашивает данные через VK API

Выполняет кластеризацию на основе полученных данных

Хранит результаты анализа в базе данных

Поддерживает экспорт данных

Логирует действия пользователей и сбои

Дополнительный контекст
Система предназначена для использования исследовательскими и коммерческими организациями

Пользователи самостоятельно авторизуются через интерфейс, предоставляя доступ к нужным данным

Интерфейс рассчитан на работу в настольных и планшетных браузерах

Используются современные веб-фреймворки: Python (FastAPI/Flask) на сервере, React на клиенте

Визуализация кластеров реализуется с использованием D3.js, Vis.js или WebGL

Кластеризация реализуется на Python с использованием библиотек NetworkX, scikit-learn или PyTorch Geometric

Платформы и технологии
Веб-клиент: современные браузеры (Chrome, Firefox, Safari)

Сервер: Python 3.9+, FastAPI / Flask

База данных: PostgreSQL

Кэширование и промежуточное хранилище: Redis

Визуализация графов: D3.js, Vis.js, возможно WebGL
