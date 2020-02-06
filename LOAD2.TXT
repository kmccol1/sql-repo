CREATE TABLE Phone

(

Phone_ID Number Not Null,
  
Phone_Number VARCHAR2(20) NOT NULL,

Phone_Type VARCHAR2(20) NOT NULL,

Contact_ID Number NOT NULL,
  
CONSTRAINT Phone_ID_PK PRIMARY KEY (Phone_ID),
  
CONSTRAINT Phone_ID_Contact_FK FOREIGN KEY (Contact_ID) REFERENCES Contact(Contact_ID)

);

CREATE TABLE Contact

(

Contact_ID Number Not Null,
  
First_Name VARCHAR2(20) NOT NULL,

Last_Name VARCHAR2(20) NOT NULL,
  
Street_Address VARCHAR2(100) NOT NULL,
  
City VARCHAR2(100) NOT NULL,
  
State VARCHAR2(2) NOT NULL,

Zipcode VARCHAR2(10) NOT NULL,

Email VARCHAR2(20) NOT NULL,

Web_Url VARCHAR2(20) NOT NULL,

Phone_ID VARCHAR2(10) NOT NULL,
  
CONSTRAINT Contact_ID_PK PRIMARY KEY (Contact_ID),
  
CONSTRAINT Contact_ID_Phone_FK FOREIGN KEY (Phone_ID) REFERENCES Phone(Phone_ID)

);

CREATE TABLE Agency

(

Agency_ID Number Not Null,
  
Agency_Name VARCHAR2(100) NOT NULL,
  
Street_Address VARCHAR2(100) NOT NULL,
  
City VARCHAR2(100) NOT NULL,
  
State VARCHAR2(2) NOT NULL,

Zipcode VARCHAR2(10) NOT NULL,

Phone VARCHAR2(10) NOT NULL,

Email VARCHAR2(20) NOT NULL,

Contact_ID Number NOT NULL,
  
CONSTRAINT Agency_ID_PK PRIMARY KEY (Agency_ID),
  
CONSTRAINT Agency_ID_Contact_FK FOREIGN KEY (Contact_ID) REFERENCES Contact(Contact_ID)

);

CREATE TABLE Project

(


Project_ID Number Not Null,
  
Description VARCHAR2(200) NOT NULL,

Agency_ID Number NOT NULL,
  
CONSTRAINT Project_ID_PK PRIMARY KEY (Project_ID),
  
CONSTRAINT Project_ID_Agency_FK FOREIGN KEY (Agency_ID) REFERENCES Agency(Agency_ID)

);

CREATE TABLE Project_Skill_Requirement

(

Project_ID Number Not Null,

Skill_ID Number NOT NULL,
  
CONSTRAINT Project_ID_PK PRIMARY KEY (Project_ID),

CONSTRAINT Skill_ID_PK PRIMARY KEY (Skill_ID),
  
CONSTRAINT Project_Skill_Requirement_ID_Skill_FK FOREIGN KEY (Skill_ID) REFERENCES Skill(Skill_ID),

CONSTRAINT Project_Skill_Requirement_ID_Project_FK FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID)

);

CREATE TABLE Skill

(

Skill_ID Number Not Null,
  
Skill_Name VARCHAR2(20) NOT NULL,
  
Description VARCHAR2(50) NOT NULL,
  
CONSTRAINT Skill_ID_PK PRIMARY KEY (Skill_ID),
  
);

CREATE TABLE Volunteer_Skill

(

Volunteer_ID Number Not Null,
  
Skill_ID Number NOT NULL,
  
CONSTRAINT Volunteer_PK PRIMARY KEY (Volunteer_ID),

CONSTRAINT Skill_PK PRIMARY KEY (Skill_ID),
  
CONSTRAINT Volunteer_Skill_Skill_FK FOREIGN KEY (Skill_ID) REFERENCES Skill(Skill_ID),

CONSTRAINT Volunteer_Skill_Volunteer_FK FOREIGN KEY (Volunteer_ID) REFERENCES Volunteer(Volunteer_ID)

);

CREATE TABLE Project_Offering

(

Project_Offering_ID Number Not Null,
  
Project_Date Number NOT NULL,

Num_Volunteer Number NOT NULL,

Num_Hour_Volunteer Number NOT NULL,

Contact_ID Number NOT NULL,

Project_ID Number NOT NULL,
  
CONSTRAINT Project_Offering_ID_PK PRIMARY KEY (Project_Offering_ID),
  
CONSTRAINT Project_Offering_Contact_FK FOREIGN KEY (Contact_ID) REFERENCES Contact(Contact_ID),

CONSTRAINT Project_Offering_Project_FK FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID)

);

