# DB_Final_project

---- Car Dealer 데이터 베이스 생성 SQL문 ------

-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

---

-- Schema Car_Dealer

---

---

-- Schema Car_Dealer

---

CREATE SCHEMA IF NOT EXISTS `Car_Dealer` DEFAULT CHARACTER SET utf8 ;
USE `Car_Dealer` ;

---

-- Table `Car_Dealer`.`Salesperson`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`Salesperson` (
`Sid` VARCHAR(10) NOT NULL,
`Password` VARCHAR(10) NULL,
`Name` VARCHAR(10) NULL,
PRIMARY KEY (`Sid`))
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`CUSTOMER`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`CUSTOMER` (
`Ssn` VARCHAR(10) NOT NULL,
`Customer_level` VARCHAR(10) NULL,
`Name` VARCHAR(10) NULL,
`Password` VARCHAR(10) NULL,
`Address` VARCHAR(45) NULL,
`Reserve_count` INT NULL,
PRIMARY KEY (`Ssn`))
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`Vehicle`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`Vehicle` (
`Vin` VARCHAR(20) NOT NULL,
`Fuel_efficiency` FLOAT(10) NULL,
`Brand` VARCHAR(20) NULL,
`Price` INT(10) NULL,
`Sid` VARCHAR(10) NULL,
`Ssn` VARCHAR(10) NULL,
`Reservate_Date` DATE NULL,
PRIMARY KEY (`Vin`),
UNIQUE INDEX `Vin_UNIQUE` (`Vin` ASC) VISIBLE,
INDEX `fk_Vehicle_Salesperson1_idx` (`Sid` ASC) VISIBLE,
INDEX `fk_Vehicle_CUSTOMER1_idx` (`Ssn` ASC) VISIBLE,
CONSTRAINT `fk_Vehicle_Salesperson1`
FOREIGN KEY (`Sid`)
REFERENCES `Car_Dealer`.`Salesperson` (`Sid`)
ON DELETE NO ACTION
ON UPDATE NO ACTION,
CONSTRAINT `fk_Vehicle_CUSTOMER1`
FOREIGN KEY (`Ssn`)
REFERENCES `Car_Dealer`.`CUSTOMER` (`Ssn`)
ON DELETE NO ACTION
ON UPDATE NO ACTION)
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`CAR`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`CAR` (
`Num_seats` VARCHAR(5) NULL,
`Engine_size` VARCHAR(5) NULL,
`Vin` VARCHAR(20) NOT NULL,
PRIMARY KEY (`Vin`),
CONSTRAINT `fk_CAR_Vehicle`
FOREIGN KEY (`Vin`)
REFERENCES `Car_Dealer`.`Vehicle` (`Vin`)
ON DELETE NO ACTION
ON UPDATE NO ACTION)
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`TRUCK`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`TRUCK` (
`Tonnage` INT(5) NULL,
`No_axles` INT(3) NULL,
`Vin` VARCHAR(20) NOT NULL,
PRIMARY KEY (`Vin`),
CONSTRAINT `fk_TRUCK_Vehicle1`
FOREIGN KEY (`Vin`)
REFERENCES `Car_Dealer`.`Vehicle` (`Vin`)
ON DELETE NO ACTION
ON UPDATE NO ACTION)
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`SUV`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`SUV` (
`Size` VARCHAR(5) NULL,
`Num_seats` VARCHAR(5) NULL,
`Vin` VARCHAR(20) NOT NULL,
PRIMARY KEY (`Vin`),
CONSTRAINT `fk_SUV_Vehicle1`
FOREIGN KEY (`Vin`)
REFERENCES `Car_Dealer`.`Vehicle` (`Vin`)
ON DELETE NO ACTION
ON UPDATE NO ACTION)
ENGINE = InnoDB;

---

-- Table `Car_Dealer`.`Motorcycle`

---

CREATE TABLE IF NOT EXISTS `Car_Dealer`.`Motorcycle` (
`Level` VARCHAR(10) NULL,
`Vin` VARCHAR(20) NOT NULL,
PRIMARY KEY (`Vin`),
CONSTRAINT `fk_Motorcycle_Vehicle1`
FOREIGN KEY (`Vin`)
REFERENCES `Car_Dealer`.`Vehicle` (`Vin`)
ON DELETE NO ACTION
ON UPDATE NO ACTION)
ENGINE = InnoDB;

