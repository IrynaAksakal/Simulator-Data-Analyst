#### В данном проекте были выстроены с нуля аналитические процессы в молодом стартапе, объединившем мессенджер и ленту новостей. 
---

Для работы с данными использовался __Python__ и __SQL__.<br>
<br> 
##### Инструменты, которые использовались в работе: 
* база данных __ClickHouse__, в которой хранятся пользовательские события;
* __Redash__ - для написания SQL-запросов и базовой визуализации;
* __Superset__ - полноценная BI-система, для построения графиков и дашбордов;
* __Airflow__ для автоматизации рабочих задач и их запуска в соответствии с расписанием; 
* репозиторий на __GitHub__ для хранения кода.
---

##### Данные об активности пользователей хранятся в таблицах Clickhouse: 
- feed_actions - таблица с событиями просмотров постов.<br> 
Структура: user_id, post_id, action, time, gender, age, country, city, os, source, exp_group.<br> 
- message_actions - таблица с данными об отправке сообщений.<br> 
Структура: user_id, reciever_id, time, source, exp_group, gender, age, country, city, os.<br>
---

##### Реализация проекта: 
• Построила базовую аналитику с помощью дашбордов в Superset поверх таблиц в Clickhouse;<br> 
• Проанализировала продуктовые метрики (в том числе Retention), поведение активной аудитории и причины всплеска и падения активной аудитории;<br> 
• Провела ad hoc анализ причин падения метрики DAU;<br> 
• A/B-тесты: [проверяла корректность работы системы сплитования](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/5.1.AA-test%20(%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0%20%D0%BA%D0%BE%D1%80%D1%80%D0%B5%D0%BA%D1%82%D0%BD%D0%BE%D1%81%D1%82%D0%B8%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B%20%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B%20%D1%81%D0%BF%D0%BB%D0%B8%D1%82%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F).ipynb), [проверяла гипотезы, анализировала результаты АB-теста](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/5.2.AB-test%20(%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7%20%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82%D0%BE%D0%B2%20AB-testa).ipynb) с использованием статистических тестов в Python, проверяла метод анализа тестов над метриками-отношениями [(linearized_likes)](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/5.3.AB-test%20(%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7%20%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2%20%D0%BD%D0%B0%D0%B4%20%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%BA%D0%B0%D0%BC%D0%B8-%D0%BE%D1%82%D0%BD%D0%BE%D1%88%D0%B5%D0%BD%D0%B8%D1%8F%D0%BC%D0%B8%20linearized_likes).ipynb);<br> 
• [Построила ETL-пайплайн](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/6.%D0%9F%D0%BE%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%B8%D0%B5%20ETL-%D0%BF%D0%B0%D0%B9%D0%BF%D0%BB%D0%B0%D0%B9%D0%BD%D0%B0%20(dag%20Airflow).ipynb) с помощью Python и Airflow, в результате чего DAG считает необходимые метрики каждый день за вчера и записывает их в отдельную таблицу в ClickHouse;<br> 
• Автоматизировала отчётность с помощью Airflow: написала скрипты, которыe по расписанию присылают в Telegram отчеты по [ленте](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/7.1.%D0%90%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F%20%D0%BE%D1%82%D1%87%D0%B5%D1%82%D0%BD%D0%BE%D1%81%D1%82%D0%B8%20(Airflow).ipynb) и [по работе приложения в целом](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/7.2.%D0%90%D0%B2%D1%82%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F%20%D0%BE%D1%82%D1%87%D0%B5%D1%82%D0%BD%D0%BE%D1%81%D1%82%D0%B8%20(%D0%B0%D0%B2%D1%82%D0%BE%D0%BE%D1%82%D1%87%D0%B5%D1%82%20%D0%BF%D0%BE%20%D0%BB%D0%B5%D0%BD%D1%82%D0%B5%20%D0%B8%20%D0%BC%D0%B5%D1%81%D1%81%D0%B5%D0%BD%D0%B4%D0%B6%D0%B5%D1%80%D1%83%20%D0%B2%20%D1%82%D0%B5%D0%BB%D0%B5%D0%B3%D1%80%D0%B0%D0%BC%2C%20Airflow).ipynb);<br> 
• Написала [систему алертов на Python](https://github.com/IrynaAksakal/Simulator-Data-Analyst/blob/main/8.1.%D0%9F%D0%BE%D0%B8%D1%81%D0%BA%20%D0%B0%D0%BD%D0%BE%D0%BC%D0%B0%D0%BB%D0%B8%D0%B9%20(%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0%20%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D0%BE%D0%B2)%20(%D1%81%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5%20%D1%82%D0%B5%D0%BA%D1%83%D1%89%D0%B5%D0%B9%2015-%D0%BC%D0%B8%D0%BD%D1%83%D1%82%D0%BA%D0%B8%20%D1%81%2015-%D0%BC%D0%B8%D0%BD%D1%83%D1%82%D0%BA%D0%BE%D0%B9%20%D0%B4%D0%B5%D0%BD%D1%8C%20%D0%BD%D0%B0%D0%B7%D0%B0%D0%B4).ipynb), чтобы отслеживать аномальные отклонения ключевых метрик в realtime.<br> 
<br> 
<br> 

Проект для просмотра сохранен в данном репозитории [Simulator-Data-Analyst](https://github.com/IrynaAksakal/Simulator-Data-Analyst).
