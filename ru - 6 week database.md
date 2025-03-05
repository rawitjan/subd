База данных для управления IT-проектами (Project Management)
**Структура базы данных**

---
employees (Сотрудники)
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,         -- ФИО сотрудника
    email VARCHAR(255) UNIQUE NOT NULL, -- Почта
    position VARCHAR(100),              -- Должность
    department VARCHAR(100),            -- Отдел
    status ENUM('active', 'inactive') NOT NULL  -- Работает или уволен
);
```
**projects (Проекты)**
```sql
CREATE TABLE projects (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,         -- Название проекта
    client VARCHAR(255),                 -- Заказчик проекта
    start_date DATE NOT NULL,            -- Дата начала
    end_date DATE,                        -- Дата завершения
    budget DECIMAL(10,2),                 -- Бюджет проекта
    status ENUM('planned', 'active', 'completed', 'on hold') NOT NULL, -- Статус проекта
    project_manager_id INT,               -- Руководитель проекта
    FOREIGN KEY (project_manager_id) REFERENCES employees(id)
);
```
tasks (Задачи)
```sql
CREATE TABLE tasks (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_id INT NOT NULL,            -- К какому проекту относится
    assignee_id INT,                    -- Назначенный сотрудник
    title VARCHAR(255) NOT NULL,        -- Короткое название задачи
    description TEXT,                    -- Описание задачи
    status ENUM('open', 'in progress', 'completed') NOT NULL,  -- Состояние
    deadline DATE,                        -- Срок выполнения
    FOREIGN KEY (project_id) REFERENCES projects(id),
    FOREIGN KEY (assignee_id) REFERENCES employees(id)
);
```
teams (Команды проекта)
```sql
CREATE TABLE teams (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_id INT NOT NULL,            -- Проект
    employee_id INT NOT NULL,           -- Сотрудник
    role ENUM('developer', 'manager', 'QA', 'analyst', 'designer'),  -- Роль в команде
    FOREIGN KEY (project_id) REFERENCES projects(id),
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```
timesheets (Рабочее время)
```sql
CREATE TABLE timesheets (
    id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT NOT NULL,           -- Сотрудник
    project_id INT NOT NULL,            -- Проект
    date DATE NOT NULL,                 -- Дата работы
    hours_worked DECIMAL(4,2) NOT NULL, -- Часы, потраченные на проект
    FOREIGN KEY (employee_id) REFERENCES employees(id),
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
```
expenses (Затраты по проекту)
```sql
CREATE TABLE expenses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_id INT NOT NULL,            -- Проект
    amount DECIMAL(10,2) NOT NULL,      -- Сумма расхода
    category ENUM('salary', 'software', 'hardware', 'misc', 'travel'),  -- Категория
    description TEXT,                    -- Доп. информация
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
```
meetings (Встречи по проектам)
```sql
CREATE TABLE meetings (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_id INT NOT NULL,            -- Проект
    date_time DATETIME NOT NULL,        -- Дата и время
    topic VARCHAR(255) NOT NULL,        -- Тема встречи
    organizer_id INT NOT NULL,          -- Кто организовал
    FOREIGN KEY (project_id) REFERENCES projects(id),
    FOREIGN KEY (organizer_id) REFERENCES employees(id)
);
```
reports (Отчёты по проектам)
```sql
CREATE TABLE reports (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_id INT NOT NULL,            -- Проект
    author_id INT NOT NULL,             -- Кто составил
    report_date DATE NOT NULL,          -- Дата отчета
    summary TEXT NOT NULL,              -- Краткое описание
    FOREIGN KEY (project_id) REFERENCES projects(id),
    FOREIGN KEY (author_id) REFERENCES employees(id)
);
```
---
### Данные для вставки 
---
```sql
INSERT INTO employees (name, email, position, department, status) VALUES
('Айдос Нурланов', 'aidos@company.kz', 'Руководитель проекта', 'Менеджмент', 'active'),
('Жанель Серикова', 'janel@company.kz', 'Бизнес-аналитик', 'Аналитика', 'active'),
('Ержан Алимов', 'yerzhan@company.kz', 'Разработчик', 'IT', 'active'),
('Алтынгуль Султанова', 'altyn@company.kz', 'Тестировщик', 'IT', 'active'),
('Кайрат Бекенов', 'kairat@company.kz', 'Дизайнер', 'Дизайн', 'active'),
('Самат Рахимов', 'samat@company.kz', 'DevOps-инженер', 'IT', 'active'),
('Гульмира Тлеубаева', 'gulmira@company.kz', 'HR-специалист', 'Кадры', 'active'),
('Мурат Исабаев', 'murat@company.kz', 'Финансовый аналитик', 'Финансы', 'active'),
('Сауле Байгожина', 'saule@company.kz', 'PR-менеджер', 'Маркетинг', 'active'),
('Данияр Оразбаев', 'daniyar@company.kz', 'Менеджер по продажам', 'Продажи', 'active'),
('Бауыржан Тастанов', 'bauyrjan@company.kz', 'Разработчик', 'IT', 'active'),
('Нурия Темирова', 'nuriya@company.kz', 'Маркетолог', 'Маркетинг', 'active'),
('Асет Абилов', 'aset@company.kz', 'Системный администратор', 'IT', 'active'),
('Айнур Ахметова', 'ainur@company.kz', 'UI/UX дизайнер', 'Дизайн', 'active'),
('Ербол Кудайбергенов', 'erbol@company.kz', 'Data Analyst', 'Аналитика', 'active'),
('Мадина Сагиева', 'madina@company.kz', 'Тестировщик', 'IT', 'active'),
('Адильхан Сеитов', 'adilhan@company.kz', 'Руководитель отдела', 'Менеджмент', 'active'),
('Айгерим Жаксылыкова', 'aigerim@company.kz', 'Бизнес-аналитик', 'Аналитика', 'active'),
('Дамир Каримов', 'damir@company.kz', 'Финансовый аналитик', 'Финансы', 'active'),
('Жасулан Ермагамбетов', 'jasulan@company.kz', 'Backend-разработчик', 'IT', 'active');

INSERT INTO projects (name, client, start_date, end_date, budget, status, project_manager_id) VALUES
('CRM-система для Kaspi', 'Kaspi Bank', '2024-01-10', '2024-06-30', 5000000, 'active', 1),
('Автоматизация отчетности для Kcell', 'Kcell', '2024-02-15', '2024-08-20', 7500000, 'active', 18),
('Мобильное приложение для Халык Банка', 'Halyk Bank', '2023-09-01', '2024-04-15', 6000000, 'completed', 1),
('Внедрение BI-аналитики для Air Astana', 'Air Astana', '2024-03-01', '2024-09-01', 9000000, 'active', 15),
('Система учета для Kaspi Gold', 'Kaspi Bank', '2023-07-10', '2024-02-01', 4500000, 'completed', 1),
('Оптимизация логистики для Magnum', 'Magnum', '2024-01-20', '2024-07-01', 7000000, 'active', 18);

INSERT INTO tasks (project_id, assignee_id, title, description, status, deadline) VALUES
(1, 3, 'Настроить базу данных', 'Оптимизация структуры данных', 'in progress', '2024-04-10'),
(1, 5, 'Разработать UI-дизайн', 'Дизайн главного экрана CRM', 'open', '2024-03-25'),
(1, 6, 'Разработать backend', 'Реализация API сервиса', 'in progress', '2024-04-20'),
(1, 11, 'Написать документацию', 'Описание API и структур БД', 'open', '2024-04-15'),
(1, 15, 'Тестирование функционала', 'Функциональное тестирование', 'open', '2024-04-30'),

(2, 6, 'Развернуть сервер', 'Настройка DevOps окружения', 'in progress', '2024-04-15'),
(2, 11, 'Разработать REST API', 'Создание API для отчетов', 'in progress', '2024-05-10'),
(2, 18, 'Бизнес-анализ', 'Определение KPI для отчетов', 'open', '2024-05-05'),
(2, 1, 'Настроить интеграцию', 'Синхронизация с CRM', 'open', '2024-06-01'),

(3, 11, 'Создать backend API', 'Разработка REST API', 'completed', '2023-11-20'),
(3, 5, 'Разработать UI', 'Дизайн мобильного приложения', 'completed', '2023-12-01'),
(3, 3, 'Оптимизировать запросы', 'Ускорение SQL-запросов', 'completed', '2023-12-10'),

(4, 15, 'Анализ данных', 'Разработка BI-дэшбордов', 'in progress', '2024-05-01'),
(4, 18, 'Оптимизация отчетов', 'Уменьшение времени генерации отчетов', 'in progress', '2024-05-10'),
(4, 1, 'Обучение персонала', 'Проведение тренингов по BI', 'open', '2024-06-01'),

(5, 6, 'Разработка архитектуры', 'Создание схемы базы данных', 'completed', '2023-08-01'),
(5, 3, 'Интеграция с банком', 'Настройка API-обмена', 'completed', '2023-09-10'),
(5, 11, 'Автоматизация отчетности', 'Скрипты для отчетов', 'completed', '2023-10-15'),

(6, 6, 'Разработка логистики', 'Оптимизация маршрутов доставки', 'in progress', '2024-04-10'),
(6, 15, 'Сбор требований', 'Анализ текущих процессов', 'in progress', '2024-04-20'),
(6, 18, 'Разработка дэшбордов', 'Создание Power BI отчетов', 'open', '2024-05-01'),
(6, 1, 'Настроить систему уведомлений', 'Push-уведомления в приложении', 'open', '2024-06-10');

INSERT INTO teams (project_id, employee_id, role) VALUES
(1, 1, 'manager'), (1, 3, 'developer'), (1, 5, 'designer'),
(1, 6, 'developer'), (1, 11, 'developer'), (1, 15, 'QA'),

(2, 1, 'manager'), (2, 6, 'developer'), (2, 11, 'developer'),
(2, 18, 'analyst'), (2, 3, 'developer'),

(3, 1, 'manager'), (3, 5, 'designer'), (3, 3, 'developer'),
(3, 11, 'developer'), (3, 15, 'QA'),

(4, 1, 'manager'), (4, 15, 'analyst'), (4, 18, 'analyst'),
(4, 11, 'developer'), (4, 6, 'developer');

INSERT INTO timesheets (employee_id, project_id, date, hours_worked) VALUES
(3, 1, '2024-03-01', 8), (5, 1, '2024-03-02', 6), (6, 2, '2024-03-03', 7),
(11, 3, '2023-11-01', 8), (15, 4, '2024-03-04', 5), (18, 4, '2024-03-05', 6),
(1, 6, '2024-03-06', 7), (6, 6, '2024-03-07', 8), (15, 5, '2024-03-08', 5),
(3, 5, '2024-03-09', 6), (11, 2, '2024-03-10', 7);

INSERT INTO expenses (project_id, amount, category, description) VALUES
(1, 200000, 'software', 'Лицензии на ПО'),
(1, 50000, 'travel', 'Командировка в Астану'),
(1, 30000, 'misc', 'Офисные расходы'),
(1, 120000, 'salary', 'Аутсорс-разработчики'),

(2, 300000, 'hardware', 'Серверное оборудование'),
(2, 150000, 'software', 'Облачные сервисы'),
(2, 50000, 'misc', 'Офисные принадлежности'),
(2, 90000, 'salary', 'Премия аналитикам'),

(3, 150000, 'salary', 'Оплата фрилансеров'),
(3, 70000, 'travel', 'Бизнес-встреча в Алматы'),
(3, 40000, 'software', 'Дополнительные лицензии'),
(3, 60000, 'misc', 'Банкет по окончании проекта'),

(4, 100000, 'misc', 'Прочие расходы'),
(4, 250000, 'software', 'BI-инструменты'),
(4, 80000, 'travel', 'Командировка в Атырау'),
(4, 110000, 'salary', 'Оплата часов аналитиков'),

(5, 250000, 'software', 'Подписка на облачные сервисы'),
(5, 50000, 'travel', 'Отчетная поездка в Шымкент'),
(5, 35000, 'misc', 'Аренда переговорных'),

(6, 400000, 'hardware', 'Закупка серверов'),
(6, 70000, 'travel', 'Конференция по логистике'),
(6, 50000, 'salary', 'Бонус для команды'),
(6, 95000, 'misc', 'Канцелярия и кофе');

INSERT INTO meetings (project_id, date_time, topic, organizer_id) VALUES
(1, '2024-03-10 10:00:00', 'Дизайн-презентация', 5),
(1, '2024-03-15 14:00:00', 'Обсуждение UI-прототипа', 6),
(1, '2024-03-20 11:00:00', 'Финальное ревью', 1),

(2, '2024-03-12 14:00:00', 'Обсуждение API', 6),
(2, '2024-03-18 16:00:00', 'Ревью отчетов', 18),
(2, '2024-03-22 09:00:00', 'Интеграция с CRM', 3),

(3, '2023-11-15 11:00:00', 'Итоговая встреча', 1),
(3, '2023-11-10 15:00:00', 'Тестирование приложения', 15),
(3, '2023-11-05 10:30:00', 'Разбор UX-ошибок', 5),

(4, '2024-04-01 10:00:00', 'Промежуточный отчет', 15),
(4, '2024-04-05 13:00:00', 'Обучение сотрудников', 18),
(4, '2024-04-15 09:30:00', 'Обсуждение KPI', 1),

(5, '2023-09-20 15:00:00', 'Интеграция с банком', 3),
(5, '2023-09-25 10:00:00', 'Анализ угроз безопасности', 6),

(6, '2024-05-05 16:00:00', 'Статус логистики', 1),
(6, '2024-05-10 14:30:00', 'Оптимизация маршрутов', 15),
(6, '2024-05-15 09:00:00', 'Автоматизация складов', 18),
(6, '2024-05-20 11:00:00', 'Обсуждение Power BI', 11);

INSERT INTO reports (project_id, author_id, report_date, summary) VALUES
(1, 1, '2024-03-01', 'Обновление статуса CRM-проекта'),
(1, 6, '2024-03-05', 'UI-дизайн утвержден'),
(1, 11, '2024-03-10', 'Первая версия backend API готова'),
(1, 3, '2024-03-15', 'База данных оптимизирована'),

(2, 18, '2024-03-05', 'Первый этап автоматизации завершен'),
(2, 6, '2024-03-10', 'API интеграция с CRM проведена'),
(2, 1, '2024-03-20', 'Запуск в пилотном режиме'),

(3, 11, '2023-12-01', 'Финальный отчет по мобильному приложению'),
(3, 15, '2023-11-10', 'Тестирование завершено'),
(3, 5, '2023-11-20', 'UX улучшения внесены'),

(4, 15, '2024-04-15', 'Прогресс по BI-аналитике'),
(4, 18, '2024-04-20', 'Обучение пользователей проведено'),
(4, 1, '2024-04-25', 'Система отчетности внедрена'),

(5, 3, '2023-10-05', 'Оптимизация базы данных'),
(5, 6, '2023-10-15', 'Безопасность усилена'),

(6, 1, '2024-04-20', 'Отчет по логистике'),
(6, 6, '2024-04-25', 'Маршруты доставки оптимизированы'),
(6, 15, '2024-05-01', 'Склады переведены на автоматизацию'),
(6, 18, '2024-05-10', 'Аналитика Power BI завершена');
```
---
### Задачи 
---
#### 1. Базовые запросы (простая выборка, фильтрация, сортировка)
1. **Получить всех сотрудников** 
   *отсортируйте по фамилии*
2. **Список всех проектов**
   *ID, название и статус всех проектов, отсортированных по дате начала*
3. **Вывести все открытые или находящиеся в работе задачи с дедлайнами.**
4. **Самые дорогие расходы `top 5`**
#### 2. Группировка и агрегатные функции
1. **Количество сотрудников**
2. **Сумма расходов по проектам**
3. **Посчитать среднюю продолжительность проектов в днях (разница между датами начала и завершения)** [Функция DATADIFF](https://oracleplsql.ru/mysql-function-datediff.html?ysclid=m7usm2iixu269684906)
4. **Количество задач по статусу**
   *Посчитать, сколько задач находится в каждом статусе*
#### 3. Объединение таблиц (JOIN)
1. **Вывести ФИО сотрудников и названия проектов, в которых они участвуют.**
   *Объединить таблицы `employees`, `teams` и `projects`.*
2. **Вывести список задач с именами сотрудников, которые за них отвечают.**
3. **Вывести все расходы с названием проекта, которому они принадлежат.**
4. **Вывести все встречи с названием проекта и именем организатора.**
#### 4. Подзапросы, аналитика, сложные запросы
1. Определить проект, у которого самая большая сумма расходов.
2. Вывести среднее количество рабочих часов на каждый проект.
3. Найти всех сотрудников, у которых нет назначенных задач.
4. Определить ближайшую по дедлайну задачу.
