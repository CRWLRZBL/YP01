 5.1 Создание таблицы УдаленныеЗаказчики и триггера DELETE

sql
Copy
-- Создание таблицы УдаленныеЗаказчики
CREATE TABLE УдаленныеЗаказчики (
    КодЗаказчика INT,
    -- Все остальные столбцы из таблицы Заказчики
    Имя NVARCHAR(100),
    Фамилия NVARCHAR(100),
    Адрес NVARCHAR(200),
    Телефон NVARCHAR(20),
    Email NVARCHAR(100),
    ДатаУдаления DATETIME DEFAULT GETDATE()
);

-- Создание триггера для логирования удаленных заказчиков
CREATE TRIGGER tr_Заказчики_AfterDelete
ON Заказчики
AFTER DELETE
AS
BEGIN
    INSERT INTO УдаленныеЗаказчики (КодЗаказчика, Имя, Фамилия, Адрес, Телефон, Email)
    SELECT КодЗаказчика, Имя, Фамилия, Адрес, Телефон, Email
    FROM deleted;
END;
5.2 Создание таблицы Logs и триггеров для таблиц Книги и Заказы

sql
Copy
-- Создание таблицы Logs
CREATE TABLE Logs (
    ID INT IDENTITY(1,1) PRIMARY KEY,
    Таблица NVARCHAR(50) NOT NULL,
    Операция NVARCHAR(10) NOT NULL,
    ДатаВремя DATETIME DEFAULT GETDATE(),
    Пользователь NVARCHAR(100) DEFAULT SUSER_SNAME()
);

-- Триггеры для таблицы Книги
CREATE TRIGGER tr_Книги_AfterInsert
ON Книги
AFTER INSERT
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Книги', 'INSERT');
END;

CREATE TRIGGER tr_Книги_AfterUpdate
ON Книги
AFTER UPDATE
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Книги', 'UPDATE');
END;

CREATE TRIGGER tr_Книги_AfterDelete
ON Книги
AFTER DELETE
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Книги', 'DELETE');
END;

-- Триггеры для таблицы Заказы
CREATE TRIGGER tr_Заказы_AfterInsert
ON Заказы
AFTER INSERT
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Заказы', 'INSERT');
END;

CREATE TRIGGER tr_Заказы_AfterUpdate
ON Заказы
AFTER UPDATE
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Заказы', 'UPDATE');
END;

CREATE TRIGGER tr_Заказы_AfterDelete
ON Заказы
AFTER DELETE
AS
BEGIN
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Заказы', 'DELETE');
END;
5.3 Изменение триггера DELETE для таблицы Заказы

sql
Copy
ALTER TRIGGER tr_Заказы_AfterDelete
ON Заказы
AFTER DELETE
AS
BEGIN
    -- Логирование операции
    INSERT INTO Logs (Таблица, Операция)
    VALUES ('Заказы', 'DELETE');
    
    -- Удаление заказчиков без заказов
    DELETE FROM Заказчики
    WHERE КодЗаказчика IN (
        SELECT КодЗаказчика
        FROM Заказчики
        WHERE NOT EXISTS (
            SELECT 1
            FROM Заказы
            WHERE Заказы.КодЗаказчика = Заказчики.КодЗаказчика
        )
    );
END;
5.4 Изменение триггера INSERT для таблицы Состав

sql
Copy
ALTER TRIGGER tr_Состав_AfterInsert
ON Состав
AFTER INSERT
AS
BEGIN
    -- Обновление стоимости заказа
    UPDATE Заказы
    SET Стоимость = (
        SELECT SUM(Книги.Цена * Состав.Количество)
        FROM Состав
        JOIN Книги ON Состав.КодКниги = Книги.КодКниги
        WHERE Состав.КодЗаказа = Заказы.КодЗаказа
    )
    WHERE КодЗаказа IN (SELECT КодЗаказа FROM inserted);
    
    -- Запись стоимости в глобальную переменную
    DECLARE @orderCost DECIMAL(10,2);
    
    SELECT @orderCost = SUM(Книги.Цена * Состав.Количество)
    FROM Состав
    JOIN Книги ON Состав.КодКниги = Книги.КодКниги
    WHERE Состав.КодЗаказа IN (SELECT КодЗаказа FROM inserted);
    
    -- Если нужно сохранить между сеансами, можно использовать временную таблицу
    IF OBJECT_ID('tempdb..#orderCost') IS NOT NULL
        DROP TABLE #orderCost;
    
    CREATE TABLE #orderCost (Cost DECIMAL(10,2));
    INSERT INTO #orderCost VALUES (@orderCost);
END;