CREATE TABLE Project_Category

(


Category_ID Number Not Null,
  
Project_ID Number NOT NULL,
  
CONSTRAINT Category_ID_PK PRIMARY KEY (Category_ID),

CONSTRAINT Project_ID_PK PRIMARY KEY (Project_ID),
  
CONSTRAINT Project_Category_Category_FK FOREIGN KEY (Category_ID) REFERENCES Category(Category_ID),

CONSTRAINT Project_Category_Project_FK FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID)

);

CREATE TABLE Category

(

Category_ID Number Not Null,
  
Category_Name VARCHAR2(20) NOT NULL,

Description VARCHAR2(50) NOT NULL,

CONSTRAINT Category_ID_PK PRIMARY KEY (Category_ID),

);

CREATE TABLE Assignment

(

Assignment_ID Number Not Null,
  
Is_Leader VARCHAR2(1) NOT NULL,
  
Project_Offering_ID Number NOT NULL,

Volunteer_ID Number NOT NULL,
  
CONSTRAINT Assignment_PK PRIMARY KEY (Assignment_ID),
  
CONSTRAINT Assignment_Project_Offering_FK FOREIGN KEY (Project_Offering_ID) REFERENCES Project_Offering(Project_Offering_ID),

CONSTRAINT Assignment_Volunteer_FK FOREIGN KEY (Volunteer_ID) REFERENCES Volunteer(Volunteer_ID)

);

CREATE TABLE Volunteer

(


Volunteer_ID Number Not Null,
  
Contact_ID Number NOT NULL,
  
CONSTRAINT Volunteer_PK PRIMARY KEY (Volunteer_ID),
  
CONSTRAINT Volunteer_Contact_FK FOREIGN KEY (Contact_ID) REFERENCES Contact(Contact_ID)

);

CREATE TABLE Category_For_Agency

(

Agency_Category_ID Number Not Null,
  
Agency_Category_Name VARCHAR2(20) NOT NULL,

Description VARCHAR2(100) NOT NULL,
  
CONSTRAINT Agency_Category_PK PRIMARY KEY (Agency_Category_ID),

);

CREATE TABLE Agency_Category

(

Agency_Category_ID Number Not Null,
  
Agency_ID Number NOT NULL,
  
CONSTRAINT Agency_Category_PK PRIMARY KEY (Agency_Category_ID),

CONSTRAINT Agency_Category_PK PRIMARY KEY (Agency_ID),

CONSTRAINT Agency_Category_Category_For_Agency_FK FOREIGN KEY (Agency_Category_ID) REFERENCES Agency_Category(Agency_Category_ID)

CONSTRAINT Agency_Category_Agency_FK FOREIGN KEY (Agency_ID) REFERENCES Agency(Agency_ID)


);

CREATE SEQUENCE Agency_Category_seq 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Agency_seq 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Contact_seq 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Phone_seq 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Category_For_Agency_seq           INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Volunteer_seq 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Assignment_seq		  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Category_SEQ 	  INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Project_Category_SEQ                INCREMENT BY 1 START WITH 1;

CREATE SEQUENCE Project_Offering_seq  		  INCREMENT BY 1 START WITH 1;

CREATE SEQUENCE Volunteer_Skill_seq           INCREMENT BY 1 START WITH 1;
CREATE SEQUENCE Skill_seq		  INCREMENT BY 1 START WITH 1;

CREATE SEQUENCE Project_Skill_Requirement_seq INCREMENT BY 1 START WITH 1;

CREATE SEQUENCE Project_seq		  INCREMENT BY 1 START WITH 1;





CREATE OR REPLACE TRIGGER INSERT_Agency_Category_seq
BEFORE INSERT ON Agency_Category
FOR EACH ROW
DECLARE
  new_id number;
BEGIN
  SELECT Agency_Category_seq.nextval INTO new_id FROM dual;
  :new.Agency_Category_ID := new_id;
END;
/

CREATE OR REPLACE TRIGGER INSERT_Agency_seq
BEFORE INSERT ON Agency
FOR EACH ROW
DECLARE
  new_id number;
BEGIN
  SELECT Agency_seq.nextval INTO new_id FROM dual;
  :new.Agency_ID := new_id;
END;
/

CREATE OR REPLACE TRIGGER INSERT_Category_For_Agency_seq
BEFORE INSERT ON Category_For_Agency
FOR EACH ROW
DECLARE
  new_id number;
BEGIN
  SELECT Category_For_Agency_seq.nextval INTO new_id FROM dual;
  :new.Agency_Category_ID := new_id;
END;
/

