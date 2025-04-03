**AMPRO - APP ( AMATEUR TO PROFESSIONAL FOOTBALL (SOCCER) SIMULATION DATABASE)**


TABLE OF CONTENTS

- [PROJECT OVERVIEW](#project-overview)
- [TOOLS](TOOLS)
- [PERSONAS](personas)
- [CODES](codes)


**PROJECT OVERVIEW**
![Picture of AMPRO database](https://github.com/user-attachments/assets/ea9ef1c1-5160-4f8c-93b9-93f3e78ad2be)

In order to complete the task of the application, I  first developed a database that will enable us provide insights into the attributes of current professional footballers in the world. This will provide the sample for which we can make predictions. 
The database will have key information such as the current earnings of players, their current teams, current playing positions, their attributes such as their height, weight, preferred foot, defending, attacking, stamina, strength, speed among others. 
The dataset will also be improved through inputs by some users who will enter their attributes such as their height, weight and other parameters who will want to predict their chances of playing for certain football teams. 
Finally, the development and hosting of the application that will allow the data to be analyzed to make predictions and prescriptions for amateur footballers to become professionals in the near future.

**TOOLS**
 - Excel - Data Cleaning
 - MySQL :Database and analysis
 - Draw.io [click here](https://draw.io/)

**PERSONAS**
The personas are the type of persons who are expected to use the application after deployment. Therefore for this application it is expected that the following persons or group of persons are expected to use this application: 
  1. Amateur Footballers
  2. Scouts/Agents
  3. Football clubs/teams
  4. Football associations

- Amateur Footballers;
These are the most likely user of the application as they would want to know based on their growth if the are likely to become professionals and what they are likely to earn in the future. It is expected that about 30 million people who are between the ages of 10 – 19 years are going to use the app globally based on the population of 45 million globally under this age bracket.   A user within this persona will add their height, weight, position, age and skillset. They will be able to check their suitability for particular teams, check potential future incomes and potential agents who work with their current similar clients.                                         

- Scouts/Agents;
They are likely to use the application to view the current players based on needs of teams they work for. This application can provide real-time data and analysis of a players potential and will allow the agent/scout to compare several players who are within a particular attribute bracket. They would be able to filter the names, age and location of certain players who fill a particular description using their height, foot preference, and other attributes.

- Teams;
Football clubs and teams will have the ability to follow players that match their required philosophy and required skills They can also use the application to match potential replacement for players. They can check the suitability of amateur players who can be groomed to fill in certain key positions based on their attributes such as stamina, speed, height and foot preferences. 

- Football Association;
The football associations will use this application to compile youth players and track their growth over time. The association can focus on amateur football using this application by getting a compilation of the data. They can will access the names, age, attributes and physical details of all members within their jurisdiction. 


![Screenshot of Output 1](https://github.com/user-attachments/assets/5180ae53-04c7-4d63-9043-4ed0717de68c)

![Screenshot of Output 2](https://github.com/user-attachments/assets/3df1703d-3a9f-46e4-a08a-c788572712fb)

**CODES**
 ```sql
CREATE SCHEMA IF NOT EXISTS `football` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `football` ;
-- -----------------------------------------------------
-- Table `football`.`academy`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`academy` ;

CREATE TABLE IF NOT EXISTS `football`.`academy` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(50) NULL DEFAULT NULL,
  `academy_location` VARCHAR(50) NULL DEFAULT NULL,
  `member_registration_id` INT NOT NULL,
  PRIMARY KEY (`id`, `member_registration_id`),
  INDEX `fk_academy_member1_idx` (`member_registration_id` ASC) VISIBLE,
  CONSTRAINT `fk_academy_member1`
    FOREIGN KEY (`member_registration_id`)
    REFERENCES `football`.`member` (`registration_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;

-- -----------------------------------------------------
-- Table `football`.`agent`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`agent` ;

CREATE TABLE IF NOT EXISTS `football`.`agent` (
  `idagent` INT NOT NULL,
  `agent_name` VARCHAR(50) NULL DEFAULT NULL,
  `member_registration_id` INT NOT NULL,
  PRIMARY KEY (`idagent`, `member_registration_id`),
  INDEX `fk_agent_member1_idx` (`member_registration_id` ASC) VISIBLE,
  CONSTRAINT `fk_agent_member1`
    FOREIGN KEY (`member_registration_id`)
    REFERENCES `football`.`member` (`registration_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `football`.`attributes`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`attributes` ;

CREATE TABLE IF NOT EXISTS `football`.`attributes` (
  `atb_index` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `stamina` INT NULL DEFAULT NULL,
  `strength` INT NULL DEFAULT NULL,
  `speed` INT NULL DEFAULT NULL,
  `defending` INT NULL DEFAULT NULL,
  `attacking` INT NULL DEFAULT NULL,
  `passing` INT NULL DEFAULT NULL,
  `weak_foot` INT NULL DEFAULT NULL,
  `position` VARCHAR(20) NULL DEFAULT NULL,
  `member_registration_id` INT NOT NULL,
  `team_idteam` INT NOT NULL,
  PRIMARY KEY (`atb_index`),
  INDEX `fk_attributes_member_idx` (`member_registration_id` ASC) VISIBLE,
  INDEX `fk_attributes_team1_idx` (`team_idteam` ASC) VISIBLE,
  CONSTRAINT `fk_attributes_member`
    FOREIGN KEY (`member_registration_id`)
    REFERENCES `football`.`member` (`registration_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_attributes_team1`
    FOREIGN KEY (`team_idteam`)
    REFERENCES `football`.`team` (`idteam`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 200
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `football`.`earnings`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`earnings` ;

CREATE TABLE IF NOT EXISTS `football`.`earnings` (
  `id` INT NOT NULL,
  `amount` INT NULL DEFAULT NULL,
  `contract_status` VARCHAR(20) NULL DEFAULT NULL,
  `duration` VARCHAR(10) NULL DEFAULT NULL,
  `team_idteam` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_earnings_team1_idx` (`team_idteam` ASC) VISIBLE,
  CONSTRAINT `fk_earnings_team1`
    FOREIGN KEY (`team_idteam`)
    REFERENCES `football`.`team` (`idteam`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `football`.`member`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`member` ;

CREATE TABLE IF NOT EXISTS `football`.`member` (
  `registration_id` INT NOT NULL AUTO_INCREMENT,
  `full_name` VARCHAR(30) NULL DEFAULT NULL,
  `age` INT NOT NULL,
  `foot` VARCHAR(10) NOT NULL,
  `date_of_birth` VARCHAR(20) NOT NULL,
  `height` INT NOT NULL,
  `weight` INT NOT NULL,
  `current_team` VARCHAR(45) NULL DEFAULT NULL,
  `current_agent` VARCHAR(45) NULL DEFAULT NULL,
  PRIMARY KEY (`registration_id`))
ENGINE = InnoDB
AUTO_INCREMENT = 200
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `football`.`team`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `football`.`team` ;

CREATE TABLE IF NOT EXISTS `football`.`team` (
  `idteam` INT NOT NULL AUTO_INCREMENT,
  `team_name` VARCHAR(45) NOT NULL,
  `teamcode` INT NULL DEFAULT NULL,
  `member_registration_id` INT NOT NULL,
  PRIMARY KEY (`idteam`),
  UNIQUE INDEX `idteam_UNIQUE` (`idteam` ASC) VISIBLE,
  INDEX `fk_team_member1_idx` (`member_registration_id` ASC) VISIBLE,
  CONSTRAINT `fk_team_member1`
    FOREIGN KEY (`member_registration_id`)
    REFERENCES `football`.`member` (`registration_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
AUTO_INCREMENT = 47
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;

-- -----------------------------------------------------
-- SELECT QUERIES FOR USERS
-- -----------------------------------------------------

SELECT m.registration_id, m.full_name, m.foot,
a.position, m.current_team,
a.speed, a.attacking
FROM member m
JOIN attributes a
ON m.registration_id=a.atb_index
WHERE stamina >80 and position='RM'
;

SELECT m.registration_id, m.full_name, m.age,
	m.foot, a.speed, a.defending,a.attacking, 
    a.position
FROM member m
JOIN attributes a
ON m.registration_id = a.atb_index;

SELECT avg(m.age) AS avg_age
FROM member m
JOIN attributes a
ON m.registration_id = a.atb_index
GROUP BY a.position;

SELECT m.registration_id, m.full_name, m.foot,
a.position, m.current_team,
a.speed, a.attacking
FROM member m
JOIN attributes a
ON m.registration_id=a.atb_index
WHERE current_team ='13';
```
