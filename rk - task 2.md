# **База данных для сервиса аренды автомобилей** 
**Цель**: Управление клиентами, машинами и бронированиями.

Таблицы: 
`locations` — города и адреса, где работает сервис
1. id, 
2. city, 
3. address, 
4. phone

`employees` — персонал на местах
1. id, 
2. name, 
3. position, -- должность
4. salary -- зарплата

`customers` — клиенты
1. id, 
2. name, 
3. phone,
4. email
5. driver_license -- номера прав вождения

`cars` — машины в парке
1. id
2. brand
3. model
4. year -- год выпуска 
5. license_plate -- гос. номер
6. price_per_day -- оплата в день
7. status 

`reservations` — бронирования 
1. id, 
2. car_id, 
3. customer_id, 
4. start_date -- дата начала аренды
5. end_date -- дата возврата авто в парк
6. total_cost 

`insurance` — страховки к бронированиям
1. id
2. reservation_id
3. type
4. cost

`payments` — оплаты бронирований
1. id, 
2. reservation_id, 
3. amount -- оплаченная сумма
4. method -- метод оплаты
5. date

`damage_reports` — поломки по машинам
1. id, 
2. car_id, 
3. description, 
4. repair_cost -- цена ремонта

---
#### Данные
```sql 
-- LOCATIONS
INSERT INTO locations (id, title, address, phone) VALUES
(1, 'Астана', 'Астана центр, улица 1 дом 11', '+7 701 5666692'),
(2, 'Алматы', 'Алматы центр, улица 2 дом 12', '+7 701 4044882'),
(3, 'Шымкент', 'Шымкент центр, улица 3 дом 13', '+7 701 8312936'),
(4, 'Атырау', 'Атырау центр, улица 4 дом 14', '+7 701 9249789'),
(5, 'Караганда', 'Караганда центр, улица 5 дом 15', '+7 701 2530793'),
(6, 'Тараз', 'Тараз центр, улица 6 дом 16', '+7 701 8885465'),
(7, 'Павлодар', 'Павлодар центр, улица 7 дом 17', '+7 701 6837817'),
(8, 'Кокшетау', 'Кокшетау центр, улица 8 дом 18', '+7 701 7850944'),
(9, 'Актобе', 'Актобе центр, улица 9 дом 19', '+7 701 6591986');

-- EMPLOYEES
INSERT INTO employees (id, name, position, salary) VALUES
(1, 'Ерлан Бекенов', 'Администратор', 355671),
(2, 'Нуржан Серик', 'Менеджер по аренде', 222159),
(3, 'Айгуль Муратова', 'Администратор', 287910),
(4, 'Санжар Рахимов', 'Менеджер по работе с клиентами', 309884),
(5, 'Жанар Амангельдиева', 'Администратор', 353692),
(6, 'Данияр Асқар', 'Механик', 393271),
(7, 'Айдана Тлеулина', 'Кассир', 189619),
(8, 'Бекзат Калменов', 'Механик', 203084),
(9, 'Ляззат Жумабекова', 'Администратор', 246164),
(10, 'Мадияр Нуртай', 'Администратор', 210388),
(11, 'Гаухар Сагындык', 'Механик', 314898),
(12, 'Талгат Искаков', 'Менеджер по аренде', 352401),
(13, 'Асель Касымова', 'Кассир', 301104),
(14, 'Арман Жумагалиев', 'Механик', 194209),
(15, 'Меруерт Баймагамбетова', 'Техник', 315905),
(16, 'Нурислам Есимов', 'Администратор', 343219),
(17, 'Айгерим Шаймерденова', 'Механик', 343947),
(18, 'Ерасыл Турлубек', 'Механик', 379226),
(19, 'Назерке Куаныш', 'Менеджер по аренде', 233361),
(20, 'Алия Турсын', 'Администратор', 323974);

-- CUSTOMERS
INSERT INTO customers (id, name, phone, email, driver_license) VALUES
(1, 'Ерлан Бекенов', '+77012000560', 'user2@example.kz', 'B340044'),
(2, 'Нуржан Серик', '+77013783722', 'user3@example.kz', 'B807053'),
(3, 'Айгуль Муратова', '+77016160869', 'user4@example.kz', 'B976566'),
(4, 'Санжар Рахимов', '+77015842082', 'user5@example.kz', 'B703139'),
(5, 'Жанар Амангельдиева', '+77018367772', 'user6@example.kz', 'B715643'),
(6, 'Данияр Асқар', '+77013086308', 'user7@example.kz', 'B121753'),
(7, 'Айдана Тлеулина', '+77018863447', 'user8@example.kz', 'B901909'),
(8, 'Бекзат Калменов', '+77016101803', 'user9@example.kz', 'B804938'),
(9, 'Ляззат Жумабекова', '+77017752972', 'user10@example.kz', 'B961322'),
(10, 'Мадияр Нуртай', '+77015567533', 'user11@example.kz', 'B382602'),
(11, 'Гаухар Сагындык', '+77019396529', 'user12@example.kz', 'B704238'),
(12, 'Талгат Искаков', '+77019284509', 'user13@example.kz', 'B142185'),
(13, 'Асель Касымова', '+77018344375', 'user14@example.kz', 'B900177'),
(14, 'Арман Жумагалиев', '+77012349590', 'user15@example.kz', 'B893005'),
(15, 'Меруерт Баймагамбетова', '+77011668752', 'user16@example.kz', 'B283700'),
(16, 'Нурислам Есимов', '+77018248238', 'user17@example.kz', 'B593355'),
(17, 'Айгерим Шаймерденова', '+77016407658', 'user18@example.kz', 'B644173'),
(18, 'Ерасыл Турлубек', '+77015200476', 'user19@example.kz', 'B783157'),
(19, 'Назерке Куаныш', '+77011433940', 'user20@example.kz', 'B563711'),
(20, 'Алия Турсын', '+77012198058', 'user1@example.kz', 'B195763');

-- CARS
INSERT INTO cars (id, brand, model, year, license_plate, price_per_day, status) VALUES
(1, 'Kia', 'Sportage', 2019, '461ZPG06', 10594, 'rented'),
(2, 'Toyota', 'Camry', 2023, '428CYQ06', 10522, 'rented'),
(3, 'Nissan', 'X-Trail', 2023, '744MLD06', 11122, 'maintenance'),
(4, 'Kia', 'Sportage', 2016, '274YNV06', 12634, 'maintenance'),
(5, 'Nissan', 'X-Trail', 2022, '844ITJ06', 13272, 'available'),
(6, 'Chevrolet', 'Cobalt', 2021, '270TSV06', 14325, 'maintenance'),
(7, 'Kia', 'Sportage', 2022, '919ICV06', 9633, 'maintenance'),
(8, 'Renault', 'Duster', 2015, '746EMZ06', 13546, 'maintenance'),
(9, 'Lada', 'Vesta', 2016, '888JIS06', 15994, 'maintenance'),
(10, 'Toyota', 'Camry', 2016, '262FCZ06', 18383, 'maintenance'),
(11, 'Hyundai', 'Elantra', 2022, '120IBJ06', 15056, 'available'),
(12, 'Chevrolet', 'Cobalt', 2023, '461EPJ06', 19192, 'available'),
(13, 'Renault', 'Duster', 2017, '264RXM06', 12712, 'maintenance'),
(14, 'Kia', 'Sportage', 2016, '435QLG06', 12949, 'available'),
(15, 'Lada', 'Vesta', 2022, '133HSA06', 18784, 'rented'),
(16, 'Nissan', 'X-Trail', 2015, '567BPM06', 12689, 'available'),
(17, 'Volkswagen', 'Polo', 2018, '666SRV06', 18293, 'available'),
(18, 'Toyota', 'Camry', 2019, '703DXI06', 14807, 'available'),
(19, 'Chevrolet', 'Cobalt', 2017, '783NHE06', 15894, 'rented'),
(20, 'Volkswagen', 'Polo', 2016, '407FRR06', 14511, 'maintenance');

-- INSERT INTO reservations
INSERT INTO reservations (id, car_id, customer_id, start_date, end_date, total_cost) VALUES
(1, 10, 15, '2024-06-25', '2024-06-28', 27456),
(2, 4, 3, '2024-09-07', '2024-09-17', 133450),
(3, 5, 9, '2024-05-20', '2024-05-25', 103785),
(4, 5, 14, '2024-03-02', '2024-03-08', 89844),
(5, 12, 8, '2024-11-04', '2024-11-11', 152467),
(6, 20, 5, '2024-04-06', '2024-04-10', 93764),
(7, 20, 10, '2024-06-14', '2024-06-19', 66855),
(8, 13, 18, '2024-01-16', '2024-01-21', 61345),
(9, 20, 16, '2024-04-08', '2024-04-10', 39626),
(10, 9, 18, '2024-02-25', '2024-03-02', 88518),
(11, 20, 17, '2024-09-11', '2024-09-13', 21778),
(12, 9, 2, '2024-02-20', '2024-02-28', 117304),
(13, 20, 17, '2024-02-13', '2024-02-18', 65865),
(14, 1, 17, '2024-09-22', '2024-09-27', 74835),
(15, 20, 11, '2024-10-11', '2024-10-14', 62376),
(16, 12, 14, '2024-06-13', '2024-06-19', 108498),
(17, 12, 13, '2024-11-24', '2024-11-28', 76336);

-- INSERT INTO payments
INSERT INTO payments (id, reservation_id, amount, method, date) VALUES
(1, 1, 92904, 'cash', '2024-06-09'),
(2, 2, 27456, 'card', '2024-06-26'),
(3, 3, 133450, 'cash', '2024-09-08'),
(4, 4, 64716, 'bank_transfer', '2024-06-11'),
(5, 5, 39884, 'bank_transfer', '2024-11-18'),
(6, 6, 70731, 'cash', '2024-03-10'),
(7, 7, 103785, 'card', '2024-05-21'),
(8, 8, 118026, 'cash', '2024-05-18'),
(9, 9, 28928, 'cash', '2024-05-03'),
(10, 10, 145512, 'cash', '2024-08-19'),
(11, 11, 45348, 'card', '2024-03-19'),
(12, 12, 89844, 'cash', '2024-03-03'),
(13, 13, 152467, 'bank_transfer', '2024-11-05'),
(14, 14, 93764, 'card', '2024-04-07'),
(15, 15, 66855, 'cash', '2024-06-15'),
(16, 16, 61345, 'card', '2024-01-17'),
(17, 17, 39626, 'cash', '2024-04-09');

-- INSERT INTO insurance
INSERT INTO insurance (id, reservation_id, type, cost) VALUES
(1, 1, 'premium', 6000),
(2, 2, 'premium', 6000),
(3, 3, 'full', 2000),
(4, 4, 'premium', 4000),
(5, 5, 'full', 6000),
(6, 6, 'premium', 6000),
(7, 7, 'standard', 6000),
(8, 8, 'standard', 6000),
(9, 9, 'premium', 4000),
(10, 10, 'standard', 2000),
(11, 11, 'premium', 6000),
(12, 12, 'full', 2000),
(13, 13, 'full', 6000),
(14, 14, 'standard', 2000),
(15, 15, 'premium', 2000),
(16, 16, 'full', 4000),
(17, 17, 'full', 4000);

-- INSERT INTO damage_reports
INSERT INTO damage_reports (id, car_id, description, repair_cost) VALUES
(1, 18, 'Скол лобового стекла', 30000),
(2, 10, 'Царапина на бампере', 45000),
(3, 16, 'Замена покрышек', 60000),
(4, 20, 'Вмятина двери', 45000),
(5, 15, 'Проблемы с подвеской', 25000),
(6, 17, 'Проблемы с подвеской', 25000),
(7, 20, 'Скол лобового стекла', 30000),
(8, 17, 'Разбитая фара', 60000),
(9, 11, 'Скол лобового стекла', 25000),
(10, 20, 'Вмятина двери', 25000),
(11, 16, 'Царапина на бампере', 25000),
(12, 1, 'Скол лобового стекла', 25000),
(13, 16, 'Замена покрышек', 15000),
(14, 15, 'Проблемы с подвеской', 60000),
(15, 7, 'Разбитая фара', 45000);
```
---
#### Задания
##### 1. Простые SELECT-запросы
1. Показать имена и номера телефонов всех клиентов
2. Получить все заказы (бронирования) с указанием даты начала и конца
3. Вывести все автомобили со статусом "available"
4. Найти все бронирования по клиенту с id = 5
##### 2. Агрегация + GROUP BY
5. Подсчитать количество машин каждого бренда
6. Общая сумма всех платежей
7. Средняя стоимость бронирования
8. Средняя цена аренды по марке автомобиля
9. Количество бронирований по каждому клиенту
##### 3. Чуть сложнее: агрегаты + фильтры + JOIN'ы
10. Вывести бронирования с данными о клиенте (имя, телефон)
11. Показать все платежи с данными о бронировании (даты и клиент)
12. Найти клиентов, арендовавших Chevrolet Cobalt 
13. Найти бронирования длительностью более 5 дней (DATEDIFF?)
14. Вывести количество повреждений и суммарную стоимость ремонта по каждому автомобилю
15. Средняя зарплата по каждой должности
---
```sql
CREATE TABLE locations (
    id INT PRIMARY KEY AUTO_INCREMENT, 
    title VARCHAR(50),
    address VARCHAR(100),
    phone VARCHAR(50)
);

CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    position VARCHAR(50),
    salary int
    );
    
CREATE TABLE customers (
	id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    phone VARCHAR(50),
    email VARCHAR(50),
    driver_license VARCHAR(50)
);

CREATE TABLE cars (
	id INT PRIMARY KEY AUTO_INCREMENT,
    brand VARCHAR(50),
    model VARCHAR(50),
    `year` YEAR, -- год выпуска 
    license_plate VARCHAR(10),
    price_per_day INT,
    `status` ENUM('rented', 'maintenance', 'available')
);

CREATE TABLE reservations (
	id INT PRIMARY KEY AUTO_INCREMENT,
    car_id INT,
    customer_id INT,
    start_date DATE,
    end_date DATE,
    total_cost INT,
    
    FOREIGN KEY (car_id) REFERENCES cars(id),
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

CREATE TABLE insurance (
	id INT PRIMARY KEY AUTO_INCREMENT,
    reservation_id INT,
    type VARCHAR(15),
    cost INT,
    
    FOREIGN KEY (reservation_id) REFERENCES reservations(id)
);

CREATE TABLE payments(
	id INT PRIMARY KEY AUTO_INCREMENT,
    reservation_id INT,
	amount INT,
    method ENUM('card','cash','bank_transfer'),
    `date` DATE,
    
	FOREIGN KEY (reservation_id) REFERENCES reservations(id)
);

CREATE TABLE damage_reports  (
	id INT PRIMARY KEY AUTO_INCREMENT,
    car_id INT,
    description VARCHAR(100),
    repair_cost INT,
    
    FOREIGN KEY (car_id) REFERENCES cars(id)
);

-- github.com/rawitjan/subd -> rk - task 2
```

---
```php
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
  </body>
</html>
```
