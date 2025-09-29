# insurance-dbms
create DATABASE NEWDATABASE ;
USE NEWDATABASE;
CREATE TABLE Driver (
    driver_id INT PRIMARY KEY,
    name VARCHAR(50),
    address VARCHAR(100),
    phone VARCHAR(15)
); 

CREATE TABLE Vehicle (
    vehicle_id INT PRIMARY KEY,
    license_plate VARCHAR(20),
    model VARCHAR(50),
    year INT
);


CREATE TABLE Accident (
    accident_id INT PRIMARY KEY,
    date DATE,
    location VARCHAR(100)
);


CREATE TABLE Owns (
    driver_id INT,
    vehicle_id INT,
    PRIMARY KEY(driver_id, vehicle_id),
    FOREIGN KEY(driver_id) REFERENCES Driver(driver_id),
    FOREIGN KEY(vehicle_id) REFERENCES Vehicle(vehicle_id)
);


CREATE TABLE Participated (
    accident_id INT,
    vehicle_id INT,
    driver_id INT,
    damage_amount DECIMAL(10,2),
    PRIMARY KEY(accident_id, vehicle_id),
    FOREIGN KEY(accident_id) REFERENCES Accident(accident_id),
    FOREIGN KEY(vehicle_id) REFERENCES Vehicle(vehicle_id),
    FOREIGN KEY(driver_id) REFERENCES Driver(driver_id)
);

INSERT INTO Driver VALUES
(1, 'Rajesh Kumar', 'Delhi', '9876543210'),
(2, 'Anita Sharma', 'Mumbai', '8765432109'),
(3, 'Vikram Singh', 'Bangalore', '7654321098'),
(4, 'Sunita Rao', 'Chennai', '6543210987'),
(5, 'Amit Patel', 'Ahmedabad', '5432109876');


INSERT INTO Vehicle VALUES
(101, 'DL3CAF1234', 'Hyundai i20', 2018),
(102, 'MH12DE5678', 'Maruti Swift', 2019),
(103, 'KA05MG9876', 'Honda City', 2020),
(104, 'TN10KL4567', 'Ford EcoSport', 2017),
(105, 'GJ01AB1234', 'Toyota Innova', 2021);


INSERT INTO Owns VALUES
(1, 101),
(2, 102),
(3, 103),
(4, 104),
(5, 105);


INSERT INTO Accident VALUES
(1001, '2023-01-15', 'Delhi Ring Road'),
(1002, '2023-03-22', 'Bandra-Kurla Complex'),
(1003, '2023-06-05', 'Electronic City, Bangalore'),
(1004, '2023-07-19', 'Mount Road, Chennai'),
(1005, '2023-09-10', 'SG Highway, Ahmedabad');


INSERT INTO Participated VALUES
(1001, 101, 1, 30000),
(1002, 102, 2, 15000),
(1003, 103, 3, 25000),
(1004, 104, 4, 5000),
(1005, 105, 5, 45000);

SELECT DISTINCT driver_id
FROM Participated
WHERE damage_amount >= 25000;

SELECT date, location
FROM Accident;

SHOW databases;
SELECT * FROM Driver;
SELECT * FROM Vehicle;
SELECT * FROM Accident;
SELECT * FROM Participated;
SELECT *FROM PARTICIPATED ORDER BY DAMAGE_AMOUNT DESC;
SELECT *FROM PARTICIPATED ORDER BY DAMAGE_AMOUNT DESC;
SELECT AVG(DAMAGE_AMOUNT) AS AVG_DAMAGE FROM PARTICIPATED;
DELETE FROM PARTICIPATED WHERE DAMAGE_AMOUNT < (SELECT AVG(DAMAGE_AMOUNT) FROM PARTICIPATED);
SELECT A.NAME FROM PERSON A, PARTICIPATED B WHERE A.DRIVER_ID = B.DRIVER_ID AND B.DAMAGE_AMOUNT > (SELECT AVG(DAMAGE_AMOUNT) FROM PARTICIPATED);
SELECT MAX(DAMAGE_AMOUNT) AS MAX_DAMAGE FROM PARTICIPATED;