create table user (
`id` varchar(10) NOT NULL,  
 `password` varchar(10) NULL,
`role` varchar(20) NULL,

PRIMARY KEY(`id`)

)ENGINE=InnoDB;

insert into customer (ssn,password,customer_level,name,address) values ("123456","pw11","normal","최윤선","abc");
insert into customer (ssn,password,customer_level,name,address) values ("124567","pw12","normal","홍길동","abc");
insert into customer (ssn,password,customer_level,name,address) values ("126789","pw13","normal","이순신","abc");
insert into customer (ssn,password,customer_level,name,address) values ("129087","pw14","normal","유재석","abc");
insert into customer (ssn,password,customer_level,name,address) values ("125242","pw15","normal","이광수","abc");
insert into customer (ssn,password,customer_level,name,address) values ("124085","pw16","normal","김종국","abc");
insert into customer (ssn,password,customer_level,name,address) values ("124549","pw17","normal","하동훈","abc");
insert into customer (ssn,password,customer_level,name,address) values ("122344","pw18","normal","송지효","abc");
insert into customer (ssn,password,customer_level,name,address) values ("129845","pw19","normal","전소민","abc");
insert into customer (ssn,password,customer_level,name,address) values ("124983","pw10","normal","양세찬","abc");

insert into user (id,password,role) values ("123456","pw11","customer");
insert into user (id,password,role) values ("124567","pw12","customer");
insert into user (id,password,role) values ("126789","pw13","customer");
insert into user (id,password,role) values ("129087","pw14","customer");
insert into user (id,password,role) values ("125242","pw15","customer");
insert into user (id,password,role) values ("124085","pw16","customer");
insert into user (id,password,role) values ("124549","pw17","customer");
insert into user (id,password,role) values ("122344","pw18","customer");
insert into user (id,password,role) values ("129845","pw19","customer");
insert into user (id,password,role) values ("124983","pw10","customer");
insert into user (id,password,role) values ("admin","admin","admin");

create view getCar as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Reservate_Date,Ssn,car.Num_seats,Engine_size
from vehicle,car where car.vin= vehicle.vin and vehicle.reservate_Date is NULL;

create view getSuv as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Reservate_Date,Ssn,suv.Num_seats,Size
from vehicle,suv where suv.vin= vehicle.vin and vehicle.reservate_Date is NULL;

create view getTruck as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Reservate_Date,Ssn,truck.Tonnage,No_axles
from vehicle,truck where truck.vin= vehicle.vin and vehicle.reservate_Date is NULL;

create view getMotorcycle as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Reservate_Date,Ssn,motorcycle.Level
from vehicle,motorcycle where motorcycle.vin= vehicle.vin and vehicle.reservate_Date is NULL;

create view reservCar as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Ssn,Reservate_Date, car.Num_seats, Engine_size
from vehicle, car where vehicle.vin =car.vin and vehicle.reservate_date is NOT NULL;

create view reservSuv as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Ssn,Reservate_Date, suv.Num_seats,Size
from vehicle,suv where vehicle.vin =suv.vin and vehicle.reservate_date is NOT NULL;

create view reservTruck as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Ssn,Reservate_Date,Truck.Tonnage,No_axles
from vehicle, truck where vehicle.vin =truck.vin and vehicle.reservate_date is NOT NULL;

create view reservMotor as select vehicle.Vin,Fuel_efficiency,Brand,Price,Sid,Ssn,Reservate_Date, motorcycle.Level
from vehicle, motorcycle where vehicle.vin =motorcycle.vin and vehicle.reservate_date is NOT NULL;

create index Vin_on_car on car (Vin) using btree;
create index Vin_on_suv on suv (Vin) using btree;
create index Vin_on_truck on truck (Vin) using btree;
create index Vin_on_motor on motorcycle (Vin) using btree;
create index Vin_on_vehicle on vehicle (Vin) using btree;

SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
